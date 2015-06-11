---
layout: docs
title: Using Images
next_section: community
prev_section: building-from-source
permalink: /docs/using-images/
---

## ARMv7-based Beaglebone boards

At the time of this writing, Robert C. Nelson is building complete images (also known as firmware images) for ARMv7-based Beaglebone boards of Debian Wheezy with Machinekit already installed. These images are being generated on a weekly basis from the Master branch of the Machinekit repository and can be found in date-stamped subdirectories of [https://rcn-ee.com/rootfs/bb.org/testing](http://rcn-ee.com/rootfs/bb.org/testing). For example, the subdirectory `2015-06-08/machinekit/` contains the compressed image `bone-debian-7.8-machinekit-armhf-2015-06-8-4gb.img.xz`. 

These images may be downloaded and installed to uSD cards, and from them to onboard eMMc is that is desired, in the same way that regular Beaglebone system images are, a process described on many other websites. The desktop wallpaper included on this image is a treat. 

RCN's website is a treasure trove of other Beagleboard/Beaglebone software builds including many Linux kernels. See [http://elinux.org/Beagleboard:BeagleBoneBlack_Debian](http://elinux.org/Beagleboard:BeagleBoneBlack_Debian) to get a feel for the breadth of his offerings (try searching on `machinekit`).

## i386/686/amd64 LiveCD/LiveUSB images

From time to time, interested parties propose to generate LiveCD/LiveUSB Machinekit images which can be used on i386/686- and amd64-based systems in the same way that comparable images for many Linux distributions are used. At the time of this writing, there is no such project-supported image but stay tuned.
