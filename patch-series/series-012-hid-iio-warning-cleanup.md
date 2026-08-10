# Series 012 – HID-IIO Warning and Coding-Style Cleanup

## Executive Summary

This series started as an 11-patch HID-IIO cleanup covering coding-style warnings, formatting alignment, NULL-check simplification and common-device usage for devres.

During review, maintainers identified that several of the initial patches represented unnecessary formatting churn rather than independently valuable changes. The series was progressively reduced from 11 patches to 6 and finally to 2 patches.

The work also had to be synchronized with the evolving IIO development tree because related HID-IIO changes, including `usage_id` type cleanup and common device handling, were being accepted independently.

The final series therefore represents a substantially more focused contribution than the original submission.

The final work was subsequently applied through the IIO development flow and reached linux-next.

---

## Quick Facts

| Item | Details |
|------|---------|
| Series | HID: iio: warning clean up and prefer kernel coding style |
| Subsystem | Industrial I/O (IIO) / HID Sensors |
| Initial Submission | 16 June 2026 |
| Final Revision | v3 – 07 July 2026 |
| Revisions | v1 → v2 → v3 |
| Patch Count | v1: 11 → v2: 6 → v3: 2 |
| Files | HID-IIO common code and driver files |
| Maintainer | Jonathan Cameron |
| Reviewers | Jonathan Cameron, Andy Shevchenko, Maxwell Doose and others |
| Final Status | Applied in linux-next |
| Mainline | Not yet confirmed |

---

## Background

The initial objective was to clean up warning and coding-style issues across HID-IIO drivers.

The first submission combined several categories:

- missing blank lines;
- parenthesis alignment;
- NULL-check simplification;
- common `struct device` usage for devres;
- related HID-IIO cleanup.

Although all changes were intended to be functionally neutral, review showed that the patches did not all have equal value.

The series therefore evolved toward keeping only changes with clear independent engineering value.

---

## Initial Objective

The v1 series aimed to:

- clean up coding-style warnings;
- align code with kernel coding style;
- simplify obvious checks;
- use the appropriate common device for devres;
- keep the changes functionally neutral.

The series was W=1 build-tested patch-by-patch.

---

## Revision Evolution

### v1 – Broad 11-patch cleanup

**11 patches**

The initial series covered nine HID-IIO files and included:

- blank-line fixes;
- parenthesis alignment;
- `NULL` check simplification;
- common device handling;
- devres-related cleanup.

The series intentionally described these as having no functional changes.

---

### Review – Scope and patch organization challenged

Reviewers identified that several patches were primarily formatting churn.

Maxwell Doose specifically indicated that the formatting-only patches could be consolidated rather than maintained as many independent commits.

This led to an important distinction:

```text
Tiny formatting change
        ≠
independently valuable patch
````

The series was therefore reduced instead of preserving the original patch count.

---

### v2 – Reduced 6-patch series

**6 patches**

The second revision removed or consolidated several style-only changes.

The remaining changes were more focused on cleanup with clearer review value.

The series was also rebased against the evolving IIO development tree.

This was important because related HID-IIO changes had already been applied independently.

---

### v3 – Focused 2-patch series

**2 patches**

The final revision narrowed the series further to the remaining changes considered independently worthwhile.

The v3 therefore represents the final focused form of the original cleanup rather than an attempt to preserve all 11 patches from v1.

---

## Why the Series Shrunk

```text
v1
11 patches
│
├── formatting churn
├── style cleanup
├── NULL-check cleanup
└── meaningful devres/device changes
        ↓
review
        ↓
v2
6 patches
│
├── unnecessary churn removed
└── useful changes retained
        ↓
rebase + further review
        ↓
v3
2 patches
│
└── focused remaining changes
```

The reduction is itself an important part of the contribution history.

---

## Important Engineering Discussion

### 1. Patch count is not the goal

The original 11-patch series was not valuable simply because it contained many changes.

Review demonstrated that some changes were better consolidated.

The final two-patch series was therefore stronger than the original 11-patch submission.

---

### 2. Formatting churn vs. engineering value

The series contained both:

```text
Formatting / style
```

and:

```text
Resource ownership / devres
```

The latter has greater engineering significance because it changes which device owns the managed resource.

For example, using the common HID platform device as the devres owner can be more meaningful than merely changing whitespace or alignment.

---

### 3. Correct devres ownership

One important example involved changing devres ownership from the IIO device to the HID platform device.

Conceptually:

```text
Before:

devm_*(&indio_dev->dev, ...)


After:

devm_*(&pdev->dev, ...)
```

The correct choice depends on which device actually owns the resource.

This reinforced that devm conversions should not be performed mechanically.

---

### 4. Keep the series synchronized with the subsystem tree

The HID-IIO area was evolving quickly during this period.

Other work had already landed, including:

* `usage_id` type unification;
* common device handling;
* devm-related changes.

Therefore, each new revision needed to be based on the current `iio/testing` state.

This avoids:

* duplicate changes;
* stale patches;
* conflicts;
* unnecessary review of changes already accepted elsewhere.

---

## Review Summary

| Reviewer             | Main Contribution                                                                                  |
| -------------------- | -------------------------------------------------------------------------------------------------- |
| **Maxwell Doose**    | Identified formatting patches as excessive churn and recommended consolidation.                    |
| **Andy Shevchenko**  | Provided coding-style and cleanup guidance and reinforced avoiding unnecessary mechanical changes. |
| **Jonathan Cameron** | Guided the final scope, subsystem synchronization and grouping of useful changes.                  |

---

## Revision Timeline

| Revision | Patches | Major Evolution                                                      |
| -------- | ------- | -------------------------------------------------------------------- |
| **v1**   | 11      | Broad HID-IIO warning and coding-style cleanup.                      |
| **v2**   | 6       | Reduced formatting churn and synchronized with the current IIO tree. |
| **v3**   | 2       | Final focused series containing the remaining worthwhile changes.    |

---

## Final Outcome

| Item                | Status                                              |
| ------------------- | --------------------------------------------------- |
| Latest Revision     | v3                                                  |
| Initial Patch Count | 11                                                  |
| Final Patch Count   | 2                                                   |
| Mainline            | Not yet confirmed                                   |
| linux-next          | ✅ Applied                                           |
| Final State         | Focused v3 work reached linux-next                  |
| Overall Result      | Successful scope reduction and upstream integration |

---

## linux-next Commits

The supplied linux-next commits are:

* `cff496bda5128dd9cf7a38fc2933440ee58b8ad1`
* `d9290c908d6f31bcdf79c1fec9b7287cf65df19b`
* `0c50c9e3b2a4acb2b5b238ba58537f5525532527`
* `a30824bbfb22f890df7e92448522b696c62ce965`
* `636deb551c2da89e798b2057d417be86ab9a3efc`
* `2e2f2de7532cbbc2269de8be20ec709606c6e79b`

> The exact mapping between these six integration commits and the final v3 two-patch Lore submission should be preserved once the commit subjects are recorded. The repository should not imply a 6-patch v3 series simply because linux-next contains six commits.

---

## Key Lessons Learned

* **Do not optimize for patch count. Optimize for logical reviewability.**
* Not every formatting change deserves its own patch.
* Consolidate mechanical churn when it does not provide independent review value.
* Separate style cleanup from changes involving resource ownership.
* Understand the actual owner of a devres-managed resource before changing the `struct device`.
* Rebase against the current subsystem development branch before preparing a new revision.
* Remove changes that have already landed through another series.
* A series shrinking from 11 patches to 2 can represent improved engineering quality rather than lost work.

---

## Looking Back

If starting this work today, I would:

* Search the current `iio/testing` tree before preparing the initial series.
* Separate pure formatting cleanup from resource-management changes from the beginning.
* Group related formatting fixes where they do not have independent review value.
* Verify devres ownership before changing the device argument.
* Re-run repository-wide searches after each related HID-IIO series lands.
* Prefer a small, clearly justified series over preserving a large initial patch set.

---

## Related Series

* [Series 008 – HID-IIO devm API and Resource-Management Modernization](series-008-hid-iio-devm-workstream.md)
* [Series 010 – HID-IIO Callback Setup and Device Exposure Ordering](series-010-hid-iio-callback-ordering.md)
* [Series 011 – HID-IIO `usage_id` Type Unification](series-011-hid-iio-usage-id.md)

### Workstream Relationship

```text
HID-IIO modernization
        |
        +-- Series 008
        |   devm infrastructure
        |
        +-- Series 010
        |   callback/device ordering
        |
        +-- Series 011
        |   usage_id API type
        |
        +-- Series 012
            coding-style + warning cleanup
            + devres ownership
```

---

## References

### Lore

* [v1 – 11 patches](https://lore.kernel.org/all/20260616-15-jun-hid-iio-alignment-v1-0-0cd544286575@gmail.com/)
* [v2 – 6 patches](https://lore.kernel.org/all/20260702-15-jun-hid-iio-alignment-v2-0-b87f01f5efbc@gmail.com/)
* [v3 – 2 patches](https://lore.kernel.org/all/20260707-15-jul-hid-iio-alignment-v3-0-8791574ad0fe@gmail.com/)

### linux-next

* [cff496bda5128dd9cf7a38fc2933440ee58b8ad1](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=cff496bda5128dd9cf7a38fc2933440ee58b8ad1)
* [d9290c908d6f31bcdf79c1fec9b7287cf65df19b](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=d9290c908d6f31bcdf79c1fec9b7287cf65df19b)
* [0c50c9e3b2a4acb2b5b238ba58537f5525532527](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=0c50c9e3b2a4acb2b5b238ba58537f5525532527)
* [a30824bbfb22f890df7e92448522b696c62ce965](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=a30824bbfb22f890df7e92448522b696c62ce965)
* [636deb551c2da89e798b2057d417be86ab9a3efc](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=636deb551c2da89e798b2057d417be86ab9a3efc)
* [2e2f2de7532cbbc2269de8be20ec709606c6e79b](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=2e2f2de7532cbbc2269de8be20ec709606c6e79b)

````
