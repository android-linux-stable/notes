# linux-stable notes

These are markdown pages offering some notes about what linux-stable is, how you should be using it, and issue resolution notes.


# Index

## Conflict resolution notes

- [`msm-4.4-conflict-resolution.md`](msm-4.4-conflict-resolution.md) These are the notes for all the conflicts in the [msm-4.4-linux-stable](https://github.com/nathanchance/msm-4.4-linux-stable) repository, which is plain CAF source with the latest linux-stable merged in.

- [`op5-conflict-resolution.md`](op5-conflict-resolution.md) These are the notes for all the conflicts in the [op5-linux-stable](https://github.com/nathanchance/op5-linux-stable) repository, which is the stock OnePlus 5 source with the latest linux-stable merged in.

- [`wahoo-conflict-resolution.md`](wahoo-conflict-resolution.md) These are the notes for all the conflicts in the [wahoo-linux-stable](https://github.com/nathanchance/wahoo-linux-stable) repository, which is the stock Pixel 2 and Pixel 2 XL source with the latest linux-stable merged in (along with commits for proper compilation and usage).

## Usability notes

These kernels do not contain everything needed to boot and use the device as normal in their current form. Since these kernels are designed to be used as a base for others or merged into existing working kernels, those commits will not be added. Instead, I give notes that can be used to get everything working properly.

- [`wahoo-usability.md`](wahoo-usability.md) Notes for the Pixel 2 and Pixel 2 XL kernel
- [`op5-usability.md`](wahoo-usability.md) Notes for the OnePlus 5 kernel

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
