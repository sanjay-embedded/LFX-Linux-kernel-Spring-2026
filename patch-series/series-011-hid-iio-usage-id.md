# Series 011 – HID-IIO `usage_id` Type Unification

## Executive Summary

This work unified the `usage_id` type used by HID-IIO callback implementations with the `u32` type defined by the HID sensor hub callback API.

The work started as a focused seven-patch cleanup. During review, Jonathan Cameron requested that the commit message explicitly explain the relationship between the local `usage_id` type and the callback API signature.

After the v2 series was applied, a repository-wide audit identified three remaining HID-IIO drivers using `unsigned int`. Those drivers were submitted as a separate three-patch follow-up series and applied independently.

The complete work therefore covered ten HID-IIO driver changes across two related submissions.

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
| Status | Applied in linux-next |
| Mainline | Not yet confirmed |
| Last Verified | 2026-08-23 |
| Main Maintainer | Jonathan Cameron |
| Primary Change | `unsigned` / `unsigned int` → `u32` |

## Background

The HID sensor hub callback API defines `usage_id` as `u32`. Several HID-IIO callback implementations nevertheless used `unsigned` or `unsigned int` for the corresponding parameter.

The cleanup aligned the local implementation with the API contract.

## Initial Objective

The initial seven-patch series aimed to:

- identify HID-IIO callback implementations using a different type;
- change `usage_id` to `u32`;
- match the HID callback API signature;
- improve type consistency across HID-IIO drivers.

All patches were W=1 build-tested.

## Technical Evolution

### v1 – Initial 7-patch cleanup

Converted `usage_id` from `unsigned` to `u32` in seven HID-IIO drivers.

### Review – API contract clarification

Jonathan Cameron requested that the commit message explicitly explain why `u32` was the correct type. The justification was the existing HID callback API contract.

### v2 – Refined rationale

The code scope remained unchanged, while the commit messages explicitly referenced the callback API and its type contract.

### Follow-up – 3 remaining drivers

A repository-wide audit after application identified three remaining callbacks using `unsigned int`. Rather than reopening the accepted series, the remaining changes were submitted as a focused follow-up.

## Review Evolution

The key change was moving the rationale from:

```text
change unsigned to u32
```

to:

```text
match the HID callback API signature
```

This made the cleanup technically justified instead of merely stylistic.

## Interesting Engineering Discussions

### 1. Type consistency follows the API contract

The important point is not simply that `u32` is preferred. The implementation should match the API that it implements.

### 2. Repository-wide cleanup needs a completion audit

The initial series covered seven drivers, but a second repository-wide search found three remaining instances. Verifying the resulting tree is part of completing a migration.

### 3. Follow-up is preferable to reopening accepted work

Once the seven-patch series was applied, the three remaining drivers were submitted independently. This kept the accepted series stable and made the remaining work independently reviewable.

### 4. Search methodology matters

For repeated kernel-tree audits, Git-aware searches such as `git grep` are useful for identifying remaining consumers and verifying completion.

## Revision Timeline

| Stage | Date | Patches | Major Evolution |
|------|------|---------|-----------------|
| **v1** | 06 Jun 2026 | 7 | Initial `usage_id` → `u32` conversion. |
| **v2** | 10 Jun 2026 | 7 | Commit messages clarified to reference the HID callback API; series applied. |
| **Follow-up v1** | 16 Jun 2026 | 3 | Three remaining drivers converted separately. |
| **Final** | Jun 2026 | 10 total | Complete HID-IIO `usage_id` type unification applied. |

## Final / Current Outcome

| Item | Status |
|------|--------|
| Initial Series | 7/7 applied |
| Follow-up | 3/3 applied |
| Total Logical Changes | 10/10 applied |
| linux-next | Applied through IIO development flow |
| Mainline | Not yet confirmed |
| Functional Impact | None intended |
| Last Verified | 2026-08-23 |

## Why This Series Matters

This work shows that even a mechanical type-unification change benefits from a precise API-based rationale, a repository-wide completion audit, and a disciplined follow-up strategy.

## Key Lessons Learned

- Match implementation types to the actual subsystem API contract.
- A mechanical cleanup should still explain the technical reason for the change.
- Perform a repository-wide audit after a broad cleanup to identify remaining instances.
- A focused follow-up series is preferable to reopening an already-applied series.
- Use `git grep` for efficient kernel-tree migration and completion audits.
- Separate “what changed” from “why the API requires it” in commit messages.

## Looking Back

If starting this work today, I would:

- Search the complete HID-IIO tree before preparing the first series.
- Use `git grep` from the beginning to identify all callback implementations.
- Explicitly compare local callback signatures against the HID API definitions.
- Verify no remaining `unsigned` / `unsigned int` instances exist before sending the first series.
- Use a focused follow-up if additional instances are discovered after application.

## Related Series

- [Series 008 – HID-IIO devm API and Resource-Management Modernization](series-008-hid-iio-devm-workstream.md)
- [Series 010 – HID-IIO Callback Setup and Device Exposure Ordering](series-010-hid-iio-callback-ordering.md)
- [Series 012 – HID-IIO Warning and Coding-Style Cleanup](series-012-hid-iio-warning-cleanup.md)

## Related Learning

- [Mentorship growth](../mentorship-growth.md)
- [Upstream review process](../upstream-review-process.md)

## References

### Lore

- Initial v1 – 7 patches
- Initial v2 – 7 patches
- Follow-up – 3 patches

### linux-next

- `b66a56fae18f1d348d5e8dcfcb75d7800ab936f9`
- `b720b5d6835cd8a61db248b1ff5798a69a470719`
- `d5b231ec6b0903480bae49475c7acd31e0077a4c`
- `946d6045f442ad1c705c5dfb7f48747e84a4180a`
- `2253c055bcdc298e49b2d2d5abcb784e2e9fd727`
- `d92974cded424b8161dd6b41e45fd2e7a2c69dbc`
- `11f8f7e813edcab1b8bedd0a95da9d2c8835dc93`
- `46d67896786c8a07e5ad6a9d6ace6cdd312ef158`
- `dc0cbeb497b00ef1c1fc307fd7d9250893dc3f43`
- `ef4c70122013c1e58b52a0d10bbca9a688be095a`
