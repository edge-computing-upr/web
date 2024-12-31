---
layout: page
title: Jetson Orin Nano Setup
slim: true
---

1. First we ned to update the Firmware on the Jetson Orin Nano. If you are not sure which one you have. Recommend the follow step 2 to upgrade firmware to 36.x or greater. Otherwise, skip to step 4.
2. In the following link for the  [Jetson Orin Nano Jetpack 5.13 firmware](https://www.jetson-ai-lab.com/initial_setup_jon.html#360-upgrade-the-jetson-uefi-firmware-to-36x) from step 2.1 (You can follow all the steps from this link and skip to step 5).
3. Download the 5.13 Jetpack and follow step 2 in the [dowload for your operating system](https://developer.nvidia.com/embedded/learn/get-started-jetson-orin-nano-devkit#write). **Make sure to flash with the Jetpack 5.13 firmware and not Jetpack 6.x**.
    - You need to download [Balena Etcher](https://etcher.balena.io/) in the guide as well. This flashes the SD card with the firmware. You may need other software depending on your operating system.
4. Then follow all the steps in [write image to micro SD card](https://developer.nvidia.com/embedded/learn/get-started-jetson-orin-nano-devkit#write). **Make sure to download latest Jetpack (currently v6.1).**
5. Once the install Jetpack on top of the Jetson Linux:
```
apt install nvidia-jetpack
```
