## March 2026 – First Large Review Experience

Submitted an exploratory cleanup series spanning multiple kernel subsystems to adopt the `__free()` helper.

Although the series was not merged, feedback from multiple maintainers highlighted the importance of:

- Keeping patch series within a single subsystem
- Avoiding purely mechanical API conversions
- Focusing on design improvements over API replacement

This milestone significantly influenced the structure of all subsequent IIO-focused patch series.

**Related Series:** Series 000

---

## March 2026 – Applying Early Review Feedback

Following the exploratory cleanup series, I restructured the work into subsystem-specific patches.

The first result was a focused ST Sensors improvement that eliminated repeated temporary allocations by reusing the driver's existing `buffer_data[]` field.

The series evolved through reviewer feedback from Andy Shevchenko, Jonathan Cameron, and David Lechner before being accepted upstream.

**Related Series**

- Series 001 – ST Sensors buffer reuse

---

## March – May 2026: Managing a Long-Running Upstream Series

The SSP Sensors modernization became one of the longest-running review efforts during the mentorship. What began as a resource cleanup gradually evolved into a broader driver modernization initiative.

Continuous feedback from Jonathan Cameron, Andy Shevchenko, David Lechner, and other reviewers expanded the work beyond cleanup to include managed resource APIs, helper abstractions, probe-path improvements, and maintainability enhancements.

The experience reinforced the value of incremental development, reviewer collaboration, and allowing technical discussions to shape the final implementation.

**Related Series**

- Series 002 – SSP Sensors: Resource Cleanup & Driver Modernization

---

## April – July 2026: Applying Upstream Review Experience Across Subsystems

After several review cycles in the IIO subsystem, the same review principles were successfully applied to the Media subsystem.

An initial three-patch modernization series for the GC0310 camera sensor driver was refined following maintainer feedback, separating the functional clock-management improvement from unrelated cleanup work. The resulting focused patch adopted the `devm_v4l2_sensor_clk_get()` helper and was accepted into linux-next.

This milestone demonstrated that upstream development practices—such as patch scoping, incremental improvements, and subsystem-specific helper adoption—are transferable across Linux kernel subsystems.

**Related Series**

- Series 003 – GC0310 Clock Modernization

---

## April 2026 – Learning When Not to Change Code

While working on cleanup patches for the AD7173 ADC driver, review discussions highlighted that not every warning reported by automated tooling represents a defect in the driver.

A discussion around `checkpatch.pl` and SI unit naming demonstrated the importance of understanding the intent behind coding standards rather than applying mechanical fixes. The series concluded without further revisions, but it reinforced the value of engineering judgment and reviewer expertise when evaluating automated analysis results.

**Related Series**

- Series 004 – AD7173 Checkpatch Analysis

---

## April – August 2026: From Cleanup to Correctness

The MMA8452 work began as a focused PM modernization but evolved through five revisions into a broader driver modernization effort.

During review and self-review, the work expanded to resource lifetime, IRQ management, regulator handling, IIO cleanup helpers and error propagation. Importantly, the modernization process exposed race conditions that required correction.

The series also demonstrated how upstream work evolves after partial acceptance: individual patches were accepted independently, while the remaining changes were reduced and continued through subsequent revisions.

This strengthened my understanding that kernel cleanup is not only about adopting newer APIs; it requires understanding concurrency, resource ordering, subsystem infrastructure and how maintainers consume individual patches.

**Related Series**

- [Series 005 – MMA8452 modernization](patch-series/series-005-mma8452-modernization.md)

---

## April 2026 – Learning to Track Subsystem State

The ADXL313 cleanup series provided an important upstream workflow lesson.

The initial three-patch series included a `guard()` conversion that was already available in the IIO development tree. After reviewer feedback, the work was rebased on `iio/testing` and the redundant change was removed.

The remaining cleanup was then extended to closely related ADXL accelerometer drivers and accepted as an eight-patch series.

This reinforced the importance of synchronizing development with the subsystem tree before preparing new revisions and avoiding duplicate work already present upstream.

**Related Series**

- [Series 006 – ADXL accelerometer cleanup](patch-series/series-006-adxl-accelerometer-cleanup.md)

---

## April – May 2026: Understanding Kernel Ownership and Maintainer Coverage

The ADI IIO MAINTAINERS work started as a simple correction of outdated maintainer information but evolved into a broader investigation of sustainable ownership and review coverage.

Through six revisions, the work explored individual maintainership, mailing-list coverage, wildcard entries, redundant driver-specific entries, and active maintainer assignments.

The series expanded significantly in v4 before being reduced again as actual ownership and coverage were reviewed. The final approach combined persistent ADI mailing-list coverage with specific maintainers where appropriate.

This contribution expanded my understanding of upstream Linux beyond driver implementation into subsystem ownership, maintainership models, and the information maintainers rely on to route patches and reviews.

**Related Series**

- [Series 007 – ADI IIO MAINTAINERS Coverage](patch-series/series-007-adi-iio-maintainers.md)

---

## April – August 2026: Learning to Structure Cross-Driver Modernization

The HID-IIO workstream became the largest and most structurally complex contribution effort during the mentorship.

It began as a 10-patch API cleanup, expanded to 36 patches while exploring common device handling and driver conversions, and was ultimately restructured into a focused 13-patch parent series with related driver conversions moved into independent submissions.

This experience demonstrated that successful upstream development is not only about identifying useful technical changes. Large-scale modernization must also be organized around logical ownership, patch independence and reviewability.

**Related Series**

- [Series 008 – HID-IIO devm API and Resource-Management Modernization](patch-series/series-008-hid-iio-devm-workstream.md)

---

## June 2026 – Maintaining the IIO Contributor Roadmap

Updated the IIO TODO documentation to correct inaccuracies and refine resource-management guidance based on the current IIO API and cleanup model.

The v2 revision was applied in linux-next.

This contribution demonstrated that upstream participation extends beyond driver code: accurate subsystem documentation also helps future contributors identify meaningful and current areas for development.

**Related Series**

- [Series 009 – IIO TODO Documentation](patch-series/series-009-iio-todo-documentation.md)

---

## June 2026 – Refining a Bug Claim Through Review

The HID-IIO callback ordering work initially described the problem as a race condition that could result in NULL dereference or use-after-free.

During review, maintainers challenged whether the claimed failure mode could actually be demonstrated. Investigation of the IIO registration and HID callback paths showed that the more defensible concern was an exposure window that could result in dropped samples or stale data.

The final v2 series therefore changed the problem statement, removed unsupported `Fixes:` tags, refined the commit-message rationale, and was applied to linux-next as eight patches.

This was an important step in developing upstream debugging and review maturity: the implementation was not simply defended; the technical claim itself was revised to match the evidence.

**Related Series**

- [Series 010 – HID-IIO Callback Ordering](patch-series/series-010-hid-iio-callback-ordering.md)

---

## June 2026 – Completing a Cross-Driver API Type Migration

Unified `usage_id` types across ten HID-IIO drivers to match the `u32` type defined by the HID sensor hub callback API.

The initial seven-patch series was reviewed and applied. A subsequent repository-wide audit identified three remaining drivers, which were submitted and applied as a focused follow-up series.

This contribution reinforced an important upstream workflow: complete the initial focused change, audit the resulting tree, and use a small follow-up for remaining instances rather than reopening accepted work.

**Related Series**

- [Series 011 – HID-IIO `usage_id` Type Unification](patch-series/series-011-hid-iio-usage-id.md)

---

## June – July 2026 – Learning to Reduce Patch-Series Scope

The HID-IIO warning and coding-style series evolved from 11 patches in v1 to 6 in v2 and finally 2 focused patches in v3.

Reviewer feedback highlighted that several formatting-only patches represented unnecessary churn. The series was subsequently consolidated, rebased against the current IIO development tree, and reduced to changes with clearer independent value.

This reinforced an important upstream lesson: patch quality is not measured by the number of changes submitted. A smaller series with clear purpose, correct scope and low review overhead is often the stronger contribution.

**Related Series**

- [Series 012 – HID-IIO Warning and Coding-Style Cleanup](patch-series/series-012-hid-iio-warning-cleanup.md)

---

## June 2026 – HID Temperature Teardown Ordering Fix

Extracted a focused correctness fix from the broader HID-IIO callback/device-exposure work.

The initial patch claimed a potential use-after-free. Maintainer review challenged the failure mechanism, leading to investigation of the actual teardown path and identification of a concrete timeout caused by the IIO device remaining exposed after the sensor-hub callback was removed.

The implementation remained unchanged in v2, while the commit message was rewritten to accurately describe the demonstrated failure. The fix was subsequently applied in linux-next.

**Related Series**

- [Series 013 – HID Temperature Teardown Ordering](patch-series/series-013-hid-temperature-teardown.md)
- [Series 010 – HID-IIO Callback Ordering](patch-series/series-010-hid-iio-callback-ordering.md)
