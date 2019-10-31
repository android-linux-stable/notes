# linux-stable notes

These are markdown pages offering some notes about what linux-stable is, how you should be using it, and issue resolution notes. Please read this whole page if nothing else!

TL;DR: linux-stable is important for stability and security. If you are a custom kernel or ROM developer with a 3.18 or 4.4 kernel and want linux-stable merged into your repo(s), you can either use these trees as a base or merge them into your own. If you have neither the time nor the confidence to get it right, please let me know via one of the methods below. I am happy to merge it into your trees and either pull request you or ping you with updates automatically.


# Index

* `info:` These are pages dedicated to answering what this stuff is and why it is important. Both users and developers should read these! If your kernel developer doesn't care for this process after reading this, they don't care about your security or stability...

* `process:` This section goes over how to get a kernel up to date with linux-stable, step by step, as well as providing helpful tips and tricks.

* `trees:` This section includes notes on each tree, including what phone it is for, the upstream repo, and the currently supported branches.

* `conflict-notes:` These pages document the conflicts during each merge (why the conflict occurred and how it was resolved). Please note, not all devices will have these as they take a lot of time. Reach out to me using one of the methods below if you have any questions!

* `usability-notes:` Some of these trees do not contain everything needed to boot and use the device as normal in their current form. Since these kernels are designed to be used as a base for others or merged into existing working kernels, those commits will not be added. Instead, I give notes that can be used to get everything working properly. I only do usability notes for devices I physically own; if you own a device in this list and there are quirks that you know of that need mentioning, feel free to contribute!

Each subfolder has its own index if you want more details!


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
git checkout -b <your_branch_name> FETCH_HEAD
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


# Getting help

If you need help with merging, I request you ask for it via one of these public methods:

* [XDA thread](https://forum.xda-developers.com/android/software-hacking/reference-how-to-upstream-android-kernel-t3626913)
* [Telegram Group](https://t.me/LinuxKernelNewbies)
* A GitHub issue in the repo in question

For all other questions/requests, you can reach out to me via:

* [Telegram](https://t.me/nathanchance)
* [Twitter](https://twitter.com/nathanchance)
* [XDA](https://forum.xda-developers.com/member.php?u=6842057)

# Other notes

Do not ask me permission to use these, they are freely available for a reason. Additionally, you don't need to give me credit for any public releases you do (although it would be appreciated). I'm not in this for glory, I just want people to be more stable and secure. Enjoy!
