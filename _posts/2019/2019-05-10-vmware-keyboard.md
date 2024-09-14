---
layout: post
title: "VMWare VM Doesn't Accept Keyboard Input after Conversion"
date: 2019-05-10 14:36:17 -0400
categories: vmware troubleshooting
---

Recently used [vCenter Converter]([https://www.vmware.com/go/getconverter](https://www.vmware.com/go/getconverter)) to create a VM from a Lenovo ThinkPad and on booting the VM afterwards, discovered that it would not accept keyboard input. Not even from the “Send Ctrl+Alt+Del” button. The mouse was fine, so I was able to use Windows’ on-screen keyboard to do some digging.

Device manager indicated that the keyboard device threw an error:

> Windows cannot start this hardware device because its configuration information (in the Registry) is incomplete or damaged.

The issue is that the registry entry carries some deprecated values for things like Lenovo’s UltraNav and Synaptics devices. So we need to track it down and clean it up. Use RegEdit and navigate to the following key:

`HKLM\SYSTEM\CurrentControlSet\Control\Class\{4d36e96b-e325-11ce-bfc1-08002be10318}`

Edit `UpperFilters` so that the only entry in it is `kbdclass`.

Reboot.