# Series 008 – HID-IIO devm API and Resource-Management Modernization

## Executive Summary

This workstream began with a focused cleanup to remove a redundant `iio_dev` argument from `hid_sensor_remove_trigger()` and evolved into a broader effort to introduce device-managed resource handling for HID-IIO sensors.

Across five revisions, the work expanded from 10 patches to 36 patches before being substantially restructured. The v4 series combined basic coding-style cleanup, common device handling, API changes, and conversions across multiple HID-IIO drivers.

Rather than carrying the large v4 series forward, v5 was reorganized around the common device-managed API. Driver-specific conversions and related cleanup were separated into smaller independent series for focused review.

The resulting workstream demonstrates the transition from a mechanical cleanup into a broader driver resource-management modernization effort and, importantly, the use of review feedback to control series scope.

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
| Status | Under Review |
| Last Verified | 2026-08-23 |

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

## Initial Objective

The initial 10-patch series focused on:

- removing the redundant `iio_dev` argument;
- updating HID-IIO drivers to the new function signature;
- preparing the common trigger handling for future device-managed cleanup.

The original submission described the change as mechanical and without functional impact.

## Technical Evolution

### v1 – Remove redundant `iio_dev` argument

The series focused on the common API and all affected HID-IIO callers.

### v2 – Introduce the devm API

The series was reframed around introducing a device-managed HID sensor setup/cleanup API.

### v3 – Common API + initial conversions

The series expanded to include the common devm API, redundant argument removal, initial driver conversions, common device handling and supporting cleanup.

### v4 – Broad HID-IIO modernization

The series expanded to 36 patches and combined several logical categories:

- basic coding-style cleanup;
- common device handling;
- API modification;
- devm API introduction;
- driver conversions.

### v5 – Major restructuring

The v5 series retained the focused common devm API work while driver-specific conversions and related cleanup were moved into independent series.

## Review Evolution

### API consistency

Andy Shevchenko questioned removing the unused `iio_dev` argument independently because related APIs retained the parameter for consistency.

This established that an apparently redundant parameter can still have an interface-design purpose.

### Devm design

The discussion moved toward introducing a reusable device-managed setup/cleanup API. The original argument removal became a supporting change rather than the primary objective.

### Patch independence

Jonathan Cameron emphasized that a series should be applicable one patch at a time without breaking anything. This became particularly important as the work expanded.

### Series scope

The v5 restructuring separated common infrastructure from driver adoption, reducing review complexity and allowing maintainers to evaluate the API independently from consumer conversions.

## Interesting Engineering Discussions

### 1. Redundant does not always mean removable

An unused parameter can still serve API consistency. Interface design must consider related APIs and subsystem conventions, not only whether a parameter is locally referenced.

### 2. Cleanup can be preparation for infrastructure

The initial argument-removal change gained clearer value when incorporated into a larger devm API design.

### 3. Common infrastructure should be separated from consumers

Combining API introduction, adoption and driver cleanup in one large series makes independent application and review harder. The v5 restructuring corrected this.

### 4. Large series should evolve with review

The series grew from 10 to 36 patches as additional opportunities were identified, then was reduced to a focused parent series with independent follow-ups.

## Revision Timeline

| Revision | Patches | Major Evolution |
|----------|---------|-----------------|
| **v1** | 10 | Remove redundant `iio_dev` argument and update affected drivers. |
| **v2** | 4 | Reframed around introducing a device-managed HID sensor API. |
| **v3** | 9 | Added common devm API, initial conversions and supporting cleanup. |
| **v4** | 36 | Expanded into broad HID-IIO cleanup, common device handling, API introduction and driver conversions. |
| **v5** | 13 | Restructured into a focused common devm API series; related driver conversions moved to independent series. |

## Final / Current Outcome

| Item | Status |
|------|--------|
| Current Revision | v5 |
| Patch Count | 13 |
| Status | Under Review |
| Common API | Focused parent work |
| Driver Conversions | Split into independent series |
| Mainline | Not yet confirmed |

## Why This Series Matters

This workstream demonstrates that upstream modernization is not simply about converting APIs. The contribution evolved from an apparently small cleanup into infrastructure design, resource ownership reasoning, and deliberate separation of common framework work from consumer-driver changes.

## Key Lessons Learned

- An apparently redundant API parameter may exist for interface consistency.
- Infrastructure changes should be separated from their consumers when possible.
- A large cleanup series should be continuously evaluated for logical boundaries.
- A series should remain independently applicable patch by patch.
- Common devm infrastructure is often better reviewed separately from driver conversions.
- Scope reduction after review is improved patch organization, not failure.
- Upstream review can change the architecture of a contribution, not merely individual lines of code.

## Looking Back

If starting this work today, I would:

- Identify the intended devm API before proposing the redundant-argument cleanup.
- Introduce common infrastructure separately from driver conversions.
- Avoid combining basic style cleanup with infrastructure and consumer changes.
- Check patch independence continuously as the series grows.
- Split driver conversions earlier once the common API is stable.

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

## Related Learning

- [Mentorship growth](../mentorship-growth.md)
- [Upstream review process](../upstream-review-process.md)

## References

### Lore

- [v1 – redundant `iio_dev` argument](https://www.spinics.net/lists/kernel/msg6174839.html)
- [v4 – 36-patch HID-IIO modernization](https://lkml.iu.edu/2605.3/index.html)
- v2 – devm API introduction
- v3 – common API and initial conversions
- v5 – focused devm API series
