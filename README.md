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
