# Series 011 – HID-IIO `usage_id` Type Unification

## Executive Summary

This work unified the `usage_id` type used by HID-IIO callback implementations with the `u32` type defined by the HID sensor hub callback API.

The work started as a focused seven-patch cleanup. During review, Jonathan Cameron requested that the commit message explicitly explain the relationship between the local `usage_id` type and the callback API signature.

After the v2 series was applied, a repository-wide audit identified three remaining HID-IIO drivers using `unsigned int`. Those drivers were submitted as a separate three-patch follow-up series and applied independently.

The complete work therefore covered ten HID-IIO driver changes across two related Lore submissions.

---

## Quick Facts

| Item | Details |
|------|---------|
| Workstream | HID-IIO `usage_id` type unification |
| Initial Series | `HID: iio: basic clean up for usage_id` |
| Follow-up | `HID: iio: callback API signature match for usage_id` |
| Subsystem | Industrial I/O (IIO) / HID Sensors |
| Initial Submission | 06 June 2026 |
| Initial Final Revision | v2 – 10 June 2026 |
| Follow-up Submission | 16 June 2026 |
| Initial Patch Count | 7 |
| Follow-up Patch Count | 3 |
| Total Logical Changes | 10 |
| Revisions | Initial v1 → v2 + follow-up v1 |
| Status | Applied in linux-next / IIO development flow |
| Main Maintainer | Jonathan Cameron |
| Reviewers | Jonathan Cameron, Andy Shevchenko, Maxwell Doose, David Lechner |
| Primary Change | `unsigned` / `unsigned int` → `u32` |

---

## Background

The HID sensor hub callback API defines `usage_id` as `u32`.

Several HID-IIO callback implementations nevertheless used `unsigned` or `unsigned int` for the corresponding parameter.

The cleanup aligned the local implementation with the API contract:

```text
HID sensor hub API
        |
        | usage_id = u32
        v
HID-IIO callback implementation
        |
        | usage_id = u32
        v
consistent interface
```

## Initial Objective

The initial seven-patch series aimed to:

identify HID-IIO callback implementations using a different type;
change usage_id to u32;
match the HID callback API signature;
improve type consistency across the HID-IIO drivers.

All patches were W=1 build-tested.

## Revision Evolution
### v1 – Initial 7-patch cleanup

The initial series converted usage_id from unsigned to u32 in seven HID-IIO drivers.

Affected drivers included:

gyro;
accelerometer;
ALS;
proximity;
inclination;
rotation;
pressure.

The change was intended to be a straightforward type-unification cleanup.

### Review – API contract clarification

Jonathan Cameron requested that the commit message explicitly explain why u32 was the correct type.

The important justification was the existing HID callback API:

usage_id = u32

Therefore, the callback implementations should use the same type.

This strengthened the commit rationale from:

"change unsigned to u32"

to:

"match the HID callback API signature"

### v2 – Refined rationale

The code scope remained unchanged.

The revision:

clarified the commit messages;
explicitly referenced the HID callback API;
added the appropriate review tags;
retained the mechanical nature of the change.

The seven-patch series was then applied to the IIO testing branch.

### Follow-up – 3 remaining drivers

After the initial series was applied, another repository-wide audit identified three remaining HID-IIO callbacks using unsigned int.

The remaining drivers were:

temperature;
humidity;
custom Intel hinge.

Rather than reopening the already-applied seven-patch series, the remaining changes were submitted as a focused three-patch follow-up.

The follow-up was also reviewed and applied.

## Overall Evolution
HID callback API
      |
      | usage_id = u32
      |
      v
Initial repository audit
      |
      +----------------------+
      |                      |
   7 drivers             3 drivers
      |                      |
      v                      v
  v1 → v2                follow-up
      |                    3 patches
      v                      |
   applied                  applied
      |                      |
      +----------+-----------+
                 |
                 v
       10 HID-IIO drivers
       consistently use u32

## Review Summary
Reviewer	Main Contribution
Jonathan Cameron	Requested explicit explanation of the callback API signature and why u32 is the appropriate local type. Applied the initial series and follow-up.
Andy Shevchenko	Reviewed the follow-up and confirmed it completed the remaining type unification. Suggested git grep for repository-wide searches.
Maxwell Doose	Provided Reviewed-by for the initial seven-patch series.
David Lechner	Participated in the broader HID-IIO usage_id discussion.

## Interesting Engineering Discussion
### 1. Type consistency should follow the API contract

The important engineering point is not simply that u32 is preferred.

The implementation should match the API that it implements.

API:

capture_sample(..., u32 usage_id, ...)
send_event(..., u32 usage_id, ...)

Implementation:

callback(..., u32 usage_id, ...)

This makes the relationship between the API and its consumers explicit.

### 2. Repository-wide cleanup needs a completion audit

The initial series covered seven drivers, but the work was not actually complete.

A second repository-wide search identified three remaining instances.

This demonstrated the importance of verifying the final tree rather than assuming that the initial search covered every consumer.

### 3. Follow-up is preferable to reopening accepted work

Once the seven-patch series had been applied, the three remaining drivers were not added retroactively.

Instead:

accepted series
      ↓
new audit
      ↓
remaining instances
      ↓
focused follow-up

This keeps the already-reviewed series stable and gives the remaining changes their own focused review.

### 4. Improve search methodology

Andy recommended using git grep rather than a longer find | xargs | grep pipeline.

For kernel-tree migration work, Git-aware searches are useful because they operate directly on the repository and make repeated audits easier.

## Revision Timeline
Stage	Date	Patches	Major Evolution
v1	06 Jun 2026	7	Initial usage_id → u32 conversion.
v2	10 Jun 2026	7	Commit messages clarified to reference the HID callback API; series applied.
Follow-up v1	16 Jun 2026	3	Three remaining drivers converted and submitted separately.
Final	Jun 2026	10 total	Complete HID-IIO usage_id type unification applied.

## Final Outcome
Item	Status
Initial Series	7/7 applied
Follow-up	3/3 applied
Total Logical Changes	10/10 applied
linux-next	✅ Applied through IIO development flow
Mainline	Track subsequent IIO merge status
Functional Impact	None intended
Final State	HID-IIO callback usage_id types aligned with API

## Key Lessons Learned
Match implementation types to the actual subsystem API contract.
A mechanical cleanup should still explain the technical reason for the change.
Perform a repository-wide audit after a broad cleanup to identify remaining instances.
A focused follow-up series is preferable to reopening an already-applied series.
Use git grep for efficient kernel-tree migration and completion audits.
Keep functional behavior unchanged when performing type-unification cleanups.
Separate "what changed" from "why the API requires it" in commit messages.

## Looking Back

If starting this work today, I would:

Search the complete HID-IIO tree before preparing the first series.
Use git grep from the beginning to identify all callback implementations.
Explicitly compare local callback signatures against the HID API definitions.
Verify that no remaining unsigned / unsigned int instances exist before sending the first series.
If additional instances are discovered after application, use a focused follow-up rather than reopening the accepted series.

## Related Series
Series 008 – HID-IIO devm API and Resource-Management Modernization
Series 010 – HID-IIO Callback Setup and Device Exposure Ordering

## Workstream Relationship

The usage_id cleanup is related to the broader HID-IIO modernization work:

Series 008
HID-IIO devm infrastructure
        |
        +---------------------------+
        |                           |
        v                           v
Series 010                    Series 011
callback/device               usage_id API
ordering                      type consistency
        |                           |
        +-------------+-------------+
                      |
                      v
             HID-IIO modernization

## References
### Lore
Initial v1 – 7 patches
Initial v2 – 7 patches
Follow-up – 3 patches

### linux-next
b66a56fae18f1d348d5e8dcfcb75d7800ab936f9
b720b5d6835cd8a61db248b1ff5798a69a470719
d5b231ec6b0903480bae49475c7acd31e0077a4c
946d6045f442ad1c705c5dfb7f48747e84a4180a
2253c055bcdc298e49b2d2d5abcb784e2e9fd727
d92974cded424b8161dd6b41e45fd2e7a2c69dbc
11f8f7e813edcab1b8bedd0a95da9d2c8835dc93
46d67896786c8a07e5ad6a9d6ace6cdd312ef158
dc0cbeb497b00ef1c1fc307fd7d9250893dc3f43
ef4c70122013c1e58b52a0d10bbca9a688be095a
