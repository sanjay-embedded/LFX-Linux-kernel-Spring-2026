# Series 000: Exploratory cleanup.h conversion

## Overview

This exploratory series proposed converting driver code across multiple kernel subsystems to use the `__free()` helper in cleanup paths. The intent was to modernize free helpers and make cleanup code more consistent across the tree.

## Background

The Linux kernel has long used various patterns for freeing resources in error and cleanup paths. The `__free()` helper provides a consistent, annotated mechanism for performing free operations in contexts where memory annotations help reviewers and static analysis.

## Objective

- Explore the impact of converting existing drivers to use `__free()`.
- Identify common conversion patterns and potential pitfalls.
- Gather reviewer feedback to determine whether subsystem-specific conversions are acceptable.

## Patch summary

The series included a set of mechanical conversions replacing ad-hoc free calls with the `__free()` helper where applicable. The changes spanned multiple subsystems and primarily focused on making cleanup paths use the standardized helper.

## Review summary

The series received reviews from multiple maintainers. Feedback highlighted that while the conversions were technically straightforward, the series scope crossed subsystem boundaries and was therefore not an ideal single submission. Reviewers suggested splitting the work into subsystem-specific series and focusing on higher-level design improvements where appropriate.

## Engineering discussion

Key discussion points:

- Subsystem maintainers prefer series scoped to their area to simplify review and acceptance.
- Purely mechanical conversions may not provide enough value to justify cross-subsystem churn.
- Conversions must ensure no behavioral change and must be carefully validated.

## Outcome

Not merged. The series was split into subsystem-specific series for subsequent submissions. The feedback shaped the approach for later IIO-targeted contributions.

## Lessons learned

- Respect subsystem boundaries when proposing wide-reaching changes.
- Prefer smaller, subsystem-scoped series.
- Use review feedback to iterate on the approach rather than pushing a large cross-cutting mechanical change.

## References

- Related discussions and review threads (maintainers' feedback).
