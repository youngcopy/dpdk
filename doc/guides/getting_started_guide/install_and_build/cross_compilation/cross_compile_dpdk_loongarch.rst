..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2025 Intel Corporation.

.. _cross_compile_dpdk_loongarch:

Cross-compiling DPDK for LoongArch on Linux
-------------------------------------------

This section describes how to cross-compile DPDK for LoongArch from x86 build hosts.

Due to some of the code under review, the current Linux 5.19 cannot boot on LoongArch
system. There are still some Linux distributions that have supported LoongArch host,
such as Anolis OS, Kylin, Loongnix and UOS. These distributions base on Linux kernel
4.19 supported by Loongson Corporation. Because LoongArch is such a new platform with
many fundamental pieces of software still under development, 
it is currently recommended to cross compile DPDK on x86 for LoongArch.

Prerequisites
=============

Make sure you have all pre-requisites for building DPDK natively as those will be
required for cross-compilation.

Linux kernel
============

Make sure that LoongArch host is running Linux kernel 4.19 or newer supported by
Loongson Corporation. The support for LoongArch in the current Linux 5.19 is not
complete because it still misses some patches to add for other subsystems.

GNU toolchain
=============

The build process was tested using a precompiled toolchain:

- Latest LoongArch GNU toolchain on Debian 10.4 or CentOS 8.

After downloading the archive, we need to unzip and add those executable binaries into
the PATH as follows::

    tar -xvf <download_dir>/loongarch64-clfs-5.1-cross-tools-gcc-glibc.tar.xz -C <cross_tool_install_dir> --strip-components 1
    export PATH=$PATH:<cross_tool_install_dir>/bin

Alternatively the toolchain may be built straight from upstream sources. 
You can refer to this thread Introduce support for LoongArch architecture.

Cross Compiling DPDK with GNU toolchain using Meson
===================================================

To cross-compile DPDK for generic LoongArch we can use the following command::

    meson setup cross-build --cross-file config/loongarch/loongarch_loongarch64_linux_gcc
    ninja -C cross-build

Supported cross-compilation targets
===================================

Currently the following target is supported:

- Generic LoongArch64 ISA: config/loongarch/loongarch_loongarch64_linux_gcc

To add a new target support, a corresponding cross-file has to be added to the
config/loongarch directory.