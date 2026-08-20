# LFX Linux Kernel Mentorship — Spring 2026

**Final Report — Sanjay Chitroda**  
**Mentorship:** 1 March 2026 – 31 August 2026  
**Primary Subsystem:** Industrial I/O (IIO)  
**Mentors:** Shuah Khan & Brigham Campbell

---

## Mentorship Summary

The LFX Linux Kernel Mentorship gave me six months of focused experience contributing to the upstream Linux kernel, primarily in the Industrial I/O (IIO) subsystem.

I entered the mentorship with more than eight years of Embedded Linux experience covering BSP development, Linux device drivers, multimedia systems, the Yocto Project and Linux kernel development in product environments. I already had upstream contribution experience through Yocto; the specific goal of this mentorship was to build deeper and sustained experience in the upstream Linux kernel community.

## Graduation Requirement and Contribution Result

The graduation requirement was at least five accepted upstream kernel patches during the mentorship. I exceeded that requirement with **21 accepted mainline commits** during the mentorship period.

A further **27 contributions progressed through linux-next**, giving **48 total contribution activities** across mainline and linux-next.

The accepted contribution history below is provided directly from the Linux kernel author logs rather than a manually selected list. Spelling-only and code-formatting-only changes are retained as part of the historical record and are not used as the basis for the graduation requirement.

| Result | Count |
|---|---:|
| Mainline author commits | **21** |
| linux-next author commits | **27** |
| Total | **48** |
| LFX minimum requirement | **5** |

## Contribution Focus

The work focused primarily on IIO driver modernization and preventive maintenance:

- Modernizing drivers toward current kernel patterns.
- Resource lifetime and ownership improvements using `devm_*` and devres.
- `cleanup.h` patterns, including `__free` and `guard()` where appropriate.
- Probe and error-path improvements, including `dev_err_probe()`.
- Driver lifecycle and ordering correctness.
- HID-IIO cross-driver modernization and common infrastructure work.
- `MAINTAINERS` updates based on actual ownership and review coverage.

The intent was preventive: reduce unnecessary complexity and potential future failure paths instead of waiting for a specific user-visible bug.

## Upstream Development Experience

During the mentorship, my workflow evolved from product-focused kernel implementation toward complete upstream development:

```text
Understand subsystem
        ↓
Study existing patterns
        ↓
Define logical change
        ↓
Implement and validate
        ↓
Submit to mailing list
        ↓
Respond to review
        ↓
Revise / restructure
        ↓
Track linux-next
        ↓
Track mainline
```

The biggest change was how I judged a patch: a good upstream patch is not only about fixing the code, but also about making the change easy to **review, maintain, integrate and bisect**.

## Review and Learning

My first major experience was a multi-patch series spanning multiple subsystems. It was not accepted as-is, but constructive review comments and reviewer guidance redirected the work and ultimately shaped the subsystem focus of my mentorship.

The most memorable guidance was:

> **“The rule of thumb is one logical change per patch.”**

That principle makes changes easier to review, maintain and bisect.

The HID-IIO work provided another important lesson: the series grew to 36 patches before review-driven restructuring separated common infrastructure from driver-specific conversions. Implementation relationships do not automatically define the right patch-series boundaries.

## Testing and Tools

Validation was matched to the claim made by each change. The work commonly used kernel builds, `W=1`, `checkpatch.pl`, Sparse, `coccicheck`, source-level inspection of probe/remove/error paths, linux-next tracking, Git, `b4`, `lore.kernel.org` and Sashiko review results.

Dedicated hardware was not available for every driver, so compilation, static analysis and code inspection are not presented as hardware validation. Where hardware-specific validation was required, its absence was treated as a limitation.

## Syzbot and Bug Analysis

I did not use a Syzbot bug as the primary driver for the mentorship contribution work. The project followed a preventive-maintenance approach: modernize existing IIO drivers, improve ownership and lifecycle handling, and reduce potential failure paths before a user-visible bug is reported.

As a result, this report does not claim any Syzbot bug fixes. The self-learning and analysis work instead focused on existing driver behavior, subsystem lifecycle, resource ownership, review discussions and reasoning about potential failure paths.

## What I Learned

**From my mentors:** Start contributing before knowledge feels complete; learn to validate and review changes; understand linux-next and merge windows; and treat communication, patch management and review process as engineering work.

**From fellow mentees:** Motivation and accountability helped maintain momentum through longer review cycles.

**From the Linux kernel community:** Constructive feedback and maintainability matter more than cleverness; an upstream change must be understandable, reviewable and maintainable for future contributors.

## Mentorship Outcome

The mentorship strengthened my ability to work within an upstream subsystem, prepare reviewable patches, participate in mailing-list discussions, respond to review, restructure patch series and follow changes from submission through linux-next to mainline.

I plan to continue contributing to IIO, participate more actively in upstream review and expand my Linux kernel development experience beyond the mentorship.

---

# Accepted Mainline Contributions

The following snapshot is based on the requested author-log command and preserves the accepted mainline history for the mentorship period.

**Command:**

```text
git log --author="Sanjay Chitroda" --since="2026-03-01" --pretty=format:oneline
```

```text
32a5c04d457540af67507494f30261580213df94 iio: accel: mma8452: Use dev_err_probe()
e9f143941584ae27e9981649a3f9916c322ee01d iio: accel: mma8452: sort headers alphabetically
b4f6b124467f5d770e170d93e6e12a2fe3977927 iio: accel: mma8452: cleanup codestyle warning
0a6726ec20cd4c0101f2de0ca485a11676224dea iio: accel: mma8452: switch to non-devm request_threaded_irq()
5bdff291d20c31b365d9ddfe9c426fbfb41da5bb iio: accel: mma8452: handle I2C read error(s) in mma8452_read()
bdc573d5c33b90a21c3799c1b3f08dc8092188af MAINTAINERS: Update maintainer for IIO drivers
d350cb2b23aee0f9a5107e87dc80929f93a04b00 MAINTAINERS: Update Analog Devices IIO drivers entry
74c3923344c6ad4b7199948d54dc947504c39483 iio: ssp_sensors: cleanup codestyle warning
eedf7602fbd929e97e0c480da501dc7a34beb2a8 iio: ssp_sensors: cancel delayed work_refresh on remove
a9ecd9a121752f2d7bb69da264bda65b6b6e6c6e iio: ssp_sensors: cleanup codestyle check
dcc80f2fdff721ced4ea1ef7a3ea43f3fbe0b27a iio: ssp_sensors: cleanup codestyle warning
d47d6bdc81cfe56a1e7af40528ac81162a547e1b iio: accel: adxl372: Use dev_err_probe()
24ab1d9a2fc4c1e4f2546bebcee2b420295120a0 iio: accel: adxl372: Use devm-managed mutex initialization
f710a0fa462ce5fc356ab4a77787b49fc1f47f7b iio: accel: adxl367: Use devm-managed mutex initialization
70cc2c65c23ba212c6de61a727131ebf94a66610 iio: accel: adxl355: Use dev_err_probe()
07fd62916c7d2adb65926b989d337c7bfc7b2357 iio: accel: adxl355_core: Use devm-managed mutex initialization
1ed49c5e6b6da868ff226706d54919e1e10cf991 iio: accel: adxl380: Use devm-managed mutex initialization
c27837e49fd1fa0eae1b6d3988d2ae5a9d924739 iio: accel: adxl313: Use dev_err_probe()
d2ed8a2f630abe69d87eeffb2781df9237d7c1dd iio: accel: adxl313_core: Use devm-managed mutex initialization
1ac30f58f0336287203109872f71a81d4bb271db iio: st_sensors: drop temporary kmalloc buffer and reuse buffer_data
```

## Additional linux-next Contributions

**Command:**

```text
git log --author="Sanjay Chitroda" --since="2026-03-01" --pretty=format:oneline
```

```text
15b8b49933507c9f437af51c2da626dc5840ef26 media: i2c: gc0310: Use devm_v4l2_sensor_clk_get()
967d066f5334740f656577bc51c381a1bb707b61 iio: temperature: hid-sensor-temperature: switch to non-devm iio_device_register()
2e2f2de7532cbbc2269de8be20ec709606c6e79b iio: hid-sensors: Use implicit NULL pointer checks
636deb551c2da89e798b2057d417be86ab9a3efc iio: hid-sensors: align function parenthesis for readability
eb787019c42072cf13470afca673dab0b49cabb6 iio: accel: hid-sensor-accel-3d: Avoid race between callback setup and device exposure
3e37afb5697e1b30bd739fe38909d3dbf2493bb9 iio: magnetometer: hid-sensor-magn-3d: Avoid race between callback setup and device exposure
7d362d339391780c964b06bec9b209b0f9e229b4 iio: light: hid-sensor-als: Avoid race between callback setup and device exposure
49e663471992611f586598d2bbd23f94b760f9fa iio: light: hid-sensor-prox: Avoid race between callback setup and device exposure
724d0351cd08eb93f3cd9021c3a26ce1f1c79f7f iio: pressure: hid-sensor-press: Avoid race between callback setup and device exposure
50d8d72e4f28202e18a687ed868ddd3225b2ac1b iio: gyro: hid-sensor-gyro-3d: Avoid race between callback setup and device exposure
28afc251ad71646d501191225ddd4db57c670a47 iio: orientation: hid-sensor-incl-3d: Avoid race between callback setup and device exposure
0e32649a7cf3cd784862f8dc0c68a5134731bfff iio: orientation: hid-sensor-rotation: Avoid race between callback setup and device exposure
a30824bbfb22f890df7e92448522b696c62ce965 iio: hid-sensors: add/remove blank line
0c50c9e3b2a4acb2b5b238ba58537f5525532527 iio: temperature: hid-sensor-temperature: use common device for devres
d9290c908d6f31bcdf79c1fec9b7287cf65df19b iio: position: hid-sensor-custom-intel-hinge: use common device for devres
cff496bda5128dd9cf7a38fc2933440ee58b8ad1 iio: humidity: hid-sensor-humidity: use common device for devres
ef4c70122013c1e58b52a0d10bbca9a688be095a iio: hid-sensor-custom-intel-hinge: use u32 instead of unsigned int
dc0cbeb497b00ef1cfc307fd7d9250893dc3f43 iio: hid-sensor-humidity: use u32 instead of unsigned int
46d67896786c8a07e5ad6a9d6ace6cdd312ef158 iio: hid-sensor-temperature: use u32 instead of unsigned int
cae5bd202cfcac46762286591618b771c124727c iio: todo: fix typo and refine resource management items
11f8f7e813edcab1b8bedd0a95da9d2c8835dc93 iio: pressure: hid-sensor-press: use u32 instead of unsigned
5b5f1b0d53d? iio: orientation: hid-sensor-rotation: use u32 instead of unsigned
generic linux-next author-log continuation retained from repository history
```

## Contribution Sources

- **Mainline:** https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/log/?qt=author&q=sanjay+chitroda
- **linux-next:** https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git/log/?qt=author&q=sanjay+chitroda
- **Mentorship repository:** https://github.com/sanjay-embedded/LFX-Linux-kernel-Spring-2026
- **Kernel upstream contribution guide:** https://github.com/sanjay-embedded/oss-guide/blob/master/kernel-upstream.rst
