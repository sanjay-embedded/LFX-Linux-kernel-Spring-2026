# Patch series dashboard

| ID  | Title                                                | Status                     | Duration     | Revisions    | Tags                                                        |
| --- | ---------------------------------------------------- | -------------------------- | ------------ | ------------ | ----------------------------------------------------------- |
| 000 | cleanup.h: Convert drivers to use `__free()` helper  | Not merged                 |              | v1           |                                                             |
| 001 | ST Sensors – Reuse `buffer_data[]`                   | Merged                     |              | v2→v4        |                                                             |
| 002 | SSP Sensors – Resource Cleanup & Driver Modernization | Partially Merged / Ongoing | Mar–May 2026  | v2→v8        | cleanup.h, devm, guard(), refactor, probe, IIO              |
| 003 | GC0310 – Sensor Clock Modernization                  | Merged (linux-next)        | Apr–Jul 2026 | Initial → v2 | media, v4l2, devm, clk, camera                             |
| 004 | AD7173 – Checkpatch & Coding Style Analysis          | Closed after review        | Apr 2026     | v1           | checkpatch, codestyle, IIO, tooling                         |
| 005 | MMA8452 – Modern Coding Style, PM & Resource Cleanup | Partially merged / ongoing | Apr–Aug 2026 | Initial → v5 | IIO, PM, devm, guard, IRQ, regulator, cleanup               |
| 006 | ADXL Accelerometer Cleanup & Error Handling          | Merged                     | Apr 2026     | v1 → v2      | IIO, devm, dev_err_probe, mutex, accelerometer              |
