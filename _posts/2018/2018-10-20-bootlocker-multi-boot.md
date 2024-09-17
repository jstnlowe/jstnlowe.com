---
layout: single
title: "Multi-booting Windows 10 Environments with Bitlocker Enabled"
date: 2018-10-20 09:53:33 -0400
categories: windows
published: true
---

The goal here is to get multiple installations of Windows 10 on separate encrypted partitions on a single physical drive and we want to use the stock Windows bootloader and Bitlocker, avoiding any third-party solutions because I'm a fan of keeping things as simple as possible. I'd say the end result accomplishes that, but figuring out how to get to that point was a pain in the ass.

It turns out that combining multi-booting and Bitlocker is a bit more complicated to set up - and to maintain - than you'd think. If you hunt around online, almost all of the information you're going to find on this topic involves dual-booting Windows and some flavor of Linux or two different versions of Windows (for some reason, Windows 10 and Windows 7 is a really popular combination) and that requires delving into the BIOS to mess with [UEFI](https://en.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface) settings, which I've dealt with in the past. Add to this that the standard way of going about using Bitlocker system drive encryption will create quite a mess for you.

First, prep your installation media: grab Rufus, a USB drive that's at least 4GB (I recommend the [Kingston DTSE9G2](https://amzn.to/2PKgDhW)), and a Windows 10 ISO. I'm also going to assume you've done a Windows 10 installation before so that I can skip some of the details.

# Installation
1. Boot into the Windows Installer and partition the drive into as many partitions as OS installations that you intend to have.
2. Continue to install the first Windows 10 instance.
3. Boot into it and complete the setup process.
4. Reboot into the Windows Installer and install your second instance on another partition.
5. Boot into that instance and complete the setup process.
6. Repeat until you have however many installations you partitioned for.

# Bitlocker Configuration
This is where things get a little complicated. _Do not just boot into each of the installs and take the usual step of enabling system drive encryption._ If you do that, you will find that the system will constantly prompt for the 48 digit Bitlocker recovery keys and your life will be hell. Instead, use the following procedure:

1. Boot into your first Windows 10 install (we'll call this the "primary" installation)
2. Enable Bitlocker system drive encryption but do not enable Bitlocker on any other partitions.
3. For the love of god back up the ID and the recovery key because, as you'll find out in a bit, you will actually need it.
4. Reboot and ensure that you can boot into installation A without an issue.
5. Now enable fixed-drive Bitlocker on each of the alternate partitions, using a different password for each of them.
6. Again, back up the IDs and recovery keys. Jesus christ, just do it. Trust me.
7. Reboot and attempt to boot into one of the alternate installations from the bootloader.

What should happen at this point, is that instead of loading the selected Windows installation, the system will reboot and prompt you for the Bitlocker key for that particular partition/install. Enter your password and, if it works, you're all set. From within any of the installations, you should still see the other partitions, but they should be locked and inaccessible unless you unlock them with their respective passwords. You now have multiple encrypted installs of Windows 10 without having to use any third-party tools.

# Recovery Keys Matter
So why the insistence on backing up the recovery keys? Because there are seemingly benign things you probably don't normally even pay attention to that will trigger Bitlocker's recovery mode. Some things that I have found that can trigger it:

- Updating device drivers
- Major OS updates (e.g. the "Creator's Update")
- Updating the UEFI/BIOS
- Modifying or clearing the TPM settings
- Group Policy changes

And probably other things. In every case, you'll have no warning. You'll install an update or apply a setting and reboot and Bitlocker will prompt you for that recovery key. It won't happen often (thank god), but it will happen. And if you don't have the appropriate recovery key for whatever partition triggered the recovery (which is why I told you to keep track of both the ID and the key), everything on that partition will be unrecoverable. Period. End of story.

# Further Isolation
This is optional, but for an added layer of isolation, you can remove the drive letters of the other partitions in each of your Windows installations using the [Disk Management interface](https://docs.microsoft.com/en-us/windows-server/storage/disk-management/overview-of-disk-management). Now, those partitions will no longer be visible or accessible from within that installation