# Patch series dashboard

| ID  | Title                                               | Status     | Duration     | Revisions | Tags                                              | Outcome                              | Key Learning                 |
| --- | --------------------------------------------------- | ---------- | ------------ | --------- | ------------------------------------------------- | ------------------------------------ | ---------------------------- |
| 000 | cleanup.h: Convert drivers to use `__free()` helper | Not merged |              | v1        |                                                   | Split into subsystem-specific series | Respect subsystem boundaries |
| 001 | ST Sensors – Reuse `buffer_data[]`                  | Merged     |              | v2→v4     |                                                   | Merged to mainline (see series doc)  | Design improvement over mechanical cleanup |
| 002 | SSP Sensors – Resource Cleanup & Driver Modernization | In Review  | Mar–May 2026 | v2→v8     | cleanup.h, devm, guard(), refactor, probe, IIO   | Partially merged                     | cleanup.h, devm, guard(), refactor, probe, IIO |
| 003 | GC0310 – Sensor Clock Modernization                 | Merged (linux-next) | Apr–Jul 2026 | Initial → v2 | media, v4l2, devm, clk, camera                | Accepted into linux-next             | Separate functional improvements from cleanup |
