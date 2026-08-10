# Series 008 – HID-IIO devm API and Resource-Management Modernization

## Executive Summary

This workstream began with a focused cleanup to remove a redundant `iio_dev` argument from `hid_sensor_remove_trigger()` and evolved into a broader effort to introduce device-managed resource handling for HID-IIO sensors.

Across five revisions, the work expanded from 10 patches to 36 patches before being substantially restructured. The v4 series combined basic coding-style cleanup, common device handling, API changes, and conversions across multiple HID-IIO drivers.

Rather than carrying the large v4 series forward, v5 was reorganized around the common device-managed API. Driver-specific conversions and related cleanup were separated into smaller independent series for focused review.

The resulting workstream demonstrates the transition from a mechanical cleanup into a broader driver resource-management modernization effort and, importantly, the use of review feedback to control series scope.

---

## Quick Facts

| Item | Details |
|------|---------|
| Workstream | HID-IIO devm API and resource-management modernization |
| Initial Title | iio: drop redundant iio_dev argument from hid_sensor_remove_trigger() |
| Latest Title | HID: iio: Introduce devm APIs for HID sensors |
| Subsystem | Industrial I/O (IIO) – HID Sensors |
| Initial Submission | 28 April 2026 |
| Latest Revision | v5 – 06 August 2026 |
| Revisions | v1 → v2 → v3 → v4 → v5 |
| Patch Count | v1: 10 → v2: 4 → v3: 9 → v4: 36 → v5: 13 |
| Final v5 Scope | Common device-managed HID sensor API |
| Maintainer | Jonathan Cameron |
| Primary Area | `drivers/iio/common/hid-sensors/` and HID-IIO drivers |
| Status | Active / split into independent series |

---

## Background

The work originated from an opportunity to simplify the HID sensor trigger cleanup API.

The existing `hid_sensor_remove_trigger()` function accepted a `struct iio_dev *` argument that was no longer required for resource cleanup. The initial series proposed removing this redundant parameter across the HID-IIO drivers.

During review, however, it became clear that the change was primarily useful as preparation for a broader device-managed API.

The resulting work therefore evolved from:

```text
remove redundant argument
```

into:

```text
introduce common devm API
        ↓
convert HID-IIO drivers
        ↓
modernize resource ownership
```

---

## Initial Objective

### v1

The initial 10-patch series focused on:

- removing the redundant `iio_dev` argument;
- updating HID-IIO drivers to the new function signature;
- preparing the common trigger handling for future device-managed cleanup.

The original submission described the change as mechanical and without functional impact.

---

## Review-Driven Direction Change

During review, Andy Shevchenko pointed out that the unused argument was retained for consistency with related APIs and rejected the initial approach as a standalone change.

The discussion clarified that removing the argument made more sense as part of the larger devm conversion.

Jonathan Cameron subsequently suggested showing the complete devm wrapper approach as a precursor and emphasized that the series should remain applicable one patch at a time without breaking the build.

This became the key turning point in the workstream.

---

## Revision Evolution

### v1 – Remove redundant `iio_dev` argument

**10 patches**

The series focused on the common API and all affected HID-IIO callers.

The main idea was:

```text
hid_sensor_remove_trigger(indio_dev, attrb)
                ↓
hid_sensor_remove_trigger(attrb)
```

This was intended as preparation for future devm-based trigger management.

---

### v2 – Introduce the devm API

**4 patches**

The series was reframed around introducing a device-managed HID sensor setup/cleanup API.

The focus shifted from changing the existing API in isolation to providing a reusable managed-resource abstraction.

---

### v3 – Common API + initial conversions

**9 patches**

The series expanded to include:

- common devm API;
- redundant argument removal;
- initial driver conversions;
- common device handling;
- supporting cleanup.

The work was now clearly becoming a reusable infrastructure change rather than a single cleanup.

---

### v4 – Broad HID-IIO modernization

**36 patches**

The series expanded substantially and combined several logical categories.

#### Basic cleanup

- missing blank lines;
- `unsigned` → `u32`;
- parenthesis alignment.

#### Common device handling

Several drivers were converted to use a common device for devres.

Additional drivers introduced local `struct device *` handling.

#### Common API

The redundant `iio_dev` argument was removed from the common trigger cleanup interface.

#### Device-managed trigger cleanup

Multiple HID-IIO drivers were converted from explicit:

```text
hid_sensor_remove_trigger()
```

to device-managed trigger cleanup.

The affected driver groups included:

- gyro;
- humidity;
- light;
- magnetometer;
- orientation;
- position;
- pressure;
- temperature;
- proximity.

The v4 series therefore combined common infrastructure, cleanup, and repeated driver conversions into one large submission.

---

## v4 Scope

The 36-patch v4 series contained several distinct logical groups:

```text
Basic cleanup
      +
Common device handling
      +
API modification
      +
devm API introduction
      +
Driver conversions
```

This broad scope made the series difficult to review and independently apply.

---

## v5 – Major Restructuring

**13 patches**

Instead of carrying the 36-patch v4 series forward, the work was reorganized.

The v5 series retained the focused common devm API work while related driver conversions and cleanup were moved into separate series.

The resulting structure became:

```text
                 HID-IIO modernization
                         │
                    v4: 36 patches
                         │
          ┌──────────────┼──────────────┐
          │              │              │
      cleanup       common devm     driver
                     API           conversions
                         │              │
                         ↓              ↓
                    v5: 13       independent
                    patches       child series
```

This was not simply a reduction from 36 to 13 patches.

It was a change in the architecture of the contribution itself.

---

## Engineering Scope

### Common device-managed API

The central contribution is the introduction of reusable device-managed HID sensor setup/cleanup infrastructure.

The objective is to make resource ownership follow the device lifecycle and reduce explicit teardown plumbing in individual drivers.

---

### Common `struct device` handling

Several drivers were converted to use the appropriate common device for devres operations.

This makes the ownership of device-managed resources explicit and consistent.

---

### Trigger cleanup

The original redundant `iio_dev` argument was removed as part of the broader devm conversion.

The eventual direction is:

```text
manual setup
    +
manual remove
        ↓
device-managed setup
    +
automatic cleanup
```

---

### Driver conversions

The v4 series demonstrated that the common API could be adopted by a large number of HID-IIO drivers.

Rather than retaining all of these conversions in the parent series, v5 moved them toward independent follow-up submissions.

---

## Review Evolution

### API consistency

Andy Shevchenko questioned removing the unused `iio_dev` argument independently because related APIs retained the parameter for consistency.

This established that an apparently redundant parameter can still have an interface-design purpose.

---

### Devm design

The discussion moved toward introducing:

```text
devm_hid_sensor_setup_trigger()
```

with cleanup registered through the device-managed resource framework.

This made the original argument removal a supporting change rather than the primary objective.

---

### Patch independence

Jonathan Cameron emphasized that a series should be applicable one patch at a time without breaking anything.

This became particularly important as the work expanded.

The v4 series demonstrated why combining infrastructure, cleanup and driver conversions into one large series makes independent application more difficult.

---

### Series scope

The eventual v5 restructuring separated:

```text
common infrastructure
```

from:

```text
driver adoption
```

This reduced review complexity and allowed maintainers to evaluate the API independently from the many consumer conversions.

---

## Review Summary

| Reviewer | Main Contribution |
|----------|-------------------|
| **Jonathan Cameron** | Guided the transition toward a common devm API, emphasized patch independence, and drove the restructuring into reviewable units. |
| **Andy Shevchenko** | Challenged the initial redundant-argument removal, highlighted API consistency, and provided guidance on the proper scope of the cleanup. |
| **David Lechner** | Participated in review of the common API and HID-IIO driver changes. |
| **Christophe JAILLET** | Reviewed individual driver conversion details. |
| **Srinivas Pandruvada** | Provided HID sensor subsystem context and review input. |

---

## Interesting Engineering Discussions

### 1. Redundant does not always mean removable

The `iio_dev` argument was technically unused by the cleanup implementation, but its presence was consistent with related APIs.

This demonstrated that API design must consider consistency and future usage, not only whether a parameter is currently referenced.

---

### 2. Cleanup can be preparation for infrastructure

The initial argument-removal patch was not valuable enough by itself.

Its real value emerged when it became part of the larger devm API design.

---

### 3. Common infrastructure should be separated from consumers

The v4 series demonstrated the difficulty of combining:

```text
API introduction
+
API adoption
+
driver cleanup
```

The v5 restructuring separated the common infrastructure from individual driver conversions.

---

### 4. Large series should evolve with review

The series grew from 10 patches to 36 patches as additional opportunities were identified.

Rather than defending the large scope, the final revision reduced the parent series to 13 patches and moved related work into independent submissions.

---

## Revision Timeline

| Revision | Patches | Major Evolution |
|----------|---------|-----------------|
| **v1** | 10 | Remove redundant `iio_dev` argument and update affected drivers. |
| **v2** | 4 | Reframed around introducing a device-managed HID sensor API. |
| **v3** | 9 | Added common devm API, initial conversions and supporting cleanup. |
| **v4** | 36 | Expanded into broad HID-IIO cleanup, common device handling, API introduction and driver conversions. |
| **v5** | 13 | Restructured into a focused common devm API series; related driver conversions moved to independent series. |

---

## Parent / Child Workstream Structure

This series should be treated as the **parent workstream**.

| Work Item | Relationship |
|-----------|--------------|
| Original redundant `iio_dev` argument series | Starting point |
| HID sensor devm API | **Parent/common infrastructure** |
| Individual HID-IIO driver conversions | Child series |
| Additional HID-IIO cleanup | Related child series |
| Remaining conversions | Follow-up work |

The child series should receive their own repository entries once their Lore history and final outcomes are documented.

---

## Current Status

| Item | Status |
|------|--------|
| Current Revision | v5 |
| Final v5 Patches | 13 |
| Parent Series | Active / under review |
| Common API | Focused parent work |
| Driver Conversions | Split into independent series |
| Mainline | Track parent and child series separately |
| Overall State | Active upstream workstream |

---

## Key Lessons Learned

- An apparently redundant API parameter may exist for interface consistency.
- Infrastructure changes should be separated from their many consumers when possible.
- A large cleanup series should be continuously evaluated for logical boundaries.
- A series should remain independently applicable patch by patch.
- Common devm infrastructure is often better reviewed separately from driver conversions.
- Scope reduction after review is a sign of improved patch organization, not failure.
- Related driver conversions can continue independently once the common infrastructure is established.
- Upstream review can change the architecture of a contribution, not merely individual lines of code.

---

## Looking Back

If starting this work today, I would:

- Identify the intended devm API before proposing the redundant-argument cleanup.
- Introduce the common infrastructure separately from driver conversions.
- Avoid combining basic style cleanup with infrastructure and consumer changes.
- Check patch independence continuously as the series grows.
- Split driver conversions earlier once the common API is stable.

---

## Related Series

- [Series 000 – Exploratory cleanup.h](series-000-exploratory-cleanup-h.md)
- [Series 001 – ST Sensors buffer reuse](series-001-st-sensors-buffer-reuse.md)
- [Series 002 – SSP Sensors modernization](series-002-ssp-sensors-modernization.md)
- [Series 003 – GC0310 clock modernization](series-003-gc0310-clock-modernization.md)
- [Series 004 – AD7173 checkpatch analysis](series-004-ad7173-checkpatch-analysis.md)
- [Series 005 – MMA8452 modernization](series-005-mma8452-modernization.md)
- [Series 006 – ADXL accelerometer cleanup](series-006-adxl-accelerometer-cleanup.md)
- [Series 007 – ADI IIO MAINTAINERS coverage](series-007-adi-iio-maintainers.md)

### Child Series

> Add links here as the independent HID-IIO driver conversion series are documented.

---

## Related Learning

- [Review Process](../learning/review-process.md)

---

## References

### Lore

- [v1 – redundant `iio_dev` argument](https://www.spinics.net/lists/kernel/msg6174839.html)
- v2 – devm API introduction
- v3 – common API and initial conversions
- [v4 – 36-patch HID-IIO modernization](https://lkml.iu.edu/2605.3/index.html)
- v5 – focused devm API series

### Related Discussions

- [Andy Shevchenko – API consistency review](https://www.spinics.net/lists/kernel/msg6175082.html)
- [Jonathan Cameron – patch independence and devm direction](https://www.spinics.net/lists/kernel/msg6176514.html)
