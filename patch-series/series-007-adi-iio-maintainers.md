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

{