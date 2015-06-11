---
layout: docs
title: Realtime Kernels
next_section: packages-debian
prev_section: installation-overview
permalink: /docs/realtime-kernels/
---

## Introduction

There are four choices of Linux kernel supported by Machinekit

* the standard[1] Linux kernel, which is capable of meeting only soft realtime requirements at best.

* the so-called RT-PREEMPT kernel. This refers to the standard Linux kernel with the addition of a preemption patch and a high-resolution clock event layer which make it fully preemptible and capable of meeting some hard realtime requirements. At the time of this writing, an RT-PREEMPT kernel is available in the stock package stream for Debian version 7, codenamed Wheezy, but not for version Debian 8, codenamed Jessie, and only for i386/686 and amd64 architectures. Within limits, of course, newer Debian releases will run on older kernels.

* the Xenomai kernel, which is a real-time development framework cooperating with the Linux kernel, capable of meeting hard realtime requirements and with generally lower latency than the RT_PREEMPT kernel. Custom Xenomai kernels are maintained by the Machinekit project and friends for all platforms supported by Machinekit.

* the RTAI kernel, which is the Linux kernel extensively modified to provide realtime extensions. It is capable of even lower latency than the Xenomai kernel at the expense of significant kernel dependencies. Custom RTAI kernels are maintained by the Machinekit project for i386/686 and amd64 architectures only.


## Choice of Kernel

What constitutes *hard* realtime requirements depends on the application.

Typically, the standard Linux kernel is used only during the development of Machinekit software and during tests and demonstrations of Machinekit applications in simulator configurations.

Both the RT-PREEMPT and the Xenomai kernels are good choices for Machinekit applications involving hardware step generation in the case of stepper motor control and with plain servo configurations in the case of servo motor control. Machinekit packages built for these kernels have no sigificant kernel dependencies so package upgrades on an existing system are easy.

The RTAI kernel only makes sense on systems with high-rate software step generation and dumb interface hardware such as a parallel port. Because Machinekit/RTAI packages run only with the RTAI kernel for which they are built, package upgrades on an existing system may not be straightforward.


[1] "standard" here means the mainline kernel possibly modified by a particular Linux distribution such as Debian.
