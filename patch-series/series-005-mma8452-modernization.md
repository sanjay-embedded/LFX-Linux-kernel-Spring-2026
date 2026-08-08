# Series 005 – MMA8452: Modern Coding Style, PM and Resource Cleanup

## Executive Summary

This work began as a focused PM modernization to use `pm_ptr()` for the MMA8452 driver's `dev_pm_ops`. Review of the initial patch identified that the PM callback macros also needed to be modernized to avoid unused-function warnings.

The work subsequently expanded into a broader driver modernization series covering coding style, PM handling, IRQ resource lifetime, regulator management, IIO direct-mode cleanup, mutex cleanup and error propagation.

During the review process, the modernization work also exposed two race conditions that required correction. The series was subsequently refined and reduced across revisions as individual changes were accepted or separated from the remaining work.

The latest revision represents the remaining incremental modernization work rather than a single monolithic series.

---

## Quick Facts

| Item | Details |
|------|---------|
| Series | iio: accel: mma8452: use modern coding style and resource cleanup |
| Subsystem | Industrial I/O (IIO) |
| Driver | MMA8452 accelerometer |
| Initial Submission | 14 April 2026 |
| Latest Revision | v5 – 08 August 2026 |
| Revisions | Initial → v2 → v3 → v4 → v5 |
| Patch Count | 1 → 6 → 10 → 5 → 4 |
| Status | Partially accepted |
| Current State | Incremental continuation of remaining work |
| Maintainer | Jonathan Cameron |

---

## Background

The work started with a focused PM cleanup for the MMA8452 driver.

The initial goal was to modernize the driver's PM handling using `pm_ptr()`. During review, it became clear that the existing PM callback definitions also needed to be modernized to avoid compiler warnings.

The investigation then identified additional opportunities to improve resource management and driver structure. The work gradually evolved into a broader modernization effort while remaining within the MMA8452 driver.

This series also followed lessons from earlier upstream work, particularly the need to separate logical changes and allow maintainers to accept valuable patches independently.

---

## Initial Objective

The original patch focused on:

- Using `pm_ptr()` for `dev_pm_ops`.
- Modernizing PM handling.
- Removing unnecessary conditional PM code.

During review, this proved to be more involved than a simple one-line conversion.

---

## Technical Evolution

### Phase 1 – Focused PM Modernization

**Initial submission**

The series started as a single patch:

`iio: accel: mma8452: use pm_ptr() for dev_pm_ops`

Review identified that `pm_ptr()` alone did not address the PM callback definitions and associated unused-function warnings.

The PM implementation therefore needed to use the appropriate modern PM helper pattern.

---

### Phase 2 – Driver Modernization (v2)

The work expanded into six patches covering:

- Coding-style cleanup.
- Header organization.
- Local `struct device` usage.
- `dev_err_probe()`.
- PM modernization.
- `guard()`-based mutex cleanup.

The series remained focused on modernization without intended functional changes.

---

### Phase 3 – Correctness and Resource Management (v3)

The third revision expanded to ten patches.

The work introduced:

- I2C error propagation.
- Explicit IRQ resource management.
- Bulk regulator handling.
- IIO direct-mode cleanup helpers.
- PM refinements.
- Additional resource-lifetime cleanup.

During this stage, review exposed two race conditions that required attention.

This was an important transition: the series was no longer only about coding style or API modernization; it also addressed driver correctness and resource lifetime.

---

### Phase 4 – Refinement After Partial Acceptance (v4)

After individual changes from v3 were accepted, the remaining work was reduced to five patches.

The series concentrated on the remaining:

- Bulk regulator conversion.
- Local `struct device`.
- PM modernization.
- IIO cleanup helpers.
- `guard()` mutex handling.

This demonstrated that the complete series did not need to be accepted as a single unit.

---

### Phase 5 – Remaining Modernization (v5)

The latest revision further reduced the series to four patches.

The work continued to focus on modern coding style and resource cleanup after previously accepted changes had been separated from the remaining work.

---

## Review Evolution

### PM implementation

Review identified that the initial `pm_ptr()` conversion was incomplete because the PM callback definitions still used the older PM-op macros.

The discussion led to adoption of the appropriate modern PM helper pattern.

---

### Race conditions

The cleanup work exposed two race conditions.

This changed the priority of the series from purely modernization to addressing correctness issues before continuing with the cleanup.

---

### IRQ resource lifetime

The series changed from `devm_request_threaded_irq()` to explicit IRQ management because resource release ordering mattered for the driver's error and teardown paths.

The resulting change was accepted independently, while its `Fixes:` tag was removed because the implementation was not considered an actual regression.

---

## Review Summary

| Reviewer | Main contribution |
|----------|-------------------|
| **Jonathan Cameron** | Guided PM implementation, identified race conditions, reviewed resource ordering and IIO cleanup design, and accepted individual changes independently. |
| **Andy Shevchenko** | Reviewed coding style, `guard()` usage, device pointer handling, regulator conversion, structure layout and patch organization. |
| **David Lechner** | Reviewed resource management and implementation details. |
| **Joshua Crofts** | Raised concerns around patch independence and dependency between patches. |
| **Geert Uytterhoeven** | Identified the limitation of the initial `pm_ptr()` conversion and recommended the appropriate PM helper approach. |
| **Kernel test robot** | Reported build/compiler warnings that helped identify issues in the initial PM implementation. |

---

## Interesting Engineering Discussions

- `pm_ptr()` conversion is not always a mechanical one-line change.
- PM helper macros must be considered together with callback definitions.
- Resource cleanup can expose latent race conditions.
- `devm_*` is not automatically preferable when resource ordering matters.
- IRQ lifetime and teardown ordering must be considered before converting to managed resources.
- Bulk regulator APIs can simplify related resource handling.
- IIO provides subsystem-specific cleanup helpers that can be preferable to generic cleanup mechanisms.
- A `Fixes:` tag should identify a real bug or regression rather than simply an undesirable implementation.
- Individual patches should remain independently understandable because maintainers may partially apply a series.

---

## Revision Timeline

| Revision | Patches | Major Evolution |
|----------|---------|-----------------|
| **Initial** | 1 | Focused PM modernization using `pm_ptr()`. |
| **v2** | 6 | Expanded into coding-style, PM and resource-management modernization. |
| **v3** | 10 | Added correctness fixes, IRQ/resource lifetime changes, bulk regulators and IIO cleanup helpers. |
| **v4** | 5 | Reduced after partial acceptance and focused on remaining modernization work. |
| **v5** | 4 | Further reduced continuation of remaining cleanup and modernization. |

---

## Partial Acceptance

The series was not accepted as one unit.

Individual patches were reviewed and accepted independently, while the remaining work continued through subsequent revisions.

This is an important part of the series' evolution:

```text
Initial focused PM change
        ↓
Broader modernization
        ↓
Correctness issues discovered
        ↓
Individual patches accepted
        ↓
Series reduced
        ↓
Remaining work continues
```

---

## Current Status

| Item               | Status                   |
| ------------------ | ------------------------ |
| Complete series    | ❌ Not merged as a whole  |
| Individual patches | ✅ Partially accepted     |
| v3 changes         | Partially accepted       |
| Latest revision    | v5                       |
| Current state      | Incremental continuation |
| Remaining work     | Under review             |

---

## Key Lessons Learned

* A seemingly simple API modernization can require understanding the complete subsystem infrastructure.
* Cleanup work should include careful analysis of resource lifetime and concurrency.
* Modern `devm_*` APIs should not be introduced mechanically when teardown ordering matters.
* Review can uncover correctness problems that were not the original objective of a cleanup.
* Maintainers may accept valuable patches independently rather than waiting for an entire series.
* Large series should be continuously reconsidered and reduced as individual patches become independently mergeable.
* `Fixes:` tags require evidence of a real bug or regression.
* Patch independence is important when maintainers may partially apply a series.

---

## Looking Back

If starting this work today, I would:

* Investigate the complete PM callback infrastructure before submitting the initial `pm_ptr()` conversion.
* Separate correctness fixes from modernization changes earlier.
* Identify resource-ordering constraints before considering `devm_*` conversions.
* Keep functional changes independently mergeable from cleanup work.
* Expect a large modernization series to evolve through multiple independently reviewable stages.

---

## Related Series

* [Series 000 – Exploratory cleanup.h](series-000-exploratory-cleanup-h.md)
* [Series 001 – ST Sensors buffer reuse](series-001-st-sensors-buffer-reuse.md)
* [Series 002 – SSP Sensors modernization](series-002-ssp-sensors-modernization.md)
* [Series 003 – GC0310 clock modernization](series-003-gc0310-clock-modernization.md)
* [Series 004 – AD7173 checkpatch analysis](series-004-ad7173-checkpatch-analysis.md)

---

## Related Learning

* [Review Process](../learning/review-process.md)

---

## References

### Lore

* [Initial patch](https://lore.kernel.org/all/20260414192045.3598010-1-sanjayembedded@gmail.com/)
* [v2](https://lore.kernel.org/all/20260422165643.2148195-1-sanjayembedded@gmail.com/)
* [v3](https://lore.kernel.org/all/20260505174640.3998281-1-sanjayembedded@gmail.com/)
* [v4](https://lore.kernel.org/all/20260602-15-apr-pm-iio-mma8452-v4-temp-v4-0-26d6dff8fc55@gmail.com/)
* [v5](https://lore.kernel.org/all/20260808-15-apr-pm-iio-mma8452-v4-temp-v5-0-d177e93ce3f8@gmail.com/)

### Mainline commits

* https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=5bdff291d20c31b365d9ddfe9c426fbfb41da5bb
* https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=0a6726ec20cd4c0101f2de0ca485a11676224dea
* https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b4f6b124467f5d770e170d93e6e12a2fe3977927
* https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=e9f143941584ae27e9981649a3f9916c322ee01d
* https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=32a5c04d457540af67507494f30261580213df94
