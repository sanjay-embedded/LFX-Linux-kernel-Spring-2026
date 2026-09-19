# Series 000 – Exploratory cleanup.h Conversion

## Executive Summary

This exploratory series investigated converting existing driver cleanup paths to the `__free()` helper across multiple kernel subsystems. The work was intentionally exploratory: it tested the applicability of the cleanup mechanism, gathered maintainer feedback, and helped identify a more effective upstream contribution strategy for the remainder of the mentorship.

The series was not merged. Its most important outcome was the review feedback that redirected the work toward smaller, subsystem-focused and higher-value changes, which directly influenced the later IIO-focused series.

## Quick Facts

| Item | Details |
|------|---------|
| Series | Exploratory cleanup.h / `__free()` conversions |
| Scope | Multiple kernel subsystems |
| Initial Focus | Cleanup-path modernization |
| Final Status | Closed / Not merged |
| Outcome | Strategy changed based on upstream review |
| Primary Lesson | Prefer focused subsystem work over broad mechanical conversion |

## Background

The series explored the use of `__free()` as a modern cleanup mechanism for existing driver code. The initial approach was broad and intentionally crossed subsystem boundaries so that common conversion patterns and potential issues could be evaluated.

## Initial Objective

- Explore practical `__free()` conversion patterns.
- Identify potential cleanup-path simplifications.
- Understand limitations and review concerns around mechanical API conversions.
- Gather upstream feedback before selecting the longer-term contribution direction.

## Technical Evolution

The initial work applied similar cleanup conversions across different drivers and subsystems. The implementation was primarily mechanical, with the objective of preserving behavior while modernizing cleanup paths.

The resulting review demonstrated that technical feasibility alone was not sufficient justification for a cross-subsystem series.

## Review Evolution

Maintainer feedback highlighted several important concerns:

- Cross-subsystem series are harder to review and route.
- Purely mechanical conversions do not necessarily provide enough value to justify broad churn.
- Cleanup changes should be evaluated in the context of subsystem design and existing APIs.
- A better contribution path was to identify focused opportunities inside a specific subsystem and build changes around clear engineering value.

This feedback became the turning point for the mentorship and led to the subsequent IIO-focused work.

## Interesting Engineering Discussions

### Mechanical conversion versus engineering value

A technically valid API conversion is not automatically a strong upstream contribution. The change should have a clear reason to exist beyond simply replacing one coding pattern with another.

### Subsystem ownership matters

Cross-subsystem work introduces different maintainers, review expectations and development trees. Keeping a series within a subsystem makes review, testing and integration more manageable.

### Review as a direction-setting mechanism

The series demonstrated that upstream review does more than identify line-level defects. Review can change the scope and strategy of future work.

## Revision Timeline

| Revision / Stage | Evolution |
|------------------|-----------|
| Initial | Exploratory cross-subsystem `__free()` conversions |
| Review | Maintainers challenged broad scope and mechanical nature |
| Outcome | Series closed and subsequent work redirected toward focused subsystem contributions |

## Final / Current Outcome

| Item | Status |
|------|--------|
| Status | Closed |
| Mainline | No |
| linux-next | No |
| Final State | Not merged |
| Contribution Impact | Established the strategy used for subsequent IIO contributions |

## Why This Series Matters

This series was the first major upstream review experience of the mentorship. Although it did not result in an upstream commit, the feedback directly influenced the structure and selection of later contributions. It established an early lesson that successful upstream work depends on scope, subsystem context, reviewability and engineering value, not only on whether the proposed code change is technically possible.

## Key Lessons Learned

- Respect subsystem boundaries when preparing upstream series.
- Avoid broad mechanical conversion work unless the engineering value is clear.
- Use reviewer feedback to improve the contribution strategy, not only the current patch.
- Small, focused series are easier to review and integrate.
- A non-merged series can still be an important and productive part of an upstream learning journey.

## Looking Back

If starting this work today, I would first select a specific subsystem, inspect its current development tree, identify a concrete modernization or correctness opportunity, and then prepare a narrowly scoped series supported by the subsystem's existing APIs and conventions.

## Related Series

- [Series 001 – ST Sensors buffer reuse](series-001-st-sensors-buffer-reuse.md)
- [Series 002 – SSP Sensors modernization](series-002-ssp-sensors-modernization.md)
- [Series 006 – ADXL accelerometer cleanup](series-006-adxl-accelerometer-cleanup.md)
- [Series 008 – HID-IIO devm modernization](series-008-hid-iio-devm-workstream.md)

## Related Learning

- [Mentorship growth](../mentorship-growth.md)
- [Mentorship milestones](../mentorship-milestones.md)
- [Upstream review process](../upstream-review-process.md)

## References

- Review history and related discussions are preserved in the mentorship repository and Linux kernel mailing-list archives.

## Metadata

| Item | Value |
|------|-------|
| Last Verified | 2026-08-23 |
| Repository Branch | enhancement |
| Documentation Role | Initial exploratory series / strategy milestone |
