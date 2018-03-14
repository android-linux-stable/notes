# How to modify the Wahoo kernel source for on-device use

The Wahoo kernel source Google provides needs a few modifications to get it to work properly.

* Google has been pushing for kernel modules as part of Project Treble and insisting on the `/vendor` partition for their location (see [here](https://source.android.com/devices/architecture/kernel/modular-kernels) for more info). As a result, the touchscreen and battery drivers are located in `/vendor/lib/modules`. This is an extremely inconvenient location to modify as it is protected by both Android Verified Boot 2.0 (avb) and it can't be modified without root or breaking apart the image and reflashing. There are two ways to work around this:

  * Force the stock modules to load by ignoring them in the `check_version` function in `kernel/module.c`
    * [`ada01ae47140`](https://github.com/nathanchance/wahoo/commit/ada01ae4714044a9986b56dad0babcd6d5d8a3b8) ("walleye: Allow stock modules to load")
    * [`1a4f1c84b7cc`](https://github.com/nathanchance/wahoo/commit/1a4f1c84b7cca5559ab49b2be62be9b95e2c2408) ("taimen: allow stock modules to load")

  * Build the drivers into the kernel image. Apply the following changes depending on your device:

    * Pixel 2:

        * Change from `=m` to `=y` in wahoo_defconfig

          ```
          CONFIG_TOUCHSCREEN_SYNAPTICS_DSX_HTC=y
          CONFIG_TOUCHSCREEN_SYNAPTICS_DSX_CORE_HTC=y
          CONFIG_TOUCHSCREEN_SYNAPTICS_DSX_RMI_DEV_HTC=y
          CONFIG_TOUCHSCREEN_SYNAPTICS_DSX_FW_UPDATE_HTC=y
          CONFIG_HTC_BATTERY=y
          ```

        * Delete in wahoo_defconfig

          ```
          CONFIG_LGE_TOUCH_CORE=y
          CONFIG_LGE_TOUCH_LGSIC_SW49408=y
          CONFIG_TOUCHSCREEN_FTM4=y
          CONFIG_LGE_BATTERY=y
          ```


    * Pixel 2 XL:

        * Change from `=m` to `=y` in wahoo_defconfig

          ```
          CONFIG_LGE_TOUCH_CORE=y
          CONFIG_LGE_TOUCH_LGSIC_SW49408=y
          CONFIG_TOUCHSCREEN_FTM4=y
          CONFIG_LGE_BATTERY=y
          ```

        * Delete in wahoo_defconfig

          ```
          CONFIG_TOUCHSCREEN_SYNAPTICS_DSX_HTC=y
          CONFIG_TOUCHSCREEN_SYNAPTICS_DSX_CORE_HTC=y
          CONFIG_TOUCHSCREEN_SYNAPTICS_DSX_RMI_DEV_HTC=y
          CONFIG_TOUCHSCREEN_SYNAPTICS_DSX_FW_UPDATE_HTC=y
          CONFIG_HTC_BATTERY=y
          ```

       * Apply [`117ffa9fe699`](https://github.com/nathanchance/wahoo/commit/117ffa9fe6994b82604c71f93332537e362f3cb7) ("lge_battery: Use EPROBE_DEFER instead of ENODEV during probe")


* Google compiles the stock kernel with Clang 4.0 on 8.0 and Clang 5.0 on 8.1. As a result, the typical kernel commands like for GCC change a bit. Additionally, they also require the versions of `dtc` and `mkdtimg` provided by AOSP. I go over how this changes your compilation in the README of [my pixel2-manifest repo](https://github.com/nathanchance/pixel2-manifest).

* Flashing the kernel can be done of two ways:

  * A compiled boot image (which I cover in the pixel2-manifest repo linked right above), which can be flashed with `fastboot`.
  * An AnyKernel2 zip you can flash in TWRP. The support for the Pixel 2 is currently pending ([pull request](https://github.com/osm0sis/AnyKernel2/pull/12)). Once that has been merged, follow the instructions in the README, zip it up, and flash it with TWRP. Instructions for TWRP installation can be found on their website ([taimen](https://twrp.me/google/googlepixel2xl.html) and [walleye](https://twrp.me/google/googlepixel2.html)).
