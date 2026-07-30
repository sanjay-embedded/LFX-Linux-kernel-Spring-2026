# Series 001 – iio: st_sensors: Drop temporary kmalloc() buffer and reuse buffer_data[]

## Summary

This series refactored the ST Sensors core driver to reuse the driver's existing `buffer_data[]` field instead of allocating and freeing a temporary buffer on every read. The work originated from feedback received on the earlier exploratory cleanup series and evolved through three revisions before being accepted upstream.

---

## Quick Facts

| Item | Details |
|------|---------|
| Series | iio: st_sensors: drop temporary kmalloc buffer and reuse buffer_data |
| Initial Submission | 11 March 2026 |
| Final Version | v4 |
| Patches | 1 |
| Revisions | v2 → v3 → v4 |
| Status | Merged |
| Subsystem | Industrial I/O (IIO) |
| Driver | ST Sensors |
| File Modified | drivers/iio/common/st_sensors/st_sensors_core.c |

---

## Background

The original exploratory cleanup series proposed adopting `cleanup.h` helpers across multiple subsystems. During review, maintainers encouraged focusing on subsystem-specific improvements and questioned whether removing `kmalloc()` alone was the right solution.

This series applies that feedback by addressing the underlying design: instead of allocating a temporary buffer, the driver reuses its existing `buffer_data[]` field.

---

## Problem Statement

The driver allocated a temporary buffer during each read operation, copied data into it, and released it immediately afterwards.

Although functionally correct, this introduced unnecessary allocation and cleanup overhead when an existing driver-owned buffer was already available.

---

## Solution

The implementation:

- Removed the temporary `kmalloc()` allocation.
- Reused the driver's existing `buffer_data[]` field.
- Simplified cleanup and return paths.
- Reduced temporary resource management.

---

## Revision History

### v2

- Split from the earlier cross-subsystem cleanup series.
- Replaced temporary allocation with reuse of `buffer_data[]`.

### v3

- Updated commit message following reviewer feedback.
- Improved wording describing the reused buffer.

### v4

- Replaced "statically allocated" with "existing `buffer_data[]` field".
- Moved variable declarations to follow kernel coding style.
- Simplified remaining cleanup logic.
- Added links to previous revisions.

---

## Review Highlights

### Andy Shevchenko

Suggested simplifications and kernel coding style improvements.

### Jonathan Cameron

Provided functional and design guidance for the IIO subsystem.

### David Lechner

Requested more accurate terminology in the commit message and clarified ownership of `buffer_data[]`.

---

## Outcome

The patch was accepted after incorporating review feedback through four revisions.

The final implementation focused on improving the underlying design rather than performing a mechanical API replacement.

---

## Engineering Lessons

- Prefer reusing existing driver-owned resources before introducing new allocations.
- Review feedback often improves both implementation and commit message quality.
- Precise terminology matters when describing kernel internals.
- Small subsystem-focused changes are easier to review and maintain.

---

## Related Journey

See: `journey/growth.md`

---

## Related Learning

See: `learning/review-process.md`

---

## References

- [Lore v2](https://lore.kernel.org/all/20260311182050.3467471-1-sanjayembedded@gmail.com/)
- [Lore v3](https://lore.kernel.org/all/20260312063424.3846945-1-sanjayembedded@gmail.com/)
- [Lore v4](https://lore.kernel.org/all/20260315121625.840769-1-sanjayembedded@gmail.com/)
- [Mainline commit](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=1ac30f58f0336287203109872f71a81d4bb271db)
