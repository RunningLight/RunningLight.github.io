---
layout: docs
title: Using Debian packages
next_section: building-from-source
prev_section: realtime-kernels
permalink: /docs/packages-debian/
---

## Summary

Installing Machinekit from binary Debian packages proceeds in a series of steps

1. install a Debian distribution.

2. configure APT

3. install a realtime kernel.

4. install the binary Debian packages for the Machinekit run-time environment.

5. (Optionally) install the binary Debian packages for a development environment.


The instructions on this website presume you have a basic proficiency working in the Linux
bash shell from the command line in a terminal, know the difference between an
ordinary user and the root user and can switch between them, know what a Debian
package is and can use APT-related tools, and so forth. Only minimal attention
is paid here to Linux subtleties such as prompts you may receive from a
command you invoke, such as a request for you to enter a password or to answer
respond yes (Y/y) or no (N/n). The answer, by the way, is almost always yes.
As the saying goes, "Google is your friend," and so are the man pages on your
system and the [Community][1] channels.

It is strongly recommended you perform these steps as an ordinary user and
not the root user. This requires that the ```sudo``` command be present and
also that you have sudo privileges. If you like living life in the fastlane,
you can perform them all as the root user, omitting the ```sudo``` prefix
where it occurs. We are not responsible for the result.

The `sudo` command may or may not be present on your Debian system
depending on the specific flavor of desktop environment you installed, if any.
If `sudo` is not present at the end of Step 1 (simple test: try to invoke `sudo`) then you need to
perform an additional step: 

```
su -c "apt-get install sudo"
```

To give yourself all sudo privileges (which is overkill, by the way):

```
su -c "adduser <your username> sudo"
```

where the entire string \<your username> should be replaced by your username.

Log out of the system, then log in again as the chosen user to
pick up the new privileges.

## Step 1- Install a Debian distribution

At the time of this writing, Machinekit is supported on Debian version 7, codenamed Wheezy, and Debian version 8, codenamed Jessie. Until very recently in the life of the Machinekit project, Wheezy was the stable Debian release. As of 20150425, Jessie became the stable Debian release and Wheezy was reclassified as "obsolete stable". While Machinekit now compiles and passes project self-tests on both releases on the Buildbot, there has been more experience accumulated with Machinekit running on Wheezy. Wrinkles which appear with Machinekit running on Jessie will be ironed out as they are reported.

It may be possible to make corresponding releases of Debian-based distributions such as Ubuntu and Linux Mint work with the binary Debian packages but this subject is not discussed further here.

## Step 2- Configure APT

The Debian Advanced Package Tool must be configured before it can locate, download, and install necessary binary packages beyond those available in the standard Debian release repository.

#### for i386/686- and amd64-based systems and ARMv7-based Beaglebone boards

If on Wheezy, copy and paste the following commands into a shell to configure APT:

```
sudo sh -c \
    "echo 'deb http://deb.dovetail-automata.com wheezy main' > \
    /etc/apt/sources.list.d/machinekit.list; \
    apt-get update ; \
    apt-get install dovetail-automata-keyring"
sudo apt-get update
```
Then proceed to Step 3.

If on Jessie, copy and paste the following instead:

```
sudo sh -c \
    "echo 'deb http://deb.dovetail-automata.com jessie main' > \
    /etc/apt/sources.list.d/machinekit.list; \
    apt-get update ; \
    apt-get install dovetail-automata-keyring"
    sudo apt-get update
```
Then proceed to Step 3.

#### For the ARMv6-based Original Raspberry Pi board

Copy and paste the following commands into a shell to configure APT:

```
sudo sh -c \
   "apt-key adv --keyserver hkp://keys.gnupg.net --recv-key 49550439; \
   echo 'deb http://0ptr.link/raspbian wheezy main' > \
   /etc/apt/sources.list.d/rpi-machinekit.list"
sudo apt-get update
```

> NOTE this repository currently supports only Wheezy

Then proceed to step 3.

#### for other ARM-based platforms

New ARM-based single-board computers are showing up like clockwork, some of them with features which appear favorable to Machinekit applications. As experience is gathered with them, additional information may be added here. This will happen sooner if you report to the [Community][1] channels your successes---and failures---applying Machinekit to new boards. At a minimum, for ARMv7-based platforms, one can configure APT as described above, then skip to Step 4 and install just the `machinekit-posix` package.

## Step 3- Install a realtime kernel

This step may be skipped if only the standard Linux kernel is to be used since it is already present in the installed distribution.

#### Install an RT-PREEMPT realtime kernel (i386/686 and amd64)

If on an i386/686-based system, run the command:

```
sudo apt-get install linux-image-rt-686-pae
```

If on an amd64-based system, run the command:

```
sudo apt-get install linux-image-rt-amd64
```

Proceed to Step 4.

#### Install a Xenomai realtime kernel (all platforms)

If on an i386/686-based system, run the following command and proceed to Step 4:

```
sudo apt-get install linux-image-xenomai.x86-686-pae

```

If on an amd64-based system, run instead the following command and proceed to Step 4:

```
sudo apt-get install linux-image-xenomai.x86-amd64
```

If on a ARMv7-based Beaglebone board, run instead the following command and proceed to Step 4:

```
sudo apt-get install linux-image-xenomai.beaglebone-omap
```

If on an ARMv6-based original Raspberry Pi board, run instead the following command and proceed to Step 4 (be sure to see the Post-Installation Hints, below):

```
sudo apt-get install linux-image-xenomai
```

#### Install an RTAI kernel (i386/686 and amd64)

If on an i386/686-based system, run the following command and proceed to step 4:

```
sudo apt-get install linux-image-rtai.x86-686-pae
```

If on an amd64-based system, instead run the following command and proceed to Step 4:

```
sudo apt-get install linux-image-rtai.x86-amd64
```

## Step 4- Install the Binary Debian Packages for the Machinekit Run-time Environment

This step is a bit of an anticlimax. Copy and paste one or more of the following commands to 
install the machinekit run-time environment for your kernel choice (multiple
kernels and flavors possible):

```
sudo apt-get install machinekit-rt-preempt
```

```
sudo apt-get install machinekit-xenomai
```

```
sudo apt-get install machinekit-rtai-kernel
```

In addition, one can install the following package over any kernel, notably the standard Linux kernel, to enable running Machinekit in non-realtime, so-called simulator mode:

```
sudo apt-get install machinekit-posix
```

## Step 5- (Optionally) Install the Binary Debian Packages for a Development Environment

For those wanting a development environment, run the following command:

```
sudo apt-get install libczmq-dev python-zmq libjansson-dev \
    libwebsockets-dev libxenomai-dev python-pyftpdlib
```

In the case of Wheezy---but not Jessie---it is necessary to install a backported version of `cython`, which is accomplished by running the following commands:

```
sudo sh -c \
    "echo 'deb http://ftp.us.debian.org/debian wheezy-backports main' > \
     /etc/apt/sources.list.d/wheezy-backports.list"
sudo apt-get update
sudo apt-get install -t wheezy-backports cython
```

## Post-installation hints

#### Original Raspberry Pi

The kernel image needs to be copied to the boot partition like so:

```
sudo mv /boot/kernel.img /boot/kernel.img.bck
sudo cp /boot/vmlinuz* /boot/kernel.img
```

#### Beaglebone

Please see [Alex's installation hints](https://github.com/strahlex/asciidoc-sandbox/wiki/Creating-a-Machinekit-Debian-Image)

#### Keeping up to date (all systems)

The preceeding steps install the version of Machinekit that was current at the time the packages were built. After installation, one can now use APT to upgrade to newer packages as they become available by running the following commands:

```
sudo apt-get update
sudo apt-get upgrade
```

Upgrading should be approached with caution because Machinekit is a rapidly moving development project and occasionally new features (or unintentional new bugs!) may break working systems. It is possible to roll back an upgrade but this may not produce the desired result. Be sure to keep up with the traffic on the [Community][1] channels.

## Other things to do

- Browse the Debian archive directly at
  [http://deb.dovetail-automata.com/pool/](http://deb.dovetail-automata.com/pool/)

[1]: /docs/community

