---
layout: docs
title: Installation Overview
next_section: realtime-kernels
prev_section: home
permalink: /docs/installation-overview/
---

## Introduction

Three approaches exist for installing Machinekit

* using binary packages (.deb files) to install Machinekit to an existing Debian Linux system. This approach is available for i386/686- and amd64-based systems, the ARMv6-based original Raspberry Pi board, and certain ARMv7-based boards (Beaglebone and Raspberry Pi 2, among others and is the approach recommended for most purposes. The files comprising Machinekit are installed into standard system directories.

* building from source. This approach is available across architectures and platforms but is the most involved of the three. In Debian and Debian-derived Linux systems, the files comprising Machinekit are installed by default into the directory in which they are built but optionally they can be installed elsewhere in the system.

* using a complete system image which has Machinekit already installed in a ready-to-run Debian Linux system. This approach is supported only for BeagleBone motherboards at present but images for other ARM-based boards and so-called LiveCD/LiveUSB versions for i386/686- and amd64-based systems likely will be supported at some point. Note that "support" is used here in the sense of the images being updated from the official Machinekit repository on a regular cycle and made available through well-known portals, at which point they are included in these instructions.

## Debian Linux

Debian Linux is the primary distribution used in the development of Machinekit. As part of our [C4][1] collaborative work process, all patches committed to the Machinekit repository must have been tested in our Buildbot to ensure they compile cleanly and pass a growing collection of project self-tests. Currently, these Buildbot tests are performed in Debian version 7, codenamed Wheezy, and Debian version 8, codenamed Jessie, systems running on virtual or real hosts. Binary packages are continually being built from the Machinekit repository and served through our third-party Debian package distribution infrastructure while the source code is available directly from the Machinekit repository for locally building Machinekit from source.

[1]: /docs/C4/
