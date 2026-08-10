# Series 009 – IIO TODO Documentation and Resource-Management Guidance

## Executive Summary

This documentation contribution updated the IIO TODO list to correct a typo and refine the resource-management items to accurately describe remaining modernization opportunities.

The work was submitted as a single patch and refined through one review revision. The final v2 was applied to linux-next.

Although documentation-only, the change required understanding the current IIO resource-management model so that the TODO list would distinguish genuine remaining work from modernization opportunities already addressed by newer APIs and helpers.

---

## Quick Facts

| Item | Details |
|------|---------|
| Series | iio: todo: fix typo and refine resource management items |
| Subsystem | Industrial I/O (IIO) |
| Contribution Type | Documentation / subsystem maintenance |
| Initial Submission | 01 June 2026 |
| Final Revision | v2 – 13 June 2026 |
| Revisions | v1 → v2 |
| Patch Count | 1 |
| File Modified | `Documentation/driver-api/iio/todo.rst` |
| Maintainer | Jonathan Cameron / IIO maintainers |
| Status | Applied in linux-next |
| Mainline | Not yet confirmed |

---

## Background

The IIO TODO documentation contained a typo and resource-management items that required more precise wording.

The purpose of the update was not to introduce new driver functionality, but to keep the contributor roadmap aligned with the current state of IIO resource-management APIs and cleanup practices.

---

## Objective

The contribution addressed:

- correction of an existing documentation typo;
- refinement of IIO resource-management TODO items;
- clearer description of remaining modernization opportunities;
- alignment of the TODO list with current IIO resource-management practices.

---

## Revision Evolution

| Revision | Major Evolution |
|----------|-----------------|
| **v1** | Corrected the documentation typo and refined the resource-management TODO entries. |
| **v2** | Incorporated review feedback and further refined the wording and accuracy of the TODO items. |

---

## Review Summary

The review focused primarily on documentation accuracy and wording rather than driver behavior.

The important engineering consideration was ensuring that the TODO list distinguishes between:

- genuinely outstanding resource-management work;
- functionality already covered by newer IIO APIs;
- modernization opportunities that should not be described as functional defects.

---

## Interesting Engineering Discussion

An IIO TODO list is more than a list of old code that should eventually be changed.

It serves as guidance for future contributors and therefore needs to describe the current preferred resource-management model accurately.

This contribution connected the documentation with broader IIO modernization work involving:

- `devm_*` APIs;
- `cleanup.h`;
- `guard()`;
- IIO-specific cleanup helpers.

As these APIs and practices evolve, the TODO documentation needs to evolve with them.

---

## Key Lessons Learned

- Subsystem TODO documentation must remain synchronized with current kernel APIs and practices.
- Documentation changes can require technical understanding of the subsystem.
- Modernization opportunities should not be presented as functional defects.
- Stale TODO items can mislead future contributors and should be updated when the underlying implementation model changes.
- Documentation is part of subsystem maintenance, not separate from upstream engineering.

---

## Final Status

| Item | Status |
|------|--------|
| Latest Revision | v2 |
| Mainline | Not yet confirmed |
| linux-next | ✅ Applied |
| Current State | Applied in linux-next |
| Contribution Type | Documentation / IIO maintenance guidance |

### linux-next Commit

`cae5bd202cfcac46762286591618b771c124727c`

---

## Looking Back

If starting this work today, I would:

- Check the current IIO resource-management APIs before proposing TODO changes.
- Verify each TODO item against existing subsystem infrastructure.
- Keep documentation language focused on contributor guidance rather than describing modernization as a defect.
- Review related recent IIO cleanup work to ensure the TODO list remains current.

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
- [Series 008 – HID-IIO devm workstream](series-008-hid-iio-devm-workstream.md)

---

## References

### Lore

- [v1 – IIO TODO documentation cleanup](https://lore.kernel.org/all/20260601190836.2766703-1-sanjayembedded@gmail.com/)
- [v2 – IIO TODO documentation cleanup](https://lore.kernel.org/all/20260613033132.2344644-1-sanjayembedded@gmail.com/)

### linux-next

- [cae5bd202cfcac46762286591618b771c124727c](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=cae5bd202cfcac46762286591618b771c124727c)
