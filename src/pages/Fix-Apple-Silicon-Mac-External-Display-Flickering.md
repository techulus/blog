---
template: post
title: "Fix Apple Silicon Mac External Display Flickering"
date_published: 1705648747176
cover: /cover/macbook.jpg
---

If you're experiencing screen flickering issues while connected to an external display on your Apple silicon Mac, you're not alone.
Flickering screens and faint lines can be frustrating, but fear not – I've got a solution for you. The only catch is that this fix requires your monitor have some sort of HDR capability.

## Step 1: Install the Latest Monitor Firmware

The first step is to ensure your monitor (in my case, it's Dell U3223QE and the firmware version is M3T103) is running the latest firmware.
If its a Dell monitor, head over to the Dell support website and find the latest firmware update for your monitor model.
Download and install it following the provided instructions.

## Step 2: Install Monitor Driver & Color Profiles (If available)

To enhance compatibility and to get custom color profiles from Dell, installing the monitor driver is essential.
Visit the Dell support website once again, locate the appropriate monitor driver, and proceed with the installation.
After the installation is complete, restart your Mac to ensure the changes take effect.

## Step 3: Update Display Settings

Start by enabling HDR on your monitor, this will probably be done using monitors hardware settings (on screen menu).
If enabled properly you will see HDR settings inside Mac display settings.

Next, on your Mac, go to System Settings > Displays and update the settings as follows:

- Enable HDR for the external display.
- Select an sRGB color profile from the color profiles installed by the monitor driver.
- Refresh rate should be 60 Hertz.

![Monitor Settings](/images/monitor-settings.png "Monitor Settings")

Next, switch to Built-in display settings and disable True Tone (if its a Macbook).

![Mac Settings](/images/mac-settings.png "Mac Settings")

Hopefully this will resolve the annoying flickering! :)

