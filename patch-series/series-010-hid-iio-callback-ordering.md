# Series 010 – HID-IIO Callback Setup and Device Exposure Ordering

## Executive Summary

This work addressed the ordering between HID sensor callback setup and IIO device exposure.

The initial v1 series described the problem as a race condition that could potentially result in NULL dereference or use-after-free and proposed ordering changes across nine HID-IIO drivers.

During review, maintainers challenged whether the claimed UAF or NULL-dereference failure mode could actually be demonstrated. Investigation of the IIO and HID sensor paths showed that the more defensible concern was a window in which the IIO device could become visible before the required sensor callback was registered, potentially resulting in dropped samples or stale data.

The v2 series therefore refined the problem statement, changed the title from "Fix race condition" to "Avoid race", removed the unsupported `Fixes:` tags, dropped the temperature-driver patch, and reduced the series to eight patches.

The final v2 series was applied through the IIO development flow and reached linux-next as eight commits.

---

## Quick Facts

| Item | Details |
|------|---------|
| Series | HID: iio: Avoid race between callback setup and device exposure |
| Subsystem | Industrial I/O (IIO) / HID Sensors |
| Initial Submission | 06 June 2026 |
| Final Revision | v2 – 22 June 2026 |
| Revisions | v1 → v2 |
| Initial Patch Count | 9 |
| Final Patch Count | 8 |
| Final Drivers | 8 HID-IIO drivers |
| Status | Applied in linux-next |
| Mainline | Not yet confirmed |
| Maintainers / Reviewers | Jonathan Cameron, Andy Shevchenko, Srinivas Pandruvada, Jiri Kosina, David Lechner, Nuno Sá |

---

## Background

The HID-IIO drivers register sensor callbacks and expose the corresponding IIO devices during probe.

The original ordering allowed the IIO device to become visible before callback registration was complete.

The initial submission treated this as a possible race/UAF problem. Review required the failure mechanism to be demonstrated rather than inferred from the ordering alone.

The investigation showed that the strongest defensible concern was the exposure window itself:

```text
iio_device_register()
        ↓
IIO device becomes visible
        ↓
consumer may enable buffered capture
        ↓
sensor callback registered
```

During this window, sensor data handling may not yet be fully available.

The resulting v2 series therefore focused on preventing the exposure window rather than claiming a proven memory-safety failure.

---

## Initial Objective

The initial goal was to ensure callback setup was complete before the IIO device became externally visible and to perform callback teardown in the correct order during device removal.

The intended ordering was:

### Probe

```text
callback setup
      ↓
iio_device_register()
      ↓
device exposed
```

### Remove

```text
device exposure removed
      ↓
callback/resource teardown
```

---

## Revision Evolution

### v1 – Race/UAF Fix

**9 patches**

The initial series:

- described the issue as a race condition;
- suggested possible NULL dereference/UAF;
- reordered callback registration and IIO device registration;
- reordered callback teardown and IIO device unregistration;
- included a special temperature-driver change using non-devm `iio_device_register()`.

---

### Review – Failure Mode Challenged

Reviewers questioned whether the claimed UAF or NULL dereference could actually occur.

The key question became:

> What concrete execution path demonstrates the claimed memory-safety failure?

Investigation of the IIO registration and HID callback paths did not establish a definite UAF.

Instead, the ordering still represented a real exposure window that could allow buffered capture to begin before callback setup was complete.

---

### v2 – Ordering Improvement

**8 patches**

The final revision:

- changed the title from **"Fix race condition"** to **"Avoid race"**;
- removed the temperature-driver patch;
- removed unsupported `Fixes:` tags;
- refined the commit-message rationale;
- focused on callback setup before device exposure;
- described the practical impact more conservatively as possible sample loss/stale data;
- retained the ordering improvement across eight HID-IIO drivers.

---

## Technical Change

The core ordering principle is:

```text
Before:

iio_device_register()
        ↓
device exposed
        ↓
callback registration

After:

callback registration
        ↓
iio_device_register()
        ↓
device exposed
```

For teardown:

```text
Before:

callback/resource teardown
        ↓
iio_device_unregister()

Preferred:

iio_device_unregister()
        ↓
callback/resource teardown
```

The exact implementation differs between drivers, but the common objective is to avoid exposing a partially initialized or partially torn-down sensor.

---

## Review Summary

| Reviewer | Key Contribution |
|----------|------------------|
| **Jonathan Cameron** | Challenged whether the original UAF claim was demonstrable, identified possible sample-loss implications, and guided the correction of the problem statement. Applied the final v2 series. |
| **Srinivas Pandruvada** | Questioned the original UAF claim and agreed with the more realistic sample-loss/stale-data interpretation. |
| **Andy Shevchenko** | Challenged unsupported bug claims and reviewed the treatment of review tags after substantial commit-message changes. |
| **David Lechner** | Participated in review of the HID-IIO implementation and ordering changes. |
| **Nuno Sá / Jiri Kosina** | Included in the broader review and subsystem discussion. |

---

## Important Review Discussion

### Prove the claimed failure mode

The most important change was understanding that:

> A suspicious ordering is not automatically a proven UAF.

The initial patch described a potentially severe memory-safety problem.

Review forced the investigation to distinguish between:

```text
Possible ordering problem
        ≠
Proven UAF
```

The final patch therefore used technically defensible wording.

---

## Interesting Engineering Discussion

### `iio_device_register()` as an exposure boundary

Calling `iio_device_register()` is not simply an internal initialization step.

Once registration completes, the IIO device can become visible to consumers.

Therefore, required callbacks and resources should be ready before crossing that boundary.

This is particularly important for buffered data capture.

---

### Ordering and devm resource management

This series also provides an important prerequisite for the broader HID-IIO devm modernization work.

Before converting resources to managed lifetime, the correct ownership and teardown ordering must be understood.

This makes Series 010 technically related to the HID-IIO devm workstream documented in Series 008.

---

## Revision Timeline

| Revision | Patches | Major Evolution |
|----------|---------|-----------------|
| **v1** | 9 | Proposed race/UAF fix and reordered callback/device registration across HID-IIO drivers. |
| **Review** | — | Maintainers challenged the evidence for UAF/NULL dereference and requested a more precise failure description. |
| **v2** | 8 | Reframed as avoiding an ordering race, removed unsupported `Fixes:` tags and temperature-driver change, and refined the technical rationale. |

---

## Final Outcome

| Item | Status |
|------|--------|
| Final Revision | v2 |
| Final Patch Count | 8 |
| Mainline | Not yet confirmed |
| linux-next | ✅ Applied |
| Final State | 8/8 v2 patches applied |
| Outcome | Accepted through IIO development flow |

---

## linux-next Commits

The final v2 series reached linux-next through these eight commits:

1. `0e32649a7cf3cd784862f8dc0c68a5134731bfff`
2. `28afc251ad71646d501191225ddd4db57c670a47`
3. `50d8d72e4f28202e18a687ed868ddd3225b2ac1b`
4. `724d0351cd08eb93f3cd9021c3a26ce1f1c79f7f`
5. `49e663471992611f586598d2bbd23f94b760f9fa`
6. `7d362d339391780c964b06bec9b209b0f9e229b4`
7. `3e37afb5697e1b30bd739fe38909d3dbf2493bb9`
8. `eb787019c42072cf13470afca673dab0b49cabb6`

---

## Key Lessons Learned

- Prove the actual failure mechanism before describing a change as a bug fix.
- Distinguish a possible race window from a demonstrated UAF or NULL dereference.
- `iio_device_register()` represents an important device-exposure boundary.
- Required callbacks should be established before exposing the IIO device.
- Teardown ordering must prevent consumers from observing partially destroyed state.
- Commit-message precision is part of technical correctness.
- `Fixes:` tags should only be used when a real historical bug/regression is established.
- Substantial changes to the rationale may justify requesting fresh review even when implementation changes are small.
- Review feedback can legitimately reduce the severity of the claim while still preserving the value of the fix.

---

## Looking Back

If starting this work today, I would:

- Establish the exact callback and IIO registration paths before describing the issue.
- Reproduce or demonstrate the claimed failure mode where possible.
- Separate "ordering improvement" from "confirmed memory-safety bug".
- Avoid adding a `Fixes:` tag until the historical regression is established.
- Review the interaction with devm-based teardown before changing resource ownership.

---

## Related Series

- [Series 008 – HID-IIO devm API and Resource-Management Modernization](series-008-hid-iio-devm-workstream.md)
- [Series 009 – IIO TODO Documentation](series-009-iio-todo-documentation.md)

### Workstream Relationship

Series 010 is technically related to Series 008:

```text
Series 008
HID-IIO devm modernization
        │
        │ requires correct resource
        │ ownership / teardown ordering
        ↓
Series 010
Callback setup ↔ IIO device exposure
ordering correctness
```

---

## References

### Lore

- [v1 – HID-IIO race fixes](https://lore.kernel.org/all/20260606-5-june-hid-iio-race-fixes-v1-0-27a848c5758f@gmail.com/)
- [v2 – HID-IIO ordering improvement](https://lore.kernel.org/all/20260622-5-june-hid-iio-race-fixes-v2-0-1cfabcd1881e@gmail.com/)

### linux-next

- `0e32649a7cf3cd784862f8dc0c68a5134731bfff`
- `28afc251ad71646d501191225ddd4db57c670a47`
- `50d8d72e4f28202e18a687ed868ddd3225b2ac1b`
- `724d0351cd08eb93f3cd9021c3a26ce1f1c79f7f`
- `49e663471992611f586598d2bbd23f94b760f9fa`
- `7d362d339391780c964b06bec9b209b0f9e229b4`
- `3e37afb5697e1b30bd739fe38909d3dbf2493bb9`
- `eb787019c42072cf13470afca673dab0b49cabb6`
