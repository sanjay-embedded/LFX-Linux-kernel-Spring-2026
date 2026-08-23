# Series 012 – HID-IIO Warning and Coding-Style Cleanup

## Executive Summary

This series started as an 11-patch HID-IIO cleanup covering coding-style warnings, formatting alignment, NULL-check simplification and common-device usage for devres.

During review, maintainers identified that several of the initial patches represented unnecessary formatting churn rather than independently valuable changes. The series was progressively reduced from 11 patches to 6 and finally to 2 patches.

The work also had to be synchronized with the evolving IIO development tree because related HID-IIO changes, including `usage_id` type cleanup and common device handling, were being accepted independently.

The final series therefore represents a substantially more focused contribution than the original submission.

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
| Status | Applied in linux-next |
| Mainline | Not yet confirmed |
| Last Verified | 2026-08-23 |

## Background

The initial objective was to clean up warning and coding-style issues across HID-IIO drivers. The first submission combined missing blank lines, parenthesis alignment, NULL-check simplification, common `struct device` usage for devres and related cleanup.

Although the changes were intended to be functionally neutral, review showed that the patches did not all have equal independent value. The series therefore evolved toward keeping only changes with clear review value.

## Initial Objective

The v1 series aimed to:

- clean up coding-style warnings;
- align code with kernel coding style;
- simplify obvious checks;
- use the appropriate common device for devres;
- keep the changes functionally neutral.

The series was W=1 build-tested patch-by-patch.

## Technical Evolution

### v1 – Broad 11-patch cleanup

The initial series covered nine HID-IIO files and included formatting, style, NULL-check and devres-related cleanup.

### Review – Scope and organization challenged

Reviewers identified that several patches were primarily formatting churn. Maxwell Doose specifically recommended consolidating formatting-only work rather than preserving many independent commits.

### v2 – Reduced 6-patch series

Unnecessary style-only changes were removed or consolidated. The remaining patches had clearer independent value and the series was rebased against the evolving IIO development tree.

### v3 – Focused 2-patch series

The final revision narrowed the series further to the remaining changes considered independently worthwhile.

## Review Evolution

The important distinction became:

```text
Formatting churn
        ≠
independently valuable engineering change
```

The review also reinforced that resource-ownership changes deserve separate treatment from purely stylistic cleanup.

## Interesting Engineering Discussions

### 1. Patch count is not the goal

A larger patch count does not imply a stronger contribution. The final two-patch series was more focused and reviewable than the initial 11-patch submission.

### 2. Formatting churn vs. engineering value

The series contained both style cleanup and changes involving resource ownership. The latter requires more technical reasoning because it affects lifecycle semantics.

### 3. Correct devres ownership

One important example changed devres ownership from the IIO device to the HID platform device. The correct `struct device` must be selected based on actual resource ownership rather than applying a mechanical conversion.

### 4. Keep synchronized with the subsystem tree

The HID-IIO area was evolving during this work. Related changes had already landed, so each revision needed to be based on current `iio/testing` state to avoid duplicate or stale patches.

## Revision Timeline

| Revision | Patches | Major Evolution |
|----------|---------|-----------------|
| **v1** | 11 | Broad HID-IIO warning and coding-style cleanup. |
| **v2** | 6 | Reduced formatting churn and synchronized with the current IIO tree. |
| **v3** | 2 | Final focused series containing the remaining worthwhile changes. |

## Final / Current Outcome

| Item | Status |
|------|--------|
| Latest Revision | v3 |
| Initial Patch Count | 11 |
| Final Patch Count | 2 |
| Mainline | Not yet confirmed |
| linux-next | Applied |
| Status | Applied in linux-next |
| Last Verified | 2026-08-23 |

## Why This Series Matters

The series demonstrates that upstream quality is not measured by how many mechanical changes can be submitted. Review-driven scope reduction can produce a smaller contribution with clearer purpose, lower review overhead and stronger technical value.

## Key Lessons Learned

- Do not optimize for patch count; optimize for logical reviewability.
- Not every formatting change deserves its own patch.
- Consolidate mechanical churn when it does not provide independent review value.
- Separate style cleanup from resource ownership changes.
- Understand the actual owner of a devres-managed resource before changing the device argument.
- Rebase against the current subsystem development branch before preparing a new revision.
- Remove changes that have already landed through another series.

## Looking Back

If starting this work today, I would:

- Search the current `iio/testing` tree before preparing the initial series.
- Separate pure formatting cleanup from resource-management changes from the beginning.
- Verify devres ownership before changing the device argument.
- Re-run repository-wide searches after related HID-IIO series land.
- Prefer a small, clearly justified series over preserving a large initial patch set.

## Related Series

- [Series 008 – HID-IIO devm API and Resource-Management Modernization](series-008-hid-iio-devm-workstream.md)
- [Series 010 – HID-IIO Callback Setup and Device Exposure Ordering](series-010-hid-iio-callback-ordering.md)
- [Series 011 – HID-IIO `usage_id` Type Unification](series-011-hid-iio-usage-id.md)

## Related Learning

- [Mentorship growth](../mentorship-growth.md)
- [Upstream review process](../upstream-review-process.md)

## References

### Lore

- [v1 – 11 patches](https://lore.kernel.org/all/20260616-15-jun-hid-iio-alignment-v1-0-0cd544286575@gmail.com/)
- [v2 – 6 patches](https://lore.kernel.org/all/20260702-15-jun-hid-iio-alignment-v2-0-b87f01f5efbc@gmail.com/)
- [v3 – 2 patches](https://lore.kernel.org/all/20260707-15-jul-hid-iio-alignment-v3-0-8791574ad0fe@gmail.com/)

### linux-next

- [cff496bda5128dd9cf7a38fc2933440ee58b8ad1](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=cff496bda5128dd9cf7a38fc2933440ee58b8ad1)
- [d9290c908d6f31bcdf79c1fec9b7287cf65df19b](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=d9290c908d6f31bcdf79c1fec9b7287cf65df19b)
- [0c50c9e3b2a4acb2b5b238ba58537f5525532527](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=0c50c9e3b2a4acb2b5b238ba58537f5525532527)
- [a30824bbfb22f890df7e92448522b696c62ce965](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=a30824bbfb22f890df7e92448522b696c62ce965)
- [636deb551c2da89e798b2057d417be86ab9a3efc](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=636deb551c2da89e798b2057d417be86ab9a3efc)
- [2e2f2de7532cbbc2269de8be20ec709606c6e79b](https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/commit/?id=2e2f2de7532cbbc2269de8be20ec709606c6e79b)
