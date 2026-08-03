# Series 002 – SSP Sensors: Resource Cleanup & Driver Modernization

## 1. Executive Summary

The SSP Sensors series represents one of the longest-running engineering efforts during the mentorship. Initially proposed as a simple cleanup to improve resource management, the series evolved through seven revisions into a comprehensive driver modernization effort. Continuous review from the IIO community expanded the scope beyond cleanup, introducing managed resource APIs, reusable helper abstractions, improved probe error handling, embedded RX buffer management, and overall maintainability improvements. Several changes have already been accepted, while the remaining hardware-dependent patches are awaiting validation before final integration.

## 2. Project Overview

| Item | Details |
|------|---------|
| Series | iio: ssp_sensors: improve resource cleanup (latest title) |
| Subsystem | Industrial I/O (IIO) |
| Driver | SSP Sensors |
| Duration | March 2026 – May 2026 |
| Initial Submission | v2 – 11 March 2026 |
| Latest Revision | v8 – 15 May 2026 |
| Revisions | v2 → v8 |
| Patch Count | 1 → 12 |
| Status | Partially merged |
| Current State | Waiting for hardware validation |

## 3. Background

Following feedback received on the initial cross-subsystem cleanup series (Series 000), subsequent work focused on subsystem-specific improvements. Experience gained from the ST Sensors series (Series 001) further shaped the approach taken here, resulting in a more structured, incremental, and review-friendly modernization of the SSP Sensors driver.

Why SSP Sensors were selected

- Representative of common IIO driver patterns and cleanup opportunities.
- Hardware exposes interesting buffering and probe complexity that benefit from managed resources.

Relationship to Series 000

- Series 000 provided the initial exploratory approach and reviewer feedback emphasizing subsystem scoping.

Relationship to Series 001

- Series 001's experience in reusing driver-owned buffers informed the reusable RX buffer design and validated the approach of focusing on design improvements rather than mechanical conversions.

How earlier reviewer feedback influenced this work

- Reviewers encouraged splitting changes into smaller, subsystem-focused revisions, introducing helper abstractions, and validating hardware-dependent changes before final merge.

## 4. Engineering Goals

- Improve resource lifetime management.
- Remove unnecessary allocations.
- Introduce managed resource APIs.
- Simplify cleanup paths.
- Improve probe error handling.
- Increase driver maintainability.
- Reduce duplicated code.

## 5. Technical Evolution

### Phase 1 – Cleanup Foundation (v2 → v4)

- Initial cleanup.h adoption.
- Reusable RX buffer.
- Cleanup path simplification.
- Patch organization improvements.

### Phase 2 – Driver Modernization (v5 → v6)

- devm_* conversions.
- guard() evaluation and refinement.
- devm_add_action_or_reset().
- Probe-path improvements.
- dev_err_probe().
- Embedded RX buffer.

### Phase 3 – Maintainability & Refinement (v7 → v8)

- Helper APIs.
- Refactoring.
- Cleaner ownership.
- Warning fixes.
- Simplified return paths.
- Hardware validation discussion.

## 6. Review Summary

| Reviewer | Key Contributions |
|----------|-------------------|
| Jonathan Cameron | Encouraged functional separation, questioned cleanup-only changes, requested hardware validation before merge, and guided overall series direction. |
| Andy Shevchenko | Recommended kernel coding style improvements, local struct device *, appropriate guard() usage, helper abstractions, and simplified return paths. |
| David Lechner | Reviewed commit messages, terminology, helper usage, and resource management details. |

## 7. Interesting Engineering Discussions

- Eliminating repeated RX buffer allocations through an embedded reusable buffer.
- Choosing devm_* resource management versus explicit cleanup.
- Appropriate use of guard() and cleanup.h.
- Separating functional improvements from mechanical cleanup.
- Balancing refactoring with review complexity.
- Hardware validation before merging functional changes.

## 8. Revision Timeline

| Revision | Evolution |
|----------|-----------|
| v2 → v4 | Initial cleanup.h conversion evolved into a structured multi-patch series with reusable RX buffer and simplified cleanup. |
| v5 → v6 | Expanded into driver modernization with managed resources, cleanup actions, and probe improvements. |
| v7 → v8 | Focus shifted to correctness, helper abstractions, maintainability, and hardware validation. |

## 9. Current Status

| Item | Status |
|------|--------|
| Mainline | Partially merged |
| linux-next | Partially applied |
| Current State | Waiting for hardware validation |
| Next Step | Validate on hardware, address remaining review comments, resend final revision if required |

## 10. Key Lessons Learned

- Large upstream series evolve incrementally through continuous review.
- Functional improvements are preferred over mechanical API conversions.
- Keep changes logically independent to simplify review.
- Hardware-dependent modifications should be validated before requesting final acceptance.
- Well-designed helper abstractions reduce duplication and improve maintainability.

## 11. Looking Back

If starting this series today, I would:

- Separate functional and cleanup changes earlier.
- Introduce helper abstractions before broader refactoring.
- Plan hardware validation earlier in the review cycle.
- Keep large modernization efforts modular to reduce reviewer load.

## 12. Related Journey

Journey: journey/growth.md

Previous Series: Series 000, Series 001

## 13. Related Learning

learning/review-process.md

## 14. References

- [Lore v2](https://lore.kernel.org/all/20260311174151.3441429-1-sanjayembedded@gmail.com/)
- [Lore v3](https://lore.kernel.org/all/20260315125509.857195-1-sanjayembedded@gmail.com/)
- [Lore v4](https://lore.kernel.org/all/20260326081815.925373-1-sanjayembedded@gmail.com/)
- [Lore v5](https://lore.kernel.org/all/20260406080852.2727453-1-sanjayembedded@gmail.com/)
- [Lore v6](https://lore.kernel.org/all/20260415050749.3858046-1-sanjayembedded@gmail.com/)
- [Lore v7](https://lore.kernel.org/all/20260426091710.3722035-1-sanjayembedded@gmail.com/)
- [Lore v8](https://lore.kernel.org/all/20260515174017.3962168-1-sanjayembedded@gmail.com/)
- [Mainline commit dcc80f2](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=dcc80f2fdff721ced4ea1ef7a3ea43f3fbe0b27a)
- [Mainline commit a9ecd9a](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=a9ecd9a121752f2d7bb69da264bda65b6b6e6c6e)
- [Mainline commit eedf7602](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=eedf7602fbd929e97e0c480da501dc7a34beb2a8)
- [Mainline commit 74c39233](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=74c3923344c6ad4b7199948d54dc947504c39483)

(Add merged commits once available.)

(Patchwork links if applicable.)
