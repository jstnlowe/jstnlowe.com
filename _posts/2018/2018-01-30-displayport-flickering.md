---
layout: single
title: "DisplayPort Flickering on Dell Optiplex 9020"
date: 2018-01-30 13:53:37 -0400
categories: hardware troubleshooting
published: true
---

When multiple DisplayPort 1.2-compatible displays are connected via DisplayPort to the integrated Intel HD 4600 in an Optiplex 9020, one or both of the displays will flicker off and on intermittently. Usually it is the secondary display. In this case, it was a pair of Dell U2415s. Updating drivers will have no effect - this is an issue with the monitor hardware/firmware.

The solution is to disable DisplayPort 1.2 on the monitors themselves. [For the U2415, see page 28 in the user manual](http://downloads.dell.com/manuals/all-products/esuprt_display_projector/esuprt_display/dell-u2415_user%27s%20guide_en-us.pdf#page=28). Note that this fix is only if you have both monitors connected to the outputs on the computer not if you are daisy-chaining. In the case of daisy-chained monitors, the final monitor in the chain should be the one to have DP 1.2 disabled.

This fix has also been reported to have worked for other systems (e.g. Macbook Pro) that experience similar issues.