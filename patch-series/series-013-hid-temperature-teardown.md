# Series 013 – HID Temperature Teardown Ordering Fix

## Executive Summary

This focused correctness fix addresses the teardown ordering of the HID temperature sensor driver. The initial v1 patch described a potential use-after-free, but maintainer review challenged the failure mechanism and prompted a closer investigation of the actual teardown path.

The investigation showed a concrete ordering problem: the IIO device could remain exposed after the sensor-hub callback had been removed, allowing a consumer operation to wait on a callback that was no longer available and leading to a timeout. The implementation remained unchanged in v2; the commit-message rationale was rewritten to accurately describe the demonstrated failure.

The v2 patch was applied through the IIO development flow and reached linux-next.

## Quick Facts

| Item | Details |
|------|---------|
| Series | HID: iio: Fix HID sensor temperature driver teardown ordering |
| Subsystem | Industrial I/O (IIO) / HID Sensors |
| Driver | HID temperature sensor |
| Initial Submission | June 2026 |
| Final Revision | v2 |
| Revisions | v1 → v2 |
| Patch Count | 1 |
| Status | Applied in linux-next |
| Mainline | Not yet confirmed |
| linux-next Commit | `967d066f5334740f656577bc51c381a1bb707b61` |
| Stable Handling | `Cc: stable@vger.kernel.org` included |
| Last Verified | 2026-08-23 |

## Background

The patch was extracted from the broader HID-IIO callback and device-exposure work. The original teardown sequence allowed callback removal to occur while the corresponding IIO device remained exposed.

The initial description suggested a use-after-free, but review required the concrete failure path to be established instead of inferred from lifetime concerns alone.

## Initial Objective

Ensure the IIO device is no longer externally usable before the underlying HID sensor callback and related resources are torn down.

## Technical Evolution

### v1 – Initial teardown fix

The initial patch reordered the teardown path but described the issue as a possible UAF.

### Review – Failure mechanism challenged

Maintainer feedback led to investigation of the actual remove path and the interaction between IIO consumers and the HID sensor hub callback.

### v2 – Corrected problem statement

The implementation remained unchanged. The commit message was rewritten to describe the demonstrated timeout/exposure problem rather than claiming an unsupported UAF.

## Review Evolution

The important distinction became:

```text
Potential lifetime concern
        ≠
Proven UAF
```

The final rationale focused on the concrete ordering and teardown behavior observed during analysis.

## Interesting Engineering Discussions

### Teardown ordering is part of device lifetime correctness

Removing a callback before removing external device exposure can leave consumers observing an incompletely torn-down device.

The safe conceptual sequence is:

```text
remove device exposure
        ↓
remove callback/resource
```

rather than:

```text
remove callback/resource
        ↓
remove device exposure
```

### Relationship to Series 010

This fix is a concrete, driver-specific follow-up to the broader callback/device-exposure ordering investigation documented in Series 010.

## Revision Timeline

| Revision | Evolution |
|----------|-----------|
| **v1** | Submitted the teardown ordering fix with an initial UAF-based rationale. |
| **v2** | Preserved the implementation, corrected the failure description and applied the patch through the IIO development flow. |

## Final / Current Outcome

| Item | Status |
|------|--------|
| Final Revision | v2 |
| Patch Count | 1 |
| Mainline | Not yet confirmed |
| linux-next | Applied |
| linux-next Commit | `967d066f5334740f656577bc51c381a1bb707b61` |
| Stable Handling | `Cc: stable@vger.kernel.org` included |
| Last Verified | 2026-08-23 |

## Why This Series Matters

This contribution demonstrates the value of validating the exact failure mechanism. The final patch was technically stronger not because the implementation changed substantially, but because the problem statement was corrected to match the evidence from the actual teardown path.

## Key Lessons Learned

- Establish the concrete failure mechanism before claiming a memory-safety bug.
- Device exposure and resource teardown must be considered together.
- Teardown ordering can affect observable driver behavior even when memory lifetime remains valid.
- Commit-message accuracy is part of upstream correctness.
- A focused follow-up patch can extract a concrete correctness fix from a broader modernization workstream.

## Looking Back

If starting this work today, I would:

- Trace the complete remove path before describing the failure mode.
- Identify the exact consumer-visible state at each teardown step.
- Separate a demonstrated timeout/exposure problem from an unproven UAF claim.
- Keep the fix focused on the specific ordering requirement.

## Related Series

- [Series 008 – HID-IIO devm API and Resource-Management Modernization](series-008-hid-iio-devm-workstream.md)
- [Series 010 – HID-IIO Callback Setup and Device Exposure Ordering](series-010-hid-iio-callback-ordering.md)
- [Series 012 – HID-IIO Warning and Coding-Style Cleanup](series-012-hid-iio-warning-cleanup.md)

## Related Learning

- [Mentorship growth](../mentorship-growth.md)
- [Upstream review process](../upstream-review-process.md)

## References

### Lore

- v1 – HID temperature teardown ordering
- v2 – HID temperature teardown ordering

### linux-next

- [967d066f5334740f656577bc51c381a1bb707b61](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=967d066f5334740f656577bc51c381a1bb707b61)
