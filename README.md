# linux-stable notes

These are markdown pages offering some notes about what linux-stable is, how you should be using it, and issue resolution notes.


# Index

## Information about linux-stable (for both users and developers)

These are pages dedicated to answering what this stuff is and why it is important. Everyone should read these! If your kernel developer doesn't care for this process after reading this, they don't care about your security or stability...

- [`info/what-is-linux-stable.md`](info/what-is-linux-stable.md) gives an overview of what linux-stable is and how it came about.
- [`info/why-is-linux-stable-important.md`](info/why-is-linux-stable-important.md) gives some reasons why this is important and addresses some of the excuses that people give for not caring about it (when they definitely should).


## How to update your kernel with linux-stable

- [`process/how-to.md`](process/how-to.md) goes over the proper process for adding the latest linux-stable into your kernel.
- [`process/tips-and-tricks.md`](process/tips-and-tricks.md) contains a few pointers and hints regarding this process.


## Conflict resolution notes

These are notes for developers to help with merging linux-stable into their own repos by documenting all of the conflicts, where they come from, and what was done to solve them. These repos are up to date with the latest linux-stable along with the latest commits from their OEMs. The name of the file is the branch that the conflicts were fixed on. A new branch will be created when the upstream source adds a new one. New tags/updates will be merged into the branches when they appear on the upstream remote.

- [`conflict-notes/msm-4.4`](conflict-notes/msm-4.4) for [the msm-4.4 repository](https://github.com/android-linux-stable/msm-4.4) (stock CAF 4.4 source, currently based on the [kernel.lnx.4.4.r18-rel](https://source.codeaurora.org/quic/la/kernel/msm-4.4/log/?h=kernel.lnx.4.4.r18-rel) branch).

- [`conflict-notes/op5`](conflict-notes/op5) for [the op5 repository](https://github.com/android-linux-stable/op5) (stock OP5 source, currently based on the [OOS Open Beta 1](https://github.com/OnePlusOSS/android_kernel_oneplus_msm8998/commits/oneplus/QC8998_O_8.0) branch).

- [`conflict-notes/wahoo`](conflict-notes/wahoo) for [the wahoo repository](https://github.com/android-linux-stable/wahoo) (stock Pixel 2 (XL) source, currently based on the [android-msm-wahoo-4.4-oreo-dr1](https://android.googlesource.com/kernel/msm/+log/android-msm-wahoo-4.4-oreo-dr1) branch).


## Usability notes

These kernels do not contain everything needed to boot and use the device as normal in their current form. Since these kernels are designed to be used as a base for others or merged into existing working kernels, those commits will not be added. Instead, I give notes that can be used to get everything working properly.

- [`usability-notes/wahoo.md`](usability-notes/wahoo.md) for using the Pixel 2 and Pixel 2 XL kernel source
- [`usability-notes/op5.md`](usability-notes/op5.md) for using the OnePlus 5 kernel source

Should you chose to merge, use the following commands:

```bash
git fetch <repo_url> <branch>
git merge FETCH_HEAD
```

Should you chose to use the kernel as a base for your own, either fork the kernel or run the following in an existing kernel repo:

```bash
git fetch <repo_url> <branch>
git branch -b <branch_name> FETCH_HEAD
git push --set-upstream origin <branch_name>
```

This will keep commit history and make it easier to keep up with updates. You can either merge the updates from this tree by using the merge commands above or add linux stable as a remote and merge changes from there:

```bash
git remote add linux-stable https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/
git fetch linux-stable
git merge v<version>
```


# Other notes

Do not ask me permission to use these, they are freely available for a reason. Additionally, you don't need to give me credit for any public releases you do (although it would be appreciated). I'm not in this for glory, I just want people to be more stable and secure. Enjoy!
