..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2015 Intel Corporation.

.. _windows_install_build:

Windows DPDK Build
==================

Before you begin the process of building DPDK on Windows, make sure your system meets all the necessary requirements as outlined in the :doc:`Windows System Requirements <../sys_reqs/windows_sys_req>` page. 

Once you have verified that your system meets these requirements, you can proceed with the following steps to build DPDK.

Build the Code
--------------

The build environment is setup to build the EAL and the helloworld example by default. To compile the examples, the flag -Dexamples is required.

**Option 1. Native Build on Windows**

When using Clang-LLVM, specifying the compiler might be required to complete the meson command::

        set CC=clang

When using MinGW-w64, it is sufficient to have toolchain executables in PATH::

        set PATH=C:\MinGW\mingw64\bin;%PATH%

To compile the examples::

        cd C:\Users\me\dpdk
        meson -Dexamples=helloworld build
        ninja -C build

**Option 2. Cross-Compile with MinGW-w64**

The cross-file option must be specified for Meson. Depending on the distribution, paths in this file may need adjustments::

        meson --cross-file config/x86/cross-mingw -Dexamples=helloworld build
        ninja -C build