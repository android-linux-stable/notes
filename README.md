# linux-stable notes

These are markdown pages offering some notes about what linux-stable is, how you should be using it, and issue resolution notes. Please read this whole page if nothing else!


# Index


* `info:` These are pages dedicated to answering what this stuff is and why it is important. Both users and developers should read these! If your kernel developer doesn't care for this process after reading this, they don't care about your security or stability...

* `process:` This section goes over how to get a kernel up to date with linux-stable, step by step, as well as providing helpful tips and tricks.

* `conflict-notes:` These pages document resolutions of all the conflicts during each merge, including why the conflict occurred and how it was resolved.

* `usability-notes:` Some of these trees do not contain everything needed to boot and use the device as normal in their current form. Since these kernels are designed to be used as a base for others or merged into existing working kernels, those commits will not be added. Instead, I give notes that can be used to get everything working properly.

Each subfolder has its own index if you want more details!


# Available trees

Each tree will have both OEM and linux-stable updates merged promptly. The branch the tree is based on will be the same as its name upstream.

* [Essential Phone](https://github.com/android-linux-stable/mata) ([upstream source](https://github.com/LineageOS/android_kernel_essential_msm8998))
* [msm-3.18](https://github.com/android-linux-stable/msm-3.18) ([upstream source](https://source.codeaurora.org/quic/la/kernel/msm-3.18))
* [msm-4.4](https://github.com/android-linux-stable/msm-4.4) ([upstream source](https://source.codeaurora.org/quic/la/kernel/msm-4.4))
* [OnePlus 3 and 3T](https://github.com/android-linux-stable/op3) ([upstream source](https://github.com/OnePlusOSS/android_kernel_oneplus_msm8996))
* [OnePlus 5 and 5T](https://github.com/android-linux-stable/op5) ([upstream source](https://github.com/OnePlusOSS/android_kernel_oneplus_msm8998))
* [Pixel and Pixel XL](https://github.com/android-linux-stable/marlin) ([upstream source](https://android.googlesource.com/kernel/msm/))
* [Pixel 2 and Pixel 2 XL](https://github.com/android-linux-stable/wahoo) ([upstream source](https://android.googlesource.com/kernel/msm/))

The lineage-15.1 branches will not have conflict notes but they generally follow the MSM trees.

If you are a custom kernel or ROM developer with a 3.18 or 4.4 kernel and want linux-stable merged into your repo(s), please let me know on either [Telegram](https://t.me/nathanchance), [Twitter](https://twitter.com/nathanchance), or [XDA](https://forum.xda-developers.com/member.php?u=6842057). I am happy to merge it into your trees and either pull request you or ping you with updates automatically.


## How to use them

These trees can either be merged into an existing tree or they can be used as a starting base.

Should you chose to merge, use the following commands:

```bash
git fetch <repo_url> <branch>
git merge FETCH_HEAD
```

Should you chose to use the kernel as a base for your own, either fork the kernel or run the following in an existing kernel repo:

```bash
git fetch <android-linux-stable_repo_url> <branch_to_use>
git branch -b <your_branch_name> FETCH_HEAD
git push --set-upstream origin <your_branch_name>
```

This will keep commit history and make it easier to keep up with updates.


## Getting updates

You can merge the updates from this organization by using the merge command:

```bash
git fetch <repo_url> <branch>
git merge FETCH_HEAD
```

If you want to do the merges yourself, you can add linux-stable as a remote and merge the tag:

```bash
git remote add linux-stable https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/
git fetch linux-stable
git merge v<version>
```

You can use [the script](https://github.com/android-linux-stable/script) to do this automatically.


# Other notes

Do not ask me permission to use these, they are freely available for a reason. Additionally, you don't need to give me credit for any public releases you do (although it would be appreciated). I'm not in this for glory, I just want people to be more stable and secure. Enjoy!
