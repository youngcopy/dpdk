..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2014 Intel Corporation.

Installation and Compilation
============================

The process of installing and compiling DPDK varies depending on the operating system you're using. Below, you'll find detailed instructions for each operating system.

Compiling the DPDK Target from Source
-------------------------------------

Compiling the DPDK Target from Source is a common step for all operating systems. For detailed instructions based on your operating system, please refer to the respective pages:

- :doc:`Linux <../linux_gsg/build_dpdk>`
- :doc:`FreeBSD <../freebsd_gsg/build_dpdk>`
- :doc:`Windows <../windows_gsg/build_dpdk>`

Cross-Compile DPDK for Different Architectures (Linux)
------------------------------------------------------

If you're using Linux, you may need to cross-compile DPDK for different architectures. For detailed instructions, please refer to the :doc:`Cross compiling DPDK for different architectures <../linux_gsg/cross_build_dpdk_for_arm64>` page.

FreeBSD
-------

If you're using FreeBSD, you can install DPDK from the Ports Collection. For detailed instructions, please refer to the :doc:`Installing DPDK from the Ports Collection <../freebsd_gsg/install_from_ports>` page.

Windows
-------

If you're using Windows, there are several additional steps:

- First, verify if your system meets the :doc:`System Requirements for compiling the DPDK Target from Source <../windows_gsg/build_dpdk>`.
- Next, choose between the :ref:`Clang-LLVM C Compiler and Microsoft MSVC Linker <Option_1._Clang-LLVM_C_Compiler_and_Microsoft_MSVC_Linker>` or the :doc:`MinGW-w64 Toolchain <../windows_gsg/build_dpdk:option-2-mingw-w64-toolchain>`.
- Finally, :doc:`Install the Build System and Backend <../windows_gsg/build_dpdk:install-the-build-system>`.