# Series 010 – HID-IIO Callback Setup and Device Exposure Ordering

## Executive Summary

This work addressed the ordering between HID sensor callback setup and IIO device exposure.

The initial v1 series described the problem as a race condition that could potentially result in NULL dereference or use-after-free and proposed ordering changes across nine HID-IIO drivers.

During review, maintainers challenged whether the claimed UAF or NULL-dereference failure mode could actually be demonstrated. Investigation of the IIO and HID sensor paths showed that the more defensible concern was a window in which the IIO device could become visible before the required sensor callback was registered, potentially resulting in dropped samples or stale data.

The v2 series therefore refined the problem statement, changed the title from "Fix race condition" to "Avoid race", removed the unsupported `Fixes:` tags, dropped the temperature-driver patch, and reduced the series to eight patches.

The final v2 series was applied through the IIO development flow and reached linux-next as eight commits.

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
| Last Verified | 2026-08-23 |
| Maintainers / Reviewers | Jonathan Cameron, Andy Shevchenko, Srinivas Pandruvada, Jiri Kosina, David Lechner, Nuno Sá |

## Background

The HID-IIO drivers register sensor callbacks and expose the corresponding IIO devices during probe.

The original ordering allowed the IIO device to become visible before callback registration was complete. The initial submission treated this as a possible race/UAF problem, but review required the failure mechanism to be demonstrated rather than inferred from the ordering alone.

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

## Initial Objective

Ensure callback setup was complete before the IIO device became externally visible and perform callback teardown in the correct order during device removal.

## Technical Evolution

### v1 – Race/UAF Fix

The initial nine-patch series reordered callback registration and IIO device registration and included a special temperature-driver change.

### Review – Failure Mode Challenged

Reviewers questioned whether the claimed UAF or NULL dereference could actually occur. Investigation did not establish a definite UAF.

### v2 – Ordering Improvement

The final revision changed the title to avoid overstating the issue, removed unsupported `Fixes:` tags, dropped the temperature-driver patch, refined the rationale and reduced the series to eight patches.

## Review Evolution

The most important lesson was to distinguish:

```text
Possible ordering problem
        ≠
Proven UAF
```

The final explanation focused on preventing an exposure window in which buffered capture could begin before callback setup was complete.

## Interesting Engineering Discussions

### `iio_device_register()` as an exposure boundary

Once registration completes, the IIO device can become visible to consumers. Required callbacks and resources should therefore be ready before crossing this boundary.

### Ordering and devm resource management

Correct ownership and teardown ordering must be understood before converting resources to managed lifetime. This makes the series technically related to the broader HID-IIO devm modernization work.

## Revision Timeline

| Revision | Patches | Major Evolution |
|----------|---------|-----------------|
| **v1** | 9 | Proposed race/UAF fix and reordered callback/device registration. |
| **Review** | — | Maintainers challenged the evidence for UAF/NULL dereference. |
| **v2** | 8 | Reframed as an ordering improvement, removed unsupported `Fixes:` tags and the temperature-driver patch. |

## Final / Current Outcome

| Item | Status |
|------|--------|
| Final Revision | v2 |
| Final Patch Count | 8 |
| Mainline | Not yet confirmed |
| linux-next | Applied |
| Final State | 8/8 v2 patches applied |
| Last Verified | 2026-08-23 |

## Why This Series Matters

This series demonstrates that upstream correctness is not only about changing code. The problem statement itself must be supported by evidence. Review changed the technical claim from a possible memory-safety failure to a defensible device-exposure ordering issue.

## Key Lessons Learned

- Prove the actual failure mechanism before describing a change as a bug fix.
- Distinguish a possible race window from a demonstrated UAF or NULL dereference.
- `iio_device_register()` represents an important device-exposure boundary.
- Required callbacks should be established before exposing the IIO device.
- Commit-message precision is part of technical correctness.
- `Fixes:` tags should only be used when a real historical bug or regression is established.

## Looking Back

If starting this work today, I would:

- Establish the exact callback and IIO registration paths before describing the issue.
- Demonstrate the claimed failure mode where possible.
- Separate an ordering improvement from a confirmed memory-safety bug.
- Avoid adding a `Fixes:` tag until the historical regression is established.

## Related Series

- [Series 008 – HID-IIO devm API and Resource-Management Modernization](series-008-hid-iio-devm-workstream.md)
- [Series 009 – IIO TODO Documentation](series-009-iio-todo-documentation.md)
- [Series 013 – HID Temperature Teardown Ordering](series-013-hid-temperature-teardown.md)

## Related Learning

- [Mentorship growth](../mentorship-growth.md)
- [Upstream review process](../upstream-review-process.md)

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
