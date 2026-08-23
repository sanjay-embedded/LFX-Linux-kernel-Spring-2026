# Series 001 – iio: st_sensors: Drop temporary kmalloc() buffer and reuse buffer_data[]

## Executive Summary

This series refactored the ST Sensors core driver to reuse the driver's existing `buffer_data[]` field instead of allocating and freeing a temporary buffer on every read. The work originated from feedback received on the earlier exploratory cleanup series and evolved through three revisions before being accepted upstream.

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
| File Modified | `drivers/iio/common/st_sensors/st_sensors_core.c` |

## Background

The original exploratory cleanup series proposed adopting `cleanup.h` helpers across multiple subsystems. During review, maintainers encouraged focusing on subsystem-specific improvements and questioned whether removing `kmalloc()` alone was the right solution.

This series applies that feedback by addressing the underlying design: instead of allocating a temporary buffer, the driver reuses its existing `buffer_data[]` field.

## Initial Objective

Remove the per-read temporary allocation while preserving the existing driver behavior and simplifying the cleanup path.

## Technical Evolution

The implementation:

- Removed the temporary `kmalloc()` allocation.
- Reused the driver's existing `buffer_data[]` field.
- Simplified cleanup and return paths.
- Reduced temporary resource management.

## Review Evolution

Review feedback refined both the implementation and terminology. The final revision described `buffer_data[]` accurately as an existing driver-owned field and aligned declarations and cleanup with kernel conventions.

## Interesting Engineering Discussions

- Reuse an existing driver-owned resource before allocating another temporary resource.
- Precise terminology in commit messages matters when describing ownership and lifetime.
- Small, subsystem-focused changes are easier to review and maintain.

## Revision Timeline

| Revision | Evolution |
|----------|-----------|
| v2 | Split from the earlier cross-subsystem cleanup series and changed the design to reuse `buffer_data[]`. |
| v3 | Updated commit-message wording following review. |
| v4 | Refined terminology, declarations and cleanup logic; linked previous revisions. |

## Final / Current Outcome

| Item | Status |
|------|--------|
| Final Revision | v4 |
| Mainline | Merged |
| Current Status | Accepted upstream |
| Last Verified | 2026-08-23 |

## Key Lessons Learned

- Prefer reusing existing driver-owned resources before introducing new allocations.
- Review feedback can improve both implementation and commit-message accuracy.
- Small subsystem-focused changes can be a strong starting point for upstream contribution.

## Looking Back

If starting this work today, I would still keep the change narrowly scoped around the underlying design improvement rather than treating it as a mechanical cleanup.

## Related Series

- [Series 000 – Exploratory cleanup.h](series-000-exploratory-cleanup-h.md)
- [Series 002 – SSP Sensors modernization](series-002-ssp-sensors-modernization.md)

## Related Learning

- [Mentorship growth](../mentorship-growth.md)
- [Upstream review process](../upstream-review-process.md)

## References

- [Lore v2](https://lore.kernel.org/all/20260311182050.3467471-1-sanjayembedded@gmail.com/)
- [Lore v3](https://lore.kernel.org/all/20260312063424.3846945-1-sanjayembedded@gmail.com/)
- [Lore v4](https://lore.kernel.org/all/20260315121625.840769-1-sanjayembedded@gmail.com/)
- [Mainline commit](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=1ac30f58f0336287203109872f71a81d4bb271db)
