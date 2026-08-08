# Series 007 – ADI IIO MAINTAINERS Coverage and Ownership

## Executive Summary

This work began as a simple correction to outdated maintainer information for ADI IIO drivers. Through six revisions, the series evolved into a broader examination of how ADI IIO drivers should be represented and maintained in the kernel's `MAINTAINERS` file.

Reviewer feedback shifted the approach from replacing an individual maintainer address to establishing sustainable coverage through an ADI mailing-list entry, consolidating redundant driver entries, and identifying appropriate specific maintainers where active ownership existed.

The series expanded to five patches in v4 before being reduced to two patches in v5 and v6 as the maintenance model became clearer.

The final v6 series consisted of two patches covering the ADI IIO umbrella entry and specific IIO maintainer assignments. Both patches were subsequently accepted into mainline Linux.

---

## Quick Facts

| Item | Details |
|------|---------|
| Series | MAINTAINERS: update ADI IIO entry and specific IIO maintainer |
| Subsystem | Industrial I/O (IIO) |
| Area | Maintainer and ownership metadata |
| Initial Submission | 18 April 2026 |
| Final Revision | v6 – 11 May 2026 |
| Revisions | v1 → v6 |
| Patch Count | 1 → 1 → 1 → 5 → 2 → 2 |
| Files Modified | `MAINTAINERS` |
| Status | Merged |
| Primary Maintainer | Jonathan Cameron |
| ADI Review/Input | Nuno Sá, Marcelo Schmitt |
| Other Review | Andy Shevchenko and others |

---

## Background

The work started after identifying outdated or invalid maintainer information associated with ADI IIO drivers.

The initial problem appeared straightforward: update the maintainer information.

During review, however, the discussion expanded into a broader question:

> What is the appropriate and sustainable maintenance coverage for these drivers?

This led to consideration of:

- individual maintainers;
- reviewer ownership;
- ADI mailing-list coverage;
- wildcard `MAINTAINERS` entries;
- redundant per-driver entries;
- specific active maintainers.

---

## Initial Objective

The original objective was to correct outdated maintainer information for affected ADI IIO drivers.

The initial submission was intentionally small, consisting of a single patch.

---

## Revision Evolution

### v1 – Correct stale maintainer information

**1 patch**

The initial proposal focused on replacing an outdated Analog Devices maintainer address associated with the affected IIO drivers.

---

### v2 – Individual maintainer proposal

**1 patch**

The series proposed adding Nuno Sá as a maintainer based on the discussion around future ownership.

Review indicated that the maintenance model should instead consider broader and more persistent coverage.

---

### v3 – Mailing-list based coverage

**1 patch**

The approach changed from assigning an individual maintainer to using the Analog Devices mailing list for persistent coverage.

Nuno also suggested using the opportunity to update another ADI IIO entry.

---

### v4 – ADI-wide consolidation

**5 patches**

The scope expanded substantially.

The series proposed consolidating ADI IIO coverage using the existing umbrella:

`ANALOG DEVICES INC IIO DRIVERS`

This allowed redundant per-driver `MAINTAINERS` entries to be removed where the wildcard entry already provided coverage.

The expansion involved approximately 40 redundant entries.

The work was split into multiple patches to keep the consolidation reviewable.

---

### v5 – Narrowing the scope

**2 patches**

The series was reduced after review of which drivers were genuinely unmaintained.

The approach became more selective rather than removing entries solely because they were covered by the umbrella entry.

---

### v6 – Specific maintainer ownership

**2 patches**

The final revision refined the maintenance model further.

Rather than simply removing entries where a maintainer was no longer active, affected drivers were assigned to an appropriate active maintainer where possible.

The final series consisted of:

1. Updating the ADI IIO umbrella entry.
2. Updating specific IIO maintainer assignments.

---

## Evolution at a Glance

```text
v1
Stale maintainer address
        ↓
v2
Individual maintainer proposal
        ↓
v3
Persistent mailing-list coverage
        ↓
v4
ADI-wide MAINTAINERS consolidation
~40 redundant entries
        ↓
v5
Narrow scope based on actual ownership
        ↓
v6
Specific active maintainers
+ persistent ADI mailing-list coverage
```

---

## Review Evolution

### Jonathan Cameron

Jonathan was central to reshaping the series.

Key guidance included:

* prefer durable mailing-list coverage where appropriate;
* distinguish individual maintainers from broader project coverage;
* consolidate redundant entries when an umbrella wildcard already covers the drivers;
* retain specific entries where an active maintainer or reviewer exists.

Jonathan also highlighted the importance of reviewing patch metadata when a patch changes substantially across revisions rather than blindly carrying old review tags forward.

---

### Nuno Sá

Nuno provided ADI-specific ownership information and suggested updating additional ADI IIO coverage.

His input helped determine the appropriate ownership model for the ADI IIO entries.

---

### Andy Shevchenko

Andy participated in the consolidation discussion, particularly around the scope and correctness of removing per-driver entries when broader wildcard coverage already existed.

---

### Marcelo Schmitt

Marcelo's input helped distinguish genuinely unmaintained drivers from drivers that still had active maintainership.

This contributed to the change in direction between v5 and v6: where possible, an appropriate active maintainer was assigned instead of simply removing the entry.

---

## Interesting Engineering Discussions

### 1. `MAINTAINERS` represents coverage, not just names

The original problem was an invalid maintainer address.

The review evolved the question into:

> Who provides sustainable coverage for this driver?

This introduced several possible maintenance mechanisms:

```text
Specific maintainer
        ↓
Specific reviewer
        ↓
Project/company mailing list
        ↓
Subsystem / umbrella wildcard
```

The correct choice depends on actual ownership and review activity.

---

### 2. Wildcard coverage can eliminate duplication

The existing ADI IIO umbrella entry could cover drivers through a wildcard path.

This made a large number of individual entries redundant.

The consolidation work therefore focused on removing duplication while preserving meaningful ownership information.

---

### 3. Don't remove specific ownership blindly

The later revisions demonstrated that wildcard coverage is not always enough.

If a specific driver has an active maintainer, retaining or assigning that maintainer provides more useful information than relying only on broad coverage.

The final approach therefore became:

```text
Specific active maintainer exists
        ↓
Keep specific ownership

No specific active maintainer
        ↓
Use appropriate broader coverage
```

---

### 4. Scope can expand and contract during review

This series went:

```text
1 patch
  ↓
1 patch
  ↓
1 patch
  ↓
5 patches
  ↓
2 patches
  ↓
2 patches
```

The expansion was driven by discovering related maintenance problems.

The reduction happened after reviewing actual ownership and eliminating changes that were unnecessary or insufficiently justified.

---

## Review Summary

| Reviewer / Contributor | Main Contribution                                                                                    |
| ---------------------- | ---------------------------------------------------------------------------------------------------- |
| **Jonathan Cameron**   | Guided the maintenance model, mailing-list coverage, consolidation strategy, and specific ownership. |
| **Nuno Sá**            | Provided ADI ownership information and suggested additional ADI IIO coverage updates.                |
| **Andy Shevchenko**    | Reviewed the consolidation approach and scope of redundant `MAINTAINERS` entries.                    |
| **Marcelo Schmitt**    | Helped identify active maintainers and distinguish genuine lack of ownership from broader coverage.  |

---

## Revision Timeline

| Revision | Date        | Patches | Major Evolution                                              |
| -------- | ----------- | ------- | ------------------------------------------------------------ |
| **v1**   | 18 Apr 2026 | 1       | Correct outdated maintainer information.                     |
| **v2**   | 19 Apr 2026 | 1       | Proposed individual maintainer ownership.                    |
| **v3**   | 21 Apr 2026 | 1       | Shifted toward persistent mailing-list coverage.             |
| **v4**   | 30 Apr 2026 | 5       | Expanded into ADI-wide `MAINTAINERS` consolidation.          |
| **v5**   | 07 May 2026 | 2       | Reduced scope based on actual maintenance status.            |
| **v6**   | 11 May 2026 | 2       | Finalized umbrella coverage and specific active maintainers. |

---

## Final Outcome

## Final Outcome

| Item | Status |
|------|--------|
| Final Revision | v6 |
| Final Patch Count | 2 |
| Files Modified | `MAINTAINERS` |
| Mainline | ✅ Merged |
| linux-next | Applied before mainline integration |
| Final State | Both v6 patches accepted upstream |

### Mainline Commits

- [d350cb2b23aee0f9a5107e87dc80929f93a04b00](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=d350cb2b23aee0f9a5107e87dc80929f93a04b00)
- [bdc573d5c33b90a21c3799c1b3f08dc8092188af](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=bdc573d5c33b90a21c3799c1b3f08dc8092188af)

---

## Key Lessons Learned

* `MAINTAINERS` is about sustainable ownership and review coverage, not simply replacing outdated email addresses.
* Verify the actual maintenance situation before changing ownership information.
* Prefer durable project or subsystem mailing-list coverage when individual corporate addresses are not reliable.
* Check existing wildcard entries before adding or retaining redundant per-driver entries.
* Preserve specific maintainer information when an active maintainer exists.
* Large metadata cleanups should be split into logically reviewable patches.
* A series can legitimately expand during investigation and later become smaller as the actual scope becomes clearer.
* Review metadata such as `Acked-by` should reflect the current patch content and should not be carried forward blindly when the patch changes substantially.

---

## Looking Back

If starting this work today, I would:

* Investigate existing umbrella `MAINTAINERS` entries before preparing the first patch.
* Identify the actual current maintainers and reviewers before proposing ownership changes.
* Separate stale-contact correction from broader consolidation earlier.
* Check whether a mailing-list entry can provide sustainable coverage before assigning individual maintainer ship.
* Build the consolidation around verified ownership rather than discovering ownership only during review.

---

## Related Series

* [Series 000 – Exploratory cleanup.h](series-000-exploratory-cleanup-h.md)
* [Series 001 – ST Sensors buffer reuse](series-001-st-sensors-buffer-reuse.md)
* [Series 002 – SSP Sensors modernization](series-002-ssp-sensors-modernization.md)
* [Series 003 – GC0310 clock modernization](series-003-gc0310-clock-modernization.md)
* [Series 004 – AD7173 checkpatch analysis](series-004-ad7173-checkpatch-analysis.md)
* [Series 005 – MMA8452 modernization](series-005-mma8452-modernization.md)
* [Series 006 – ADXL accelerometer cleanup](series-006-adxl-accelerometer-cleanup.md)

---

## Related Learning

* [Review Process](../learning/review-process.md)

---

## References

### Lore

* [v1](https://lore.kernel.org/all/20260418211336.1800221-1-sanjayembedded@gmail.com/)
* [v2](https://lore.kernel.org/all/20260419173830.2802263-1-sanjayembedded@gmail.com/)
* [v3](https://lore.kernel.org/all/20260421165856.2245598-1-sanjayembedded@gmail.com/)
* [v4](https://lore.kernel.org/all/20260430190642.3434650-1-sanjayembedded@gmail.com/)
* [v5](https://lore.kernel.org/all/20260507175132.3063161-1-sanjayembedded@gmail.com/)
* [v6](https://lore.kernel.org/all/20260511171643.3173872-1-sanjayembedded@gmail.com/)
