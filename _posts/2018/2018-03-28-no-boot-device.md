---
layout: post
title: "Dell Optiplex 9020: No boot device available"
date: 2018-03-28 23:04:51 -0400
categories: hardware troubleshooting
---

The mid-2013 Optiplex 9020 models that shipped with Windows 7 run into an issue on installing Windows 10 (or any UEFI OS), as they're configured for Legacy boot mode from the factory. You'll finish the install, reboot, and be presented with the message: "No boot device available."

To fix this:

1. Reboot the system and hit `F12`
2. Select Change Boot Mode Settings
3. Select UEFI Boot Mode, Secure Boot ON
4. Confirm the selection and reboot

Note that you may have to do a hard boot in order to get the Dell bios splash and be able to access the boot menu.