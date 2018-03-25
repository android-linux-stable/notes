# 4.4.88 to 4.4.105

* `drivers/gpu/drm/msm/msm_gem_submit.c`

  * **Resolution:** Take both sides (make final diff match upstream's)

  * **Cause:** Commit [`031b02bc16ae`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=031b02bc16aeeb34c8038026cbbca1e6430c9d75) ("drm/msm: Fix potential buffer overflow issue") had to be adapted to work around the changed parameter (`struct msm_gem_address_space *aspac` instead of `struct msm_gpu *gpu`) that was introducted in commit [`231c57eeaf8e`](https://android.googlesource.com/kernel/msm/+/231c57eeaf8e10ec2a4510ffc98382ef1d7513ed) ("drm/msm: Pass the MMU domain index in struct msm_file_private").


* `drivers/media/v4l2-core/v4l2-compat-ioctl32.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`93ff127ef6c7`](https://android.googlesource.com/kernel/msm/+/93ff127ef6c7a2a120f7ed843c292b3cd5dca1c2) ("v4l2: Refactor, fix security bug in compat ioctl32") rewrote the `put_user` statements with a `convert_in_user` macro, which was unexpected by commit [`04affe4e1171`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=04affe4e117169e75c4ff1f12dd30d74c9a629fc) ("media: v4l2-compat-ioctl32: Fix timespec conversion"). The former fixes the issue described by the latter (as they are by the same author).


* `drivers/mmc/core/bus.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Commit [`5c65b739389f`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=5c65b739389fbc353fb42d379e9b7379cfe6d3f6) ("mmc: core: Do not leave the block driver in a suspended state") was already resolved by [`192cfe16ca57`](https://android.googlesource.com/kernel/msm/+/192cfe16ca5761bb7a5aafc016e79a21b2bd4002) ("mmc: bus: Handle error in case bus_ops suspend fails") but the latter has an extra comment block so git could not tell the fix was already present.


* `drivers/net/wireless/iwlwifi/iwl-nvm-parse.c`

  * **Resolution:** Take both sides (use mainline version)

  * **Causes:** Commit [`fc29713fa7c7`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=fc29713fa7c78fda30855444eeab2d5ea8088762) ("iwlwifi: add workaround to disable wide channels in 5GHz") was backported, ignoring the changes from commit [`57fbcce37be7`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=57fbcce37be7c1d2622b56587c10ade00e96afa3) ("cfg80211: remove enum ieee80211_band"). However, the Pixel 2 tree as it as commit [`56f601d6bb9e`](https://android.googlesource.com/kernel/msm/+/56f601d6bb9e51c3c8a79a5f40878b8d1e6ff481) ("BACKPORT: cfg80211: remove enum ieee80211_band") so we can use mainline commit [`01a9c948a093`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=01a9c948a09348950515bf2abb6113ed83e696d8) ("iwlwifi: add workaround to disable wide channels in 5GHz").


* `drivers/scsi/ufs/ufshcd.h`

  * **Solution:** Take left side (discard all changes)

  * **Cause:** Commit [`0c098158785b`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=0c098158785b5c8091c0bae3aa505060414076cc) ("scsi: ufs: add capability to keep auto bkops always enabled") is already present as commit [`9f06dddf5bee`](https://android.googlesource.com/kernel/msm/+/9f06dddf5beecbcdf36535e0e587c23aaa7785f5) ("scsi: ufs: add capability to keep auto bkops always enabled") with a different shift value.


* `kernel/power/process.c`

  * **Resolution:** Take both sides

  * **Cause:** Commit [`57caa2ad5ce3`](https://android.googlesource.com/kernel/msm/+/57caa2ad5ce35bedb7ab374a2e5b4d7adf63da2b) ("power: Adds functionality to log the last suspend abort reason.") added an include, which was not expected by commit [`90fd6738731b`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=90fd6738731b6d105fc8f04832ae17a9ac82c05c) ("sched/cpuset/pm: Fix cpuset vs. suspend-resume bugs").


* `net/wireless/nl80211.c`

  * **Resolution:** Take left side (discard conflict)

  * **Cause:** Commit [`6a6c61d8467d`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=6a6c61d8467d2dd7059b7d52773c18f8122e4f68) ("nl80211: Define policy for packet pattern attributes") did not account for commit [`3fee1ede34a6`](https://android.googlesource.com/kernel/msm/+/3fee1ede34a6c3b2dd7d816643e887c2308f6a78) ("nl80211: add feature for BSS selection support") being present.


* `sound/usb/card.c`

  * **Resolution:** Take right side (shuffle resolution)

  * **Cause:** Commit [`2ecedf5dc75b`](https://android.googlesource.com/kernel/msm/+/2ecedf5dc75bc770ec09bd2238e798063aeafc4b) ("sound: usb: Add support for parsing AudioStreaming intf for BADD devices") shuffled the function `snd_usb_create_streams`, which commit [`46c7b1fa4911`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=46c7b1fa4911a859a82575e3ffb55b34a89a222d) ("ALSA: usb-audio: Check out-of-bounds access by corrupted buffer descriptor") did not expect. Resolution is identical but has been moved into the `switch` statement to satisfy the changes made by CAF's shuffling.


# 4.4.106

* `arch/arm/include/asm/kvm_arm.h`

  * **Resolution:** Take right side (use mainline diff)

  * **Cause:** When mainline commit [`5553b142be11`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=5553b142be11e794ebc0805950b2e8313f93d718) ("arm: KVM: Fix VTTBR_BADDR_MASK BUG_ON off-by-one") was backported as commit [`a5fa9efe4e01`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=a5fa9efe4e019e1f8f213142836c84f010cc4faf) ("arm: KVM: Fix VTTBR_BADDR_MASK BUG_ON off-by-one") in the 4.4 tree, it did not expect mainline commit [`8420dcd37ef3`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=8420dcd37ef34040c8fc5a27bf66887b3b2faf80) ("arm: KVM: Make kvm_arm.h friendly to assembly code") to be here, as it was introduced in 4.5. However, it is as commit [`516f3f777e5f`](https://android.googlesource.com/kernel/msm/+/516f3f777e5fb0710f1626c79e3dacca751b8c30) ("arm: KVM: Make kvm_arm.h friendly to assembly code") so we can just use mainline's version.


# 4.4.109

* `net/ipv4/raw.c`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** When mainline commit [`8f659a03a0ba`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=8f659a03a0ba9289b9aeb9b4470e6fb263d6f483) ("net: ipv4: fix for a race condition in raw_sendmsg") was backported to the 4.4 stable tree as commit [`be27b620a861`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=be27b620a861dc2a143b78e81e23f5622d9105da), it was slightly changed because mainline commit [`e2d118a1cb5e`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=e2d118a1cb5e60d077131a09db1d81b90a5295fe) ("net: inet: Support UID-based routing in IP protocols.") is not present in the stable 4.4 tree. However, it is in this one since Google added it as a backport in commit [`b8ebf03fc6a9`](https://android.googlesource.com/kernel/msm/+/b8ebf03fc6a9cee79cb71a2921953425fdee8e97) ("net: inet: Support UID-based routing in IP protocols.") so adjust the diff to account for this (final diff matches both the stable and mainline commit).


# 4.4.110

* `kernel/fork.c`

  * **Resolution:** Modified right side (adjust context)

  * **Cause:** The changes to `kernel/fork.c` (viewable by running `git log v4.4.109..v4.4.110 kernel/fork.c`) had to be adjusted for Google's addition of commit [`059eb79ae99a`](https://android.googlesource.com/kernel/msm/+/059eb79ae99a798c2d7424e763d4e1ef335fa4db) ("UPSTREAM: Clarify naming of thread info/stack allocators"). Final diff matches what was merged into Google's 4.4 kernel/common branch by Greg Kroah-Hartman.


# 4.4.112

* `drivers/md/dm-bufio.c`

  * **Resolution:** Take right side (make final diff match upstream's with one note below)

  * **Cause:** When mainline commit [`fbc7c07ec23c`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=fbc7c07ec23c040179384a1f16b62b6030eb6bdd) ("dm bufio: fix shrinker scans when (nr_to_scan < retain_target)") was backported to the 4.4 tree as commit [`cbb1cc722aaa`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=cbb1cc722aaa9f55b6fa3f8f9be7635652ddc2ae) ("dm bufio: fix shrinker scans when (nr_to_scan < retain_target)"), it was modified to work around the absence of mainline commit [`d12067f428c0`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=d12067f428c037b4575aaeb2be00847fc214c24a) ("dm bufio: don't take the lock in dm_bufio_shrink_count"). However, it is present in this tree as commit [`e3c2e858b996`](https://android.googlesource.com/kernel/msm/+/e3c2e858b996e0c1d9bc3e3702c7160ec5385215) ("BACKPORT: dm bufio: don't take the lock in dm_bufio_shrink_count"). Take the mainline diff and modify it to use ACCESS_ONCE instead of READ_ONCE due to lack of mainline commit [`6aa7de059173`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=6aa7de059173a986114ac43b8f50b297a86f09a8) ("locking/atomics: COCCINELLE/treewide: Convert trivial ACCESS_ONCE() patterns to READ_ONCE()/WRITE_ONCE()").


# 4.4.113

* `arch/x86/include/asm/thread_info.h`

  * **Resolution:** Take right side (make final diff match upstream's)

  * **Cause:** The addition of commit [`fdb92b0de361`](https://android.googlesource.com/kernel/msm/+/fdb92b0de361f9043f359a1de52e2bedd9da4599) ("mm: Implement stack frame object validation") prevented git from cleanly applying stable commit [`cfc8c1d61e46`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=cfc8c1d61e46fd3c60a34a5b1962eeeb03222a3d) ("x86/asm: Use register variable to get stack pointer value").


# 4.4.115

* `drivers/usb/gadget/function/f_fs.c`

  * **Resolution:** Take left side (discard all changes)

  * **Cause:** Stable commit [`68b43caf4a4b`](https://android.googlesource.com/kernel/msm/+/68b43caf4a4b98256bdb67dba025f858bdf21725) ("usb: f_fs: Prevent gadget unbind if it is already unbound") is already present as commit [`35fdb9cd7e90`](https://source.codeaurora.org/quic/la/kernel/msm-4.4/commit/?id=35fdb9cd7e90c08ac9697fa330e4e290b9d34f8a) ("usb: f_fs: Prevent gadget unbind if it is already unbound") with a slightly different resolution so it could not be cleanly resolved.


# 4.4.118

  * `net/Kconfig`

    * **Resolution:** Take both sides (make final diff match upstream's)

    * **Cause:** Stable commit [`d365b297433c`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=d365b297433cf2969fa94f243d7afddc073c7bf1) ("net: add dst_cache support") was not expecting the change to this file from commit [`016c030cc678`](https://android.googlesource.com/kernel/msm/+/016c030cc67882b2143fc8098afa471c8bf33bdf) ("net: ipc_router: Add snapshot of IPC Router") to be present.

  * `net/core/Makefile`

    * **Resolution:** Take both sides (make final diff match upstream's)

    * **Cause:** Stable commit [`d365b297433c`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=d365b297433cf2969fa94f243d7afddc073c7bf1) ("net: add dst_cache support") was not expecting the change to this file from commit [`274f3cfdd0a0`](https://android.googlesource.com/kernel/msm/+/274f3cfdd0a0a14a73b510405cc6fc91abee74e0) ("net: sockev: Initial Commit") to be present.


# 4.4.124

* `drivers/gpu/drm/msm/msm_gem.c`

  * **Resolution:** Take both sides (make final diff match upstream's)

  * **Cause:** Commit [`a808f9895c87`](https://android.googlesource.com/kernel/msm/+/a808f9895c87773833650271eb7c5281fbc0d8ff) ("drm/msm: Use dma_sync_sg_for_device() to flush cache for new buffers") changed one of the sections modified by stable commit [`c1b1c1af967a`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=c1b1c1af967a84e986a9e893b4eebf6f7a40045c) ("drm/msm: fix leak in failed get_pages"), requiring a slight context change.


# 4.4.125

* `arch/arm64/mm/mmu.c`

  * **Resolution:** Take both sides (make final diff match upstream's)

  * **Cause:** The backport of mainline commit [`b6bdb7517c3d`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=b6bdb7517c3d3f41f20e5c2948d6bc3f8897394e) ("mm/vmalloc: add interfaces to free unmapped page table"), stable commit [`31895cfd7956`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=31895cfd79564111cdd5a9f48c5d491ae26a238e) ("mm/vmalloc: add interfaces to free unmapped page table"), was not expecting commit [`324420bf91f6`](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/commit/?id=324420bf91f60582bb481133db9547111768ef17) ("arm64: add support for ioremap() block mappings") to be present; however, it is in this tree as commit [`37cbc7db8e4f`](https://android.googlesource.com/kernel/msm/+/37cbc7db8e4fa9b66e15cf8661383a6b51c9a3e7) ("arm64: add support for ioremap() block mappings") so adjust the context to match mainline's version.
