## mainline kernel commits

$ git remote -v

linux-torvalds	https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git (fetch)

linux-torvalds	https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git (push)

--------------------------------------------------------------------------------------------
$ git log --author="Sanjay Chitroda" --since="2026-03-01" --pretty --format=oneline

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


## linux-next kernel commits

$ git remote -v

linux-next	https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git (fetch)

linux-next	https://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git (push)

--------------------------------------------------------------------------------------------
$ git log --author="Sanjay Chitroda" --since="2026-03-01" --pretty --format=oneline

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

dc0cbeb497b00ef1c1fc307fd7d9250893dc3f43 iio: hid-sensor-humidity: use u32 instead of unsigned int

46d67896786c8a07e5ad6a9d6ace6cdd312ef158 iio: hid-sensor-temperature: use u32 instead of unsigned int

cae5bd202cfcac46762286591618b771c124727c iio: todo: fix typo and refine resource management items

11f8f7e813edcab1b8bedd0a95da9d2c8835dc93 iio: pressure: hid-sensor-press: use u32 instead of unsigned

d92974cded424b8161dd6b41e45fd2e7a2c69dbc iio: orientation: hid-sensor-rotation: use u32 instead of unsigned

2253c055bcdc298e49b2d2d5abcb784e2e9fd727 iio: orientation: hid-sensor-incl-3d: use u32 instead of unsigned

946d6045f442ad1c705c5dfb7f48747e84a4180a iio: light: hid-sensor-prox: use u32 instead of unsigned

d5b231ec6b0903480bae49475c7acd31e0077a4c iio: light: hid-sensor-als: use u32 instead of unsigned

b720b5d6835cd8a61db248b1ff5798a69a470719 iio: accel: hid-sensor-accel-3d: use u32 instead of unsigned

b66a56fae18f1d348d5e8dcfcb75d7800ab936f9 iio: gyro: hid-sensor-gyro-3d: use u32 instead of unsigned

