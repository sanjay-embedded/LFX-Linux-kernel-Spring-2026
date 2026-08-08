# Series 006 – ADXL Accelerometer Cleanup and Error-Handling Improvements

## Executive Summary

This work began as a focused three-patch cleanup series for the ADXL313 accelerometer driver. The initial series proposed modernizing mutex initialization, mutex cleanup using `guard()`, and probe error handling using `dev_err_probe()`.

During review, the `guard()` conversion was found to already be present in the IIO development tree. The series was therefore rebased on `iio/testing` and the redundant patch was dropped.

The remaining cleanup was then extended to closely related ADXL accelerometer drivers. The final v2 series covered five drivers and eight patches, focusing on `devm_mutex_init()` and `dev_err_probe()` conversions.

The complete v2 series was accepted and subsequently reached mainline.

---

## Quick Facts

| Item | Details |
|------|---------|
| Series | iio: accel: small cleanups and error-handling improvements |
| Initial Scope | ADXL313 |
| Final Scope | ADXL313, ADXL380, ADXL355, ADXL367, ADXL372 |
| Subsystem | Industrial I/O (IIO) |
| Initial Submission | 16 April 2026 |
| Final Revision | v2 – 17 April 2026 |
| Revisions | v1 → v2 |
| Initial Patch Count | 3 |
| Final Patch Count | 8 |
| Status | Merged |
| Files Modified | 9 |
| Maintainer | Jonathan Cameron |

> **Note:** The v2 cover-letter subject was `[PATCH 0/2]`, while the actual submission contained 8 patches. The series was nevertheless reviewed and applied as an 8-patch series.

---

## Background

The initial work focused on the ADXL313 driver and proposed three small modernization changes:

- use `devm_mutex_init()` for mutex lifetime management;
- use `guard()` for mutex handling;
- use `dev_err_probe()` for probe error handling.

During review, it became clear that the development base needed to be synchronized with the current IIO subsystem tree. The proposed `guard()` conversion was already available in `iio/testing`.

Rather than resubmitting an already existing change, the series was rebased on the subsystem development branch and the redundant patch was removed.

The remaining changes were then extended to related ADXL accelerometer drivers where the same modernization opportunities existed.

---

## Initial Proposal

### v1 – 3 patches

The initial ADXL313-specific series contained:

1. `devm_mutex_init()` conversion.
2. `guard()` conversion for mutex handling.
3. `dev_err_probe()` conversion.

The goal was to reduce manual resource handling and simplify probe error paths using established kernel APIs.

---

## Review-Driven Evolution

### Subsystem tree synchronization

Review identified that the `guard()` conversion was already present in `iio/testing`.

The change was therefore dropped from the follow-up series and development was rebased onto the current IIO testing branch.

This avoided duplicating work that had already entered the subsystem development tree.

---

### Expansion to related drivers

After removing the redundant patch, the remaining modernization pattern was applied to closely related ADXL accelerometer drivers:

- ADXL313
- ADXL355
- ADXL367
- ADXL372
- ADXL380

The resulting v2 series contained eight focused cleanup and error-handling patches.

---

## Technical Evolution

### v1 – ADXL313

| Change | Purpose |
|--------|---------|
| `devm_mutex_init()` | Tie mutex lifetime to the device |
| `guard()` | Simplify mutex locking/unlocking |
| `dev_err_probe()` | Simplify probe error handling and deferred-probe reporting |

### v2 – ADXL3xx drivers

The `guard()` patch was removed because the corresponding change was already present upstream in the IIO development tree.

The remaining changes were expanded across five related accelerometer drivers:

- `devm_mutex_init()`
- `dev_err_probe()`
- consistent probe error handling
- local `struct device *` usage where appropriate

---

## Review Summary

### Andy Shevchenko

The most important feedback was related to development against the correct subsystem state.

The `guard()` change was already present in `iio/testing`, so the follow-up work should be based on the current IIO development tree rather than an older base.

Andy also suggested improvements to the resulting `dev_err_probe()` conversions and device-pointer handling.

---

### Jonathan Cameron

Jonathan accepted the final v2 series after the requested changes were incorporated.

He also provided useful guidance about the scope and value of this type of cleanup.

`devm_mutex_init()` and `dev_err_probe()` provide useful modernization and cleanup, but they are relatively small improvements. Such changes are reasonable as early upstream contributions, but should not turn into a broad mechanical cleanup across the entire IIO subsystem.

---

## Interesting Engineering Discussions

### 1. Subsystem development trees matter

The initial series contained a change that had already landed in `iio/testing`.

This demonstrated that development should be based on the current subsystem integration branch when preparing follow-up work.

### 2. Modernization is not automatically high-impact

`devm_mutex_init()` and `dev_err_probe()` improve consistency and reduce boilerplate, but their practical impact is relatively small compared with functional or correctness changes.

### 3. Related drivers can share a focused modernization

The final series expanded beyond ADXL313 because the same cleanup pattern applied naturally to closely related ADXL accelerometer drivers.

This remained a coherent subsystem-level series rather than an unrelated mass cleanup.

### 4. Remove obsolete work instead of carrying it forward

The `guard()` conversion was not retained merely because it was part of the original proposal. Once it was found to already exist in the subsystem tree, it was removed from the new series.

---

## Revision Timeline

| Revision | Patches | Major Evolution |
|----------|---------|-----------------|
| **v1** | 3 | ADXL313-specific cleanup covering `devm_mutex_init()`, `guard()`, and `dev_err_probe()`. |
| **v2** | 8 | Rebased on `iio/testing`, dropped the already-existing `guard()` change, and expanded the remaining cleanup/error-handling work to related ADXL accelerometer drivers. |

---

## Final Outcome

| Item | Status |
|------|--------|
| Series | ✅ Accepted |
| Mainline | ✅ Merged |
| Patches | 8 |
| Drivers | 5 |
| Final Revision | v2 |
| Remaining Work | None from this series |

### Mainline Commits

- `d2ed8a2f630abe69d87eeffb2781df9237d7c1dd`
- `c27837e49fd1fa0eae1b6d3988d2ae5a9d924739`
- `1ed49c5e6b6da868ff226706d54919e1e10cf991`
- `07fd62916c7d2adb65926b989d337c7bfc7b2357`
- `70cc2c65c23ba212c6de61a727131ebf94a66610`
- `f710a0fa462ce5fc356ab4a77787b49fc1f47f7b`
- `24ab1d9a2fc4c1e4f2546bebcee2b420295120a0`
- `d47d6bdc81cfe56a1e7af40528ac81162a547e1b`

---

## Key Lessons Learned

- Always check the current subsystem development tree before preparing a new revision.
- Do not carry changes forward when they have already landed through another development path.
- A focused cleanup can be extended to closely related drivers when the engineering rationale is consistent.
- Distinguish useful modernization from broad mechanical cleanup.
- `dev_err_probe()` can simplify probe error handling and deferred-probe reporting.
- `devm_mutex_init()` provides managed lifetime and consistency, but its practical benefit should be evaluated rather than assumed.
- Reviewer feedback can change both the contents and scope of a series.

---

## Looking Back

If starting this work today, I would:

- Check `iio/testing` before preparing the initial series.
- Identify existing or recently accepted cleanup work before proposing overlapping changes.
- Group related-driver changes only after confirming that the same rationale applies consistently.
- Prefer focused, high-value changes over broad mechanical modernization.

---

## Related Series

- [Series 000 – Exploratory cleanup.h](series-000-exploratory-cleanup-h.md)
- [Series 001 – ST Sensors buffer reuse](series-001-st-sensors-buffer-reuse.md)
- [Series 002 – SSP Sensors modernization](series-002-ssp-sensors-modernization.md)
- [Series 003 – GC0310 clock modernization](series-003-gc0310-clock-modernization.md)
- [Series 004 – AD7173 checkpatch analysis](series-004-ad7173-checkpatch-analysis.md)
- [Series 005 – MMA8452 modernization](series-005-mma8452-modernization.md)

---

## Related Learning

- [Review Process](../learning/review-process.md)

---

## References

### Lore

- [v1 – ADXL313 cleanup series](https://lore.kernel.org/all/20260416051631.551250-1-sanjayembedded@gmail.com/)
- [v2 – ADXL accelerometer cleanup series](https://lore.kernel.org/all/20260417124924.353189-1-sanjayembedded@gmail.com/)

### Mainline

See the eight commit IDs listed above.
