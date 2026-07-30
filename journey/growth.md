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
