# Series 004 – AD7173: Checkpatch & Coding Style Analysis

## Executive Summary

This series investigated coding-style and spelling issues reported by `checkpatch.pl` in the AD7173 ADC driver. During review, maintainers identified that one reported CamelCase warning was caused by a limitation of `checkpatch.pl` in recognizing standard SI unit abbreviations rather than a defect in the driver.

The series was therefore closed without further revisions. The key outcome was learning to validate automated-tool findings against kernel conventions and engineering intent before changing technically correct code.

## Quick Facts

| Item | Details |
|------|---------|
| Series | `iio: adc: ad7173: cleanup codestyle check and spell correct` |
| Subsystem | Industrial I/O (IIO / ADC) |
| Driver | AD7173 |
| Initial Submission | 13 April 2026 |
| Final Revision | v1 |
| Patch Count | 3 |
| Status | Closed |
| Mainline | No |
| linux-next | No |

## Background

The series started as a cleanup effort based on warnings and spelling issues reported by `checkpatch.pl`. The intention was to improve consistency with kernel coding conventions and reduce avoidable static-analysis noise.

## Initial Objective

- Investigate `checkpatch.pl` warnings in the driver.
- Correct genuine coding-style and spelling issues.
- Determine whether reported warnings represented actual kernel-code problems.
- Keep the resulting series focused on changes with engineering value.

## Technical Evolution

The initial three-patch series addressed coding-style and spelling findings. One warning concerned identifiers using standard SI notation such as `uV` and `C`.

The review demonstrated that this particular warning did not represent an actual violation in the driver. Changing the identifier solely to satisfy the tool would have made the source less correct rather than more correct.

## Review Evolution

The key review question became whether the reported warning was a genuine source-code problem or a limitation of the checking tool.

The conclusion was that the identifier was technically valid and that improving `checkpatch.pl` would be a better long-term solution than changing correct driver code.

## Interesting Engineering Discussions

- Static-analysis tools are valuable aids, but their warnings require engineering judgment.
- Kernel coding conventions and domain-specific terminology take precedence over mechanical tool output.
- Tooling defects can be more appropriate targets for improvement than technically correct source code.
- Upstream review can prevent unnecessary churn by challenging the premise of a proposed cleanup.

## Revision Timeline

| Revision | Evolution |
|----------|-----------|
| v1 | Initial three-patch cleanup submitted and reviewed. The CamelCase warning was determined to be a `checkpatch.pl` limitation, so no further revision was pursued. |

## Final / Current Outcome

| Item | Status |
|------|--------|
| Final Revision | v1 |
| Patch Count | 3 |
| Mainline | Not merged |
| linux-next | Not applied |
| Final State | Closed after review |
| Reason | Reported issue included a tooling limitation rather than a driver defect |

## Why This Series Matters

This series is an important example of learning when **not** to change code. Upstream contribution is not about eliminating every warning mechanically; it is about understanding whether a warning reflects a real problem and whether a proposed change improves the kernel.

## Key Lessons Learned

- `checkpatch.pl` is guidance, not an authority that overrides engineering judgment.
- Validate automated findings against subsystem conventions and technical correctness.
- Do not modify standards-compliant identifiers merely to silence a warning.
- A closed series can still produce an important upstream engineering lesson.

## Looking Back

If starting this work today, I would first inspect the reported warning in the context of the subsystem and relevant kernel conventions, then determine whether a driver change, tooling improvement, or no change is the most appropriate outcome.

## Related Series

- [Series 000 – Exploratory cleanup.h](series-000-exploratory-cleanup-h.md)
- [Series 001 – ST Sensors buffer reuse](series-001-st-sensors-buffer-reuse.md)
- [Series 002 – SSP Sensors modernization](series-002-ssp-sensors-modernization.md)
- [Series 003 – GC0310 clock modernization](series-003-gc0310-clock-modernization.md)
- [Series 005 – MMA8452 modernization](series-005-mma8452-modernization.md)

## Related Learning

- [Mentorship growth](../mentorship-growth.md)
- [Mentorship milestones](../mentorship-milestones.md)
- [Upstream review process](../upstream-review-process.md)

## References

- Review and discussion history is preserved in the Linux kernel mailing-list archives.

## Metadata

| Item | Value |
|------|-------|
| Last Verified | 2026-08-23 |
| Repository Branch | enhancement |
| Documentation Role | Tooling-vs-source-code judgment milestone |
