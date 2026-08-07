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

The SSP Sensors modernization became one of the longest-running review efforts during the mentorship. What began as a resource cleanup gradually evolved into a broader driver modernization initiative through seven revisions.

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
