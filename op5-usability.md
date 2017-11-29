# How to modify the OnePlus 5 kernel source for on-device use

The OnePlus 5 kernel source OnePlus provides needs a few modifications to get it to work properly.

* CAF drivers mandate that the kernel be compiled using an out folder. Add `O=out` to all of your make commands (i.e. change all instances of `make` to `make O=out`).

* Since flashing the modules will modify the `/system` partition, dm-verity must be disabled in order to boot. Add the following commit to disable it: [`c0e8841e6f07`](https://github.com/nathanchance/op5/commit/c0e8841e6f073f67f9409bed52af47e83484e9f9) ("dumpling: Disable verity on /system")

* The Wi-Fi driver for this device is not included in the kernel tree so it must be fetched. This process can be used for both adding it initially and updating it.

  1. Run this in the root of your kernel tree:

    ```bash
    for REPO in "fw-api" "qca-wifi-host-cmn" "qcacld-3.0"; do
        rm -rf drivers/staging/${REPO}
        git clone -b LA.UM.6.4.r1-04900-8x98.0 https://source.codeaurora.org/quic/la/platform/vendor/qcom-opensource/wlan/${REPO} drivers/staging/${REPO}
        rm -rf drivers/staging/${REPO}/.git
    done
    ```

  2. Add the following to `drivers/staging/Kconfig` towards the bottom above the `endif # STAGING`: `source "drivers/staging/qcacld-3.0/Kconfig"`

  3. Add the following to `drivers/staging/Makefile` at the bottom of the file: `obj-$(CONFIG_QCA_CLD_WLAN)   += qcacld-3.0/`

  4. Add the following `CONFIG_` options to `msmcortex-perf_defconfig`:

    ```
    CONFIG_QCA_CLD_WLAN=m
    CONFIG_QCACLD_WLAN_LFR3=y
    CONFIG_PRIMA_WLAN_OKC=y
    CONFIG_PRIMA_WLAN_11AC_HIGH_TP=y
    CONFIG_WLAN_FEATURE_11W=y
    CONFIG_WLAN_FEATURE_LPSS=y
    CONFIG_QCOM_VOWIFI_11R=y
    CONFIG_QCACLD_FEATURE_NAN=y
    CONFIG_QCACLD_FEATURE_GREEN_AP=y
    CONFIG_HELIUMPLUS=y
    CONFIG_QCOM_TDLS=y
    CONFIG_QCOM_LTE_COEX=y
    CONFIG_WLAN_OFFLOAD_PACKETS=y
    CONFIG_WLAN_FEATURE_MEMDUMP=y
    CONFIG_WLAN_FASTPATH=y
    CONFIG_WLAN_NAPI=y
    CONFIG_MCC_TO_SCC_SWITCH=y
    CONFIG_QCACLD_WLAN_LFR2=y
    CONFIG_WLAN_FEATURE_DISA=y
    ```

* The generated modules should be stripped as they can be quite large. This would normally be done on `module_install` but we don't run this on Android kernels (because we aren't building on device). Use the strip command from your cross compiler to do this. If you have exported `CROSS_COMPILE`, you can run this one-liner in your kernel tree to strip all modules:
```bash
find ./ -name "*.ko" -exec ${CROSS_COMPILE}strip --strip-unneeded {} \;
```

* The generated modules need to be resigned to avoid triggering `CONFIG_MODULE_SIG_FORCE` or `CONFIG_MODVERSIONS` (neither of these should be disabled). Assuming your out folder from point 1 was `out`, run the following one-liner in your kernel tree to resign all modules:
```bash
find ./ -name "*.ko" -exec out//scripts/sign-file sha512 out/certs/signing_key.pem out/certs/signing_key.x509 {} \;
```

* To flash the kernel and accompanying modules, use [AnyKernel2](https://github.com/osm0sis/AnyKernel2) and [TWRP](https://twrp.me/oneplus/oneplus5.html). The README explains how to properly setup AK2 and an example tree is available in [my fork](https://github.com/nathanchance/AnyKernel2/tree/op5-flash-8.0.0). Use this one-liner in your kernel tree to move all kernel modules to the AnyKernel folder:
```bash
find ./ -name "*.ko" -exec cp {} <anykernel_folder>/modules \;
```
