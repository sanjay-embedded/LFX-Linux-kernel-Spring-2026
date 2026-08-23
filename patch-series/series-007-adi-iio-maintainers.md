# Series 007 – ADI IIO MAINTAINERS Coverage and Ownership

## Executive Summary

This work began as a simple correction to outdated maintainer information for ADI IIO drivers. Through six revisions, the series evolved into a broader examination of sustainable ownership and review coverage in the kernel's `MAINTAINERS` file.

The work expanded from an individual contact correction to mailing-list coverage, wildcard consolidation and specific active maintainer assignments. The final v6 series contained two focused patches and both were accepted into mainline Linux.

## Quick Facts

| Item | Details |
|------|---------|
| Series | `MAINTAINERS: update ADI IIO entry and specific IIO maintainer` |
| Subsystem | Industrial I/O (IIO) |
| Area | Maintainer and ownership metadata |
| Initial Submission | 18 April 2026 |
| Final Revision | v6 – 11 May 2026 |
| Revisions | v1 → v6 |
| Patch Count | 1 → 1 → 1 → 5 → 2 → 2 |
| Files Modified | `MAINTAINERS` |
| Status | Merged |
| Mainline | Yes |
| Primary Maintainer | Jonathan Cameron |

## Background

The initial issue was outdated or invalid maintainer information associated with ADI IIO drivers. Review expanded the problem into a broader question: what maintenance coverage is actually sustainable for these drivers?

## Initial Objective

- Correct stale maintainer information.
- Determine appropriate current ownership.
- Improve durable review coverage.
- Remove redundant maintenance metadata where broader coverage already exists.

## Technical Evolution

### v1 – Contact Correction

The initial patch addressed outdated maintainer information.

### v2 – Individual Ownership

The approach considered assigning an individual maintainer based on current ownership discussions.

### v3 – Mailing-list Coverage

The maintenance model shifted toward persistent ADI mailing-list coverage.

### v4 – Consolidation

The work expanded to an ADI-wide `MAINTAINERS` consolidation, including removal of redundant entries where an umbrella wildcard already provided coverage.

### v5/v6 – Selective Ownership

Review narrowed the scope and retained specific maintainers where active ownership existed while using broader coverage where appropriate.

## Review Evolution

The key change was moving from “replace a stale email address” to “represent sustainable ownership and review coverage.” Reviewers distinguished between broad project coverage, specific active maintainers and redundant metadata.

## Interesting Engineering Discussions

- `MAINTAINERS` represents sustainable ownership and review coverage, not just contact information.
- Wildcard entries can remove redundant per-driver metadata.
- Specific active maintainers should be retained where they provide meaningful ownership.
- Maintenance status should be verified before changing ownership fields.
- Large metadata changes should be split into logically reviewable patches.
- Review tags should reflect the current patch content rather than being carried forward blindly after substantial changes.

## Revision Timeline

| Revision | Date | Patches | Major Evolution |
|----------|------|---------|-----------------|
| v1 | 18 Apr 2026 | 1 | Corrected outdated maintainer information. |
| v2 | 19 Apr 2026 | 1 | Proposed individual maintainer ownership. |
| v3 | 21 Apr 2026 | 1 | Shifted toward persistent mailing-list coverage. |
| v4 | 30 Apr 2026 | 5 | Expanded into ADI-wide consolidation. |
| v5 | 07 May 2026 | 2 | Reduced scope based on actual maintenance status. |
| v6 | 11 May 2026 | 2 | Finalized umbrella coverage and specific active maintainers. |

## Final / Current Outcome

| Item | Status |
|------|--------|
| Final Revision | v6 |
| Final Patch Count | 2 |
| Mainline | Merged |
| linux-next | Applied before mainline integration |
| Final State | Both v6 patches accepted upstream |

## Why This Series Matters

This contribution expanded the mentorship beyond driver implementation into subsystem ownership and maintenance infrastructure. It demonstrated that upstream engineering also includes ensuring the right people, lists and review paths are represented for long-term code maintenance.

## Key Lessons Learned

- `MAINTAINERS` is about sustainable ownership and review coverage.
- Verify actual maintenance status before modifying ownership information.
- Prefer durable mailing-list coverage when it represents the real project ownership.
- Check wildcard coverage before retaining redundant per-driver entries.
- Preserve specific active ownership where it adds value.
- Scope large metadata changes into reviewable units.

## Looking Back

If starting this work today, I would investigate current ownership and existing umbrella entries before sending the first revision and separate stale-contact correction from broader consolidation earlier.

## Related Series

- [Series 002 – SSP Sensors modernization](series-002-ssp-sensors-modernization.md)
- [Series 006 – ADXL accelerometer cleanup](series-006-adxl-accelerometer-cleanup.md)
- [Series 008 – HID-IIO devm modernization](series-008-hid-iio-devm-workstream.md)

## Related Learning

- [Mentorship growth](../mentorship-growth.md)
- [Mentorship milestones](../mentorship-milestones.md)
- [Upstream review process](../upstream-review-process.md)

## References

- [v1](https://lore.kernel.org/all/20260418211336.1800221-1-sanjayembedded@gmail.com/)
- [v2](https://lore.kernel.org/all/20260419173830.2802263-1-sanjayembedded@gmail.com/)
- [v3](https://lore.kernel.org/all/20260421165856.2245598-1-sanjayembedded@gmail.com/)
- [v4](https://lore.kernel.org/all/20260430190642.3434650-1-sanjayembedded@gmail.com/)
- [v5](https://lore.kernel.org/all/20260507175132.3063161-1-sanjayembedded@gmail.com/)
- [v6](https://lore.kernel.org/all/20260511171643.3173872-1-sanjayembedded@gmail.com/)
- [d350cb2b](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=d350cb2b23aee0f9a5107e87dc80929f93a04b00)
- [bdc573d5](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=bdc573d5c33b90a21c3799c1b3f08dc8092188af)

## Metadata

| Item | Value |
|------|-------|
| Last Verified | 2026-08-23 |
| Repository Branch | enhancement |
| Documentation Role | Maintainer ownership and subsystem coverage milestone |
