# Patch Series Dashboard

This dashboard provides a quick overview of the upstream Linux kernel patch series documented in this repository.

| ID | Title | Subsystem | Status | Revisions | Topics |
|---|---|---|---|---|---|
| 000 | [Exploratory cleanup.h conversion](series-000-exploratory-cleanup-h.md) | Multiple | Closed | v1 | `cleanup.h`, `__free()`, review strategy |
| 001 | [ST Sensors buffer reuse](series-001-st-sensors-buffer-reuse.md) | IIO | Merged | v2 → v4 | buffer reuse, allocation, cleanup |
| 002 | [SSP Sensors resource cleanup & modernization](series-002-ssp-sensors-modernization.md) | IIO | Under Review | v2 → v8 | devm, cleanup, probe, buffering |
| 003 | [GC0310 sensor clock modernization](series-003-gc0310-clock-modernization.md) | Media / V4L2 | Applied in linux-next | Initial → v2 | devm, clock, camera sensor |
| 004 | [AD7173 checkpatch & coding-style analysis](series-004-ad7173-checkpatch-analysis.md) | IIO | Closed | v1 | checkpatch, coding style, tooling judgment |
| 005 | [MMA8452 modernization](series-005-mma8452-modernization.md) | IIO | Under Review | Initial → v5 | PM, devm, IRQ, regulators, cleanup |
| 006 | [ADXL accelerometer cleanup](series-006-adxl-accelerometer-cleanup.md) | IIO | Merged | v1 → v2 | devm mutex, `dev_err_probe()` |
| 007 | [ADI IIO MAINTAINERS coverage](series-007-adi-iio-maintainers.md) | IIO | Merged | v1 → v6 | maintainership, coverage, ownership |
| 008 | [HID-IIO devm modernization](series-008-hid-iio-devm-workstream.md) | IIO / HID | Under Review | v1 → v5 | devm, devres, cleanup, resource ownership |
| 009 | [IIO TODO documentation](series-009-iio-todo-documentation.md) | IIO | Applied in linux-next | v1 → v2 | documentation, resource management |
| 010 | [HID-IIO callback and device exposure ordering](series-010-hid-iio-callback-ordering.md) | IIO / HID | Applied in linux-next | v1 → v2 | ordering, callbacks, correctness |
| 011 | [HID-IIO `usage_id` type unification](series-011-hid-iio-usage-id.md) | IIO / HID | Applied in linux-next | v1 → v2 + follow-up | API contract, `u32`, audit |
| 012 | [HID-IIO warning and coding-style cleanup](series-012-hid-iio-warning-cleanup.md) | IIO / HID | Applied in linux-next | v1 → v3 | scope reduction, devres, cleanup |
| 013 | [HID temperature teardown ordering](series-013-hid-temperature-teardown.md) | IIO / HID | Applied in linux-next | v1 → v2 | teardown, exposure, stable |

## Status Vocabulary

The series use the following normalized status terms:

- **Merged** — accepted into the mainline Linux kernel.
- **Applied in linux-next** — accepted by the subsystem development flow and present in linux-next, with mainline status not yet confirmed here.
- **Under Review** — still being developed or reviewed upstream.
- **Closed** — intentionally concluded without upstream integration.
- **Superseded** — replaced by a later series or approach.

## Contribution Themes

The documented series cover several recurring areas:

- Driver modernization
- Resource and lifetime management
- Error-path handling
- Power-management integration
- Device exposure and teardown ordering
- Subsystem ownership and maintainership
- Documentation maintenance
- Review-driven patch-series restructuring

## Navigation

- [Mentorship Growth](../mentorship-growth.md)
- [Mentorship Milestones](../mentorship-milestones.md)
- [Upstream Review Process](../upstream-review-process.md)
- [Final Report](../submission/final-report.md)

## Verification

Series metadata and links are being normalized during the repository enhancement phase. The detailed series pages remain the authoritative source for each contribution.
