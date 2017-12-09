# 4.4.56 to 4.4.102

* `arch/arm64/kernel/armv8_deprecated.c`

  * **Resolution:** Take both sides

  * **Causes:** Commit [`01ce16f40c97`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=01ce16f40c9767c2465fc86b1b54ad11192c6d10) ("arm64: armv8_deprecated: ensure extension of addr") was not expecting commit [`83f01e7ca215`](https://android.googlesource.com/kernel/msm/+/83f01e7ca2150ed9f996319c87e32782b42ce703) ("BACKPORT: arm64: Factor out PAN enabling/disabling into separate uaccess\_\* macros") to be present. Resulting diff is equivalent with both linux-stable and mainline.


* `arch/arm64/kernel/entry.S`

  * **Resolution:** Take both sides (make final diff match upstream's)

  * **Causes:** Commit [`e946579e4bfd`](https://android.googlesource.com/kernel/msm/+/e946579e4bfdb5985f6d0d1450dbe6495a8319c8) ("BACKPORT: arm64: Disable TTBR0_EL1 during normal kernel execution") added an include, which was not expected by commit [`3ccf69562ac2`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=3ccf69562ac2ae701e274b30ac36165d15128ac6) ("arm64: entry: improve data abort handling of tagged pointers")


* `arch/arm64/kernel/hw_breakpoint.c`

  * **Resolution:** Take mainline version

  * **Causes:** Commit [`4eaef3651815`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=4eaef365181564203f4f9fb8fb576c89481cca12) ("arm64: hw_breakpoint: fix watchpoint matching for tagged pointers") was reworked for 4.4 because it doesn't have commit [`fdfeff0f9e3d`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=fdfeff0f9e3d9be2b68fa02566017ffc581ae17b) ("arm64: hw_breakpoint: Handle inexact watchpoint addresses"). However, the Pixel 2 tree does, as commit [`6bd71c8c03d1`](https://android.googlesource.com/kernel/msm/+/6bd71c8c03d1e4838bf34598307ec314923b08dc) ("BACKPORT: arm64: hw_breakpoint: Handle inexact watchpoint addresses"). Thus, we can use the upstream commit [`7dcd9dd8cebe`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=7dcd9dd8cebe9fa626af7e2358d03a37041a70fb) ("arm64: hw_breakpoint: fix watchpoint matching for tagged pointers") for proper resolution.


* `drivers/android/binder.c`

  * **Resolution:** Take left side (discard all changes)

  * **Causes:**

    * Commit [`596b97ec2e5e`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=596b97ec2e5e24c966b9cb4aa9a9766e53ecdd43) ("binder: use group leader instead of open thread") is already present as commit [`9036bcc59e36`](https://android.googlesource.com/kernel/msm/+/9036bcc59e36952da230f31187b1ab2f866ebfae) ("binder: use group leader instead of open thread") and commit [`359795138dc5`](https://android.googlesource.com/kernel/msm/+/359795138dc5440e09c58025e28ec1b38d648c09) ("binder: use group leader instead of open thread") and there have been other changes to this section since then.

    * Commit [`1792d6c17cb2`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=1792d6c17cb282fd8e5cd197a8b33cb78484eb6a) ("binder: Use wake up hint for synchronous transactions.") is already present as commit [`0cebb407b2f`](https://android.googlesource.com/kernel/msm/+/0cebb407b2f431d748d9cc85cf7e4232a9223342) ("FROMLIST: binder: Use wake up hint for synchronous transactions.") and commit [`3956eabb34de`](https://android.googlesource.com/kernel/msm/+/3956eabb34de6b24bdbe90013c7567867bb139ea) ("android: binder: Use wake up hint for synchronous transactions.") and there have been other changes to this section since then.

    * Commit [`9dac44d5d4b0`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=9dac44d5d4b0a7fffe04ad505e0a082e900ad767) ("ANDROID: binder: fix proc->tsk check.") was included as part of commit [`9036bcc59e36`](https://android.googlesource.com/kernel/msm/+/9036bcc59e36952da230f31187b1ab2f866ebfae) ("binder: use group leader instead of open thread").


* `drivers/gpu/drm/msm/adreno/adreno_gpu.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`b54e58ccceb7`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=b54e58ccceb794176b37037e76df3a7ed876b360) ("drm/msm: Ensure that the hardware write pointer is valid") is already present as commit [`7d080736a4b4`](https://android.googlesource.com/kernel/msm/+/7d080736a4b4601a16a2d81a4537d0202fc05157) ("drm/msm: Make sure that WPTR stays in bounds") and there have been other changes to this section since then.


* `drivers/gpu/drm/msm/msm_gem_submit.c`

  * **Resolution:** Take both sides (make final diff match upstream's)

  * **Cause:** Commit [`031b02bc16ae`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=031b02bc16aeeb34c8038026cbbca1e6430c9d75) ("drm/msm: Fix potential buffer overflow issue") had to be adapted to work around the changed parameter (`struct msm_gem_address_space *aspac` instead of `struct msm_gpu *gpu`) that was introducted in commit [`231c57eeaf8e`](https://android.googlesource.com/kernel/msm/+/231c57eeaf8e10ec2a4510ffc98382ef1d7513ed) ("drm/msm: Pass the MMU domain index in struct msm_file_private").


* `drivers/gpu/drm/msm/msm_ringbuffer.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** The power of 2 alignment check in commit [`b54e58ccceb7`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=b54e58ccceb794176b37037e76df3a7ed876b360) ("drm/msm: Ensure that the hardware write pointer is valid") is already present in commit [`378583458fa1`](https://android.googlesource.com/kernel/msm/+/378583458fa167277b15d145dccce253459393ec) ("drm/msm: Add support for multiple ringbuffers") and there have been other changes to this section since then.


* `drivers/mmc/host/sdhci.c`

  * **Resolution:** Take left side (discard all changes)

  * **Causes:** Commit [`81dd76ac077b`](https://android.googlesource.com/kernel/msm/+/81dd76ac077bdbc120ddb05ea9a27bc2ae8d7796) ("mmc: sdhci: Poll for register status much tightly") changed this same area and appears to resolve the same issue that commit [`74b4a5b7cf03`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=74b4a5b7cf03ff2d3ef9fab55b0e65588c00dd45) ("Revert some commits for cleaner 4.4.102 merge") does. However, because this wasn't a clearly equivalent swap, the platform change was taken over the upstream fix to avoid any regressions.


* `drivers/net/wireless/ath/ath10k/core.c`

  * **Resolution:** Take both sides (make final diff match upstream's)

  * **Cause:** Commit [`2c65494080c9`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=2c65494080c900c8a0aa4a865b57a8001960ff26) ("ath10k: fix memory leak in rx ring buffer allocation") did not account for commit [`9eaeb4e0974b`](https://android.googlesource.com/kernel/msm/+/9eaeb4e0974b976a037b7c55f0fe409bccbb7fdd) ("ath10k: fix spurious tx/rx during boot"), which was added by CAF to 4.4 (since it didn't appear upstream until v4.8-rc2).


* `drivers/net/wireless/ath/ath10k/pci.c`

  * **Resolution:** Take both sides (make final diff match upstream's)

  * **Causes:** Commit [`483b1c69655d`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=483b1c69655d61a4c15648cf96011cfb20aa2000) ("ath10k: override CE5 config for QCA9377") did not expect the location of the `if (QCA_REV_6174(ar))` statement to be moved by commit [`85541146968a`](https://android.googlesource.com/kernel/msm/+/85541146968a4753e28c6192948007960c46c36f) ("ath10k: pull reusable code from pci probe and remove for ahb").


* `drivers/net/wireless/iwlwifi/iwl-nvm-parse.c`

  * **Resolution:** Take both sides (use mainline version)

  * **Causes:** Commit [`fc29713fa7c7`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=fc29713fa7c78fda30855444eeab2d5ea8088762) ("iwlwifi: add workaround to disable wide channels in 5GHz") was backported, ignoring the changes from commit [`57fbcce37be7`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=57fbcce37be7c1d2622b56587c10ade00e96afa3) ("cfg80211: remove enum ieee80211_band"). However, the Pixel 2 tree as it as commit [`56f601d6bb9e`](https://android.googlesource.com/kernel/msm/+/56f601d6bb9e51c3c8a79a5f40878b8d1e6ff481) ("BACKPORT: cfg80211: remove enum ieee80211_band") so we can use mainline commit [`01a9c948a093`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=01a9c948a09348950515bf2abb6113ed83e696d8) ("iwlwifi: add workaround to disable wide channels in 5GHz").


* `drivers/regulator/core.c`

  * **Resolution:** Take left side (discard all changes)

  * **Causes:** Commit [`f9157b4ed20e`](https://android.googlesource.com/kernel/msm/+/f9157b4ed20e81a86d6316bff5c666b76ae6f1a0) ("Revert "regulator: Enable supply regulator if child rail is enabled."") removed the section changed by commit [`3e19487b9bf5`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=3e19487b9bf5076dcc2cd79da3dbd57b94d4e6b7) ("regulator: core: Clear the supply pointer if enabling fails"). Since the upstream commit doesn't appear to fix the issue described by the CAF commit, discard the change.


* `drivers/scsi/sd.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Causes:** Commit [`7e83faf32824`](https://android.googlesource.com/kernel/msm/+/7e83faf32824cba959a710abcc13daeb0b673a86) ("Revert "sd: Fix rw_max for devices that report an optimal xfer size"") removed the curly brace before the `else` statement, which was expected in the diff of commit [`448961955592`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=448961955592c46f1490fb6ca8d3e52ce17e6222) ("scsi: sd: Consider max_xfer_blocks if opt_xfer_blocks is unusable")


* `drivers/scsi/sg.c`

  * **Resolution:** Take both sides (leave mutex in place)

  * **Causes:** Commit [`82e2e0f9914d`](https://android.googlesource.com/kernel/msm/+/82e2e0f9914df19d910d3d249a12d416090a6802) ("Prevent potential double frees in sg driver") introduced a mutex, which commit [`a4075bbb67b9`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=a4075bbb67b9562b9599affc6fb38f04bd7073ff) ("scsi: sg: protect accesses to 'reserved' page array") did not expect.


* `drivers/scsi/ufs/ufshcd.h`

  * **Solution:** Take left side (discard all changes)

  * **Cause:** Commit [`0c098158785b`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=0c098158785b5c8091c0bae3aa505060414076cc) ("scsi: ufs: add capability to keep auto bkops always enabled") is already present as commit [`9f06dddf5bee`](https://android.googlesource.com/kernel/msm/+/9f06dddf5beecbcdf36535e0e587c23aaa7785f5) ("scsi: ufs: add capability to keep auto bkops always enabled") with a different shift value.


* `drivers/staging/android/ion/ion.c`

  * **Resolution:** Take left side (discard all changes)

  * **Causes:** Commit [`a7544fdd1626`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=a7544fdd1626b65db635022c9d36007bb32dd6d8) ("staging/android/ion : fix a race condition in the ion driver") is already present as commit [`cf229da50854`](https://android.googlesource.com/kernel/msm/+/cf229da5085451839eae40e5dc94164c74ae5b3a) ("staging/android/ion : fix a race condition in the ion driver") and there have been other changes to this file since then.


* `drivers/usb/gadget/function/f_fs.c`

  * **Resolution:** Take left side (discard all changes)

  * **Causes:**

    * It appears commit [`4a1a3bb70fb4`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=4a1a3bb70fb4255a9f6052eb86db1ff2140255a6) ("usb: gadget: function: f_fs: pass companion descriptor along") was omitted in the CAF merge up to 4.4.55 in commit [`a4b9c109c2f9`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=a4b9c109c2f9143790c1d1a96475eecf7338713a) ("Merge tag v4.4.55 into branch 'msm-4.4'"). I assume this was done for a reason so the follow up fix in commit [`889caad4fbe4`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=889caad4fbe49e3a612ccb971e40c50912f90ace) ("usb: gadget: f_fs: avoid out of bounds access on comp_desc") is not needed.

    * The issue described by commit [`1e0f216195a6`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=1e0f216195a6d106ed50c386abffdf60f496d518) ("usb: gadget: f_fs: Fix possibe deadlock") is already fixed by commit [`dfe8b29ad1df`](https://android.googlesource.com/kernel/msm/+/dfe8b29ad1dfb84411c3c897a619b44c4cbf8905) ("usb: gadget: f_fs: Unlock mutex before unregistering gadget"). While the latter is much uglier than the former, there has been some minor code churn around that section since then so to avoid more conflicts from the CAF side of things, ignore this conflict as well.


* `fs/ext4/crypto_key.c`

  * **Resolution:** Take left side (discard conflicting changes)

  * **Causes:** Commit [`7a5202190810`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=7a5202190810dde1467718235c1f650fcf57592a) ("fscrypt: remove broken support for detecting keyring key revocation") is already present as commit [`8afa82212a86`](https://android.googlesource.com/kernel/msm/+/8afa82212a862d54386327710ef1ccd8c0d51263) ("fscrypt: remove broken support for detecting keyring key revocation") but git couldn't tell because of commit [`a8059e6d39ec`](https://android.googlesource.com/kernel/msm/+/a8059e6d39ecfab6c90abc8a7502652907cdf258) ("ext4 crypto: enable HW based encryption with ICE").


* `fs/ext4/ext4.h`

  * **Resolution:** Take left side (discard all changes)

  * **Causes:**

    * Commit [`7a5202190810`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=7a5202190810dde1467718235c1f650fcf57592a) ("fscrypt: remove broken support for detecting keyring key revocation") is already present as commit [`8afa82212a86`](https://android.googlesource.com/kernel/msm/+/8afa82212a862d54386327710ef1ccd8c0d51263) ("fscrypt: remove broken support for detecting keyring key revocation") but git couldn't tell due to the functions added by commit [`a8059e6d39ec`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=a8059e6d39ecfab6c90abc8a7502652907cdf258) ("ext4 crypto: enable HW based encryption with ICE").


* `fs/ext4/page-io.c`

  * **Resolution:** Take left side (discard all changes)

  * **Causes:** Commit [`0a76f023e6f2`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=0a76f023e6f2073936cc87ff839b2aaeccc4fb9a) ("ext4 crypto: don't let data integrity writebacks fail with ENOMEM") is already present as commit [`4dfa31b4af7e`](https://android.googlesource.com/kernel/msm/+/4dfa31b4af7e936832f657b18fd9f64eb26ed09d) ("ext4 crypto: don't let data integrity writebacks fail with ENOMEM") but git couldn't tell due to changes from commit [`a8059e6d39ec`](https://android.googlesource.com/kernel/msm/+/a8059e6d39ecfab6c90abc8a7502652907cdf258) ("ext4 crypto: enable HW based encryption with ICE").


* `fs/ext4/readpage.c`

  * **Resolution:** Take left side (discard all changes)

  * **Causes:** Commit [`0a76f023e6f2`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=0a76f023e6f2073936cc87ff839b2aaeccc4fb9a) ("ext4 crypto: don't let data integrity writebacks fail with ENOMEM") is already present as commit [`4dfa31b4af7e`](https://android.googlesource.com/kernel/msm/+/4dfa31b4af7e936832f657b18fd9f64eb26ed09d) ("ext4 crypto: don't let data integrity writebacks fail with ENOMEM") but git couldn't tell due to changes from commit [`d6567feb8f2b`](https://android.googlesource.com/kernel/msm/+/d6567feb8f2b6e479ec1a14aa6d04fdddd9b1092) ("ext4: don't allow ICE encryption on ICE-less block devices").


* `fs/f2fs/crypto_key.c`

  * **Resolution:** Take right side

  * **Causes:** Commit [`7a5202190810`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=7a5202190810dde1467718235c1f650fcf57592a) ("fscrypt: remove broken support for detecting keyring key revocation") is already present as commit [`8afa82212a86`](https://android.googlesource.com/kernel/msm/+/8afa82212a862d54386327710ef1ccd8c0d51263) ("fscrypt: remove broken support for detecting keyring key revocation"), which causes git to fail to generate a proper diff from commit [`7a5202190810`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=7a5202190810dde1467718235c1f650fcf57592a) ("fscrypt: remove broken support for detecting keyring key revocation") to commit [`1dda04c761ab`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=1dda04c761abf006402f7f5e9adb11f9044731c8) ("fscrypt: fix dereference of NULL user_key_payload").


* `fs/pstore/ram.c`

  * **Resolution:** Take both sides

  * **Causes:** Commit [`aca5b1e3c5b7`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=aca5b1e3c5b7e73f20b686ca712cb4cf9fccb219) ("pstore: Allow prz to control need for locking") conflicts with commit [`b71d012395a4`](https://android.googlesource.com/kernel/msm/+/b71d012395a42ae6b58f36f5eaf460a9ff29e31a) ("fs/pstore/ramoops: add alternate encrypted buffer support") due to the added `*alt_paddr` parameter.


* `fs/pstore/ram_core.c`

  * **Resolution:** Take left side

  * **Causes:** Commit [`9ece74e1006e`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=9ece74e1006e1706a7c239fd158f93f126c04c2e) ("pstore: Correctly initialize spinlock and flags") conflicts with commit [`b71d012395a4`](https://android.googlesource.com/kernel/msm/+/b71d012395a42ae6b58f36f5eaf460a9ff29e31a) ("fs/pstore/ramoops: add alternate encrypted buffer support")


* `kernel/power/process.c`

  * **Resolution:** Take both sides

  * **Cause:** Commit [`57caa2ad5ce3`](https://android.googlesource.com/kernel/msm/+/57caa2ad5ce35bedb7ab374a2e5b4d7adf63da2b) ("power: Adds functionality to log the last suspend abort reason.") added an include, which was not expected by commit [`90fd6738731b`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=90fd6738731b6d105fc8f04832ae17a9ac82c05c) ("sched/cpuset/pm: Fix cpuset vs. suspend-resume bugs").


* `kernel/sched/sched.h`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** Commit [`62208707b466`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=62208707b466cc3c6ce951a7c4b7b4bb9b9192f6) ("sched/cputime: Fix prev steal time accouting during CPU hotplug") conflicts with both commit [`a2944ff05e77`](https://android.googlesource.com/kernel/msm/+/a2944ff05e7789f07a1f92164a697057d9613ef8) ("ANDROID: sched: avoid scheduling RT threads on cores currently handling softirqs") and commit [`87c4c5d01bb0`](https://android.googlesource.com/kernel/msm/+/87c4c5d01bb0d9414bb4a43f0631abf2b004c1d8) ("sched: backport cpufreq hooks from 4.9-rc4"), as they add functions above and below the removed section respectively.


* `kernel/sysctl.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Causes:** Commit [`9cc5c789d91e`](https://android.googlesource.com/kernel/msm/+/9cc5c789d91e4174298c38cb5c7acafc5910a95d) ("Merge remote-tracking branch 'msm4.4/tmp-da9a92f' into msm-4.4") omitted the sysctl changes from commit [`fa6d0ba12a8e`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=fa6d0ba12a8eb6a2e9a1646c5816da307c1f93a7) ("pipe: limit the per-user amount of pages allocated in pipes"), causing a conflict with commit [`c50fd34e1089`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=c50fd34e10897114a7be2120133bd7e0b4184024) ("mnt: Add a per mount namespace limit on the number of mounts").


* `mm/mempool.c`

  * **Resolution:** Take left side (discard all changes)

  * **Causes:** Commit [`d45aabadbcb9`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=d45aabadbcb967d3b01451732f65da9ff7315450) ("mm/mempool: avoid KASAN marking mempool poison checks as use-after-free") is already present as commit [`42b909889a93`](https://android.googlesource.com/kernel/msm/+/42b909889a9337559417a24fc597010a904ece03) ("mm/mempool: avoid KASAN marking mempool poison checks as use-after-free") but git couldn't tell due to changes from commit [`13d2da8a5178`](https://android.googlesource.com/kernel/msm/+/13d2da8a5178820c49e73cc71f5470a064ae1268) ("mm, kasan: add GFP flags to KASAN API").


* `net/wireless/nl80211.c`

  * **Resolution:** Take left side

  * **Cause:** Commit [`6a6c61d8467d`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=6a6c61d8467d2dd7059b7d52773c18f8122e4f68) ("nl80211: Define policy for packet pattern attributes") did not account for commit [`3fee1ede34a6`](https://android.googlesource.com/kernel/msm/+/3fee1ede34a6c3b2dd7d816643e887c2308f6a78) ("nl80211: add feature for BSS selection support") being present.


* `sound/usb/card.c`

  * **Resolution:** Take right side (shuffle resolution)

  * **Cause:** Commit [`2ecedf5dc75b`](https://android.googlesource.com/kernel/msm/+/2ecedf5dc75bc770ec09bd2238e798063aeafc4b) ("sound: usb: Add support for parsing AudioStreaming intf for BADD devices") shuffled the function `snd_usb_create_streams`, which commit [`46c7b1fa4911`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=46c7b1fa4911a859a82575e3ffb55b34a89a222d) ("ALSA: usb-audio: Check out-of-bounds access by corrupted buffer descriptor") did not expect. Resolution is identical but has been moved into the `switch` statement to satisfy the changes made by CAF's shuffling.


# 4.4.104

* `drivers/mmc/core/bus.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`5c65b739389f`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=5c65b739389fbc353fb42d379e9b7379cfe6d3f6) ("mmc: core: Do not leave the block driver in a suspended state") was already resolved by [`192cfe16ca57`](https://android.googlesource.com/kernel/msm/+/192cfe16ca5761bb7a5aafc016e79a21b2bd4002) ("mmc: bus: Handle error in case bus_ops suspend fails") but the latter has an extra comment block so git could not tell the fix was already present.
