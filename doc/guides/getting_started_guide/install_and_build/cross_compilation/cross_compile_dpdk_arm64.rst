..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2025 Intel Corporation.

.. _cross_compile_dpdk_arm64:

Cross-compiling DPDK for ARM64 on Linux
---------------------------------------

This section provides instructions on how to cross-compile DPDK for ARM64 on an x86
build machine. It also covers how to compile a 32-bit aarch32 DPDK on an ARM64 build
machine. While it's generally recommended to natively build DPDK on ARM64 
(just like with x86), it's also possible to cross-compile DPDK for ARM64 using either
a GNU toolchain or an LLVM/Clang toolchain.

Prerequisites
=============

NUMA Library
^^^^^^^^^^^^

Most modern machines require the NUMA library. However, it's not needed for non-NUMA
architectures. To compile the NUMA library, make sure the libtool version is 2.2
or higher. Otherwise, the compilation will fail with errors. 
You can clone the NUMA library from its GitHub repository and compile it using the
following commands:

.. code-block:: bash

   git clone https://github.com/numactl/numactl.git
   cd numactl
   git checkout v2.0.13 -b v2.0.13
   ./autogen.sh
   autoconf -i
   ./configure --host=aarch64-linux-gnu CC=aarch64-none-linux-gnu-gcc --prefix=<numa install dir>
   make install

Meson Prerequisites
^^^^^^^^^^^^^^^^^^^

Meson depends on pkgconfig to find the dependencies. 
The package ``pkg-config-aarch64-linux-gnu``
is required for aarch64. To install it in Ubuntu, you can use the following command:

.. code-block:: bash

   sudo apt install pkg-config-aarch64-linux-gnu

For aarch32, you need to install pkg-config-arm-linux-gnueabihf:

.. code-block:: bash

   sudo apt install pkg-config-arm-linux-gnueabihf

GNU Toolchain
=============

Get the Cross Toolchain
^^^^^^^^^^^^^^^^^^^^^^^

You can download the latest GNU cross compiler toolchain from the ARM developer
website. It's always recommended to check and get the latest compiler tool from the
page and use it to generate better code. As of this writing, 9.2-2019.12 is the newest
version. The following description is an example of this version.

For aarch64:

.. code-block:: bash

   wget https://developer.arm.com/-/media/Files/downloads/gnu-a/9.2-2019.12/binrel/gcc-arm-9.2-2019.12-x86_64-aarch64-none-linux-gnu.tar.xz
   tar -xvf gcc-arm-9.2-2019.12-x86_64-aarch64-none-linux-gnu.tar.xz
   export PATH=$PATH:<cross_install_dir>/gcc-arm-9.2-2019.12-x86_64-aarch64-none-linux-gnu/bin

For aarch32:

.. code-block:: bash

   wget https://developer.arm.com/-/media/Files/downloads/gnu-a/9.2-2019.12/binrel/gcc-arm-9.2-2019.12-x86_64-arm-none-linux-gnueabihf.tar.xz
   tar -xvf gcc-arm-9.2-2019.12-x86_64-arm-none-linux-gnueabihf.tar.xz
   export PATH=$PATH:<cross_install_dir>/gcc-arm-9.2-2019.12-x86_64-arm-none-linux-gnueabihf/bin

Augment the GNU Toolchain with NUMA Support
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You need to copy the NUMA header files and lib to the cross compiler’s directories:

.. code-block:: bash

   cp <numa_install_dir>/include/numa*.h <cross_install_dir>/gcc-arm-9.2-2019.12-x86_64-aarch64-none-linux-gnu/aarch64-none-linux-gnu/libc/usr/include/
   cp <numa_install_dir>/lib/libnuma.a <cross_install_dir>/gcc-arm-9.2-2019.12-x86_64-aarch64-none-linux-gnu/lib/gcc/aarch64-none-linux-gnu/9.2.1/
   cp <numa_install_dir>/lib/libnuma.so <cross_install_dir>/gcc-arm-9.2-2019.12-x86_64-aarch64-none-linux-gnu/lib/gcc/aarch64-none-linux-gnu/9.2.1/

Cross Compiling DPDK with GNU Toolchain Using Meson
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To cross-compile DPDK on a desired target machine, you can use the following command:

.. code-block:: bash

   meson setup cross-build --cross-file <target_machine_configuration>
   ninja -C cross-build

For example, if the target machine is aarch64, you can use the following command, 
provided the cross file has been modified accordingly:

.. code-block:: bash

   meson setup aarch64-build-gcc --cross-file config/arm/arm64_armv8_linux_gcc
   ninja -C aarch64-build-gcc

If the target machine is aarch32, you can use the following command, 
provided the cross file has been modified accordingly:

.. code-block:: bash

   meson setup aarch32-build --cross-file config/arm/arm32_armv8_linux_gcc
   ninja -C aarch32-build

LLVM/Clang Toolchain
====================

Obtain the Cross Tool Chain
^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can download the latest LLVM/Clang cross compiler toolchain from the ARM developer
website.

.. code-block:: bash

   wget https://github.com/llvm/llvm-project/releases/download/llvmorg-10.0.0/clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz

The LLVM/Clang toolchain does not implement the standard c library. 
The GNU toolchain ships an implementation we can use. 
Refer to the section on obtaining the GNU toolchain to get the GNU toolchain.

Unzip and Add into the PATH
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

   tar -xvf clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz
   export PATH=$PATH:<cross_install_dir>/clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04/bin

Cross Compiling DPDK with LLVM/Clang Toolchain Using Meson
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To use the NUMA library, follow the same steps as for augmenting the GNU toolchain
with NUMA support. The paths to GNU stdlib must be specified in a cross file.
Augmenting the default ``cross-file’s c_args`` and ``c_link_args config/arm/arm64_armv8_linux_clang_ubuntu1804`` would look like this:

.. code-block:: bash

   c_args = ['-target', 'aarch64-linux-gnu', '--sysroot', '<cross_install_dir>/gcc-arm-9.2-2019.12-x86_64-aarch64-none-linux-gnu/aarch64-none-linux-gnu/libc']
   c_link_args = ['-target', 'aarch64-linux-gnu', '-fuse-ld=lld', '--sysroot', '<cross_install_dir>/gcc-arm-9.2-2019.12-x86_64-aarch64-none-linux-gnu/aarch64-none-linux-gnu/libc', '--gcc-toolchain=<cross_install_dir>/gcc-arm-9.2-2019.12-x86_64-aarch64-none-linux-gnu']

Assuming the file with augmented ``c_args`` and ``c_link_args`` is named
``arm64_armv8_linux_clang``, 
use the following command to cross-compile DPDK for the target machine:

.. code-block:: bash

   meson setup aarch64-build-clang --cross-file config/arm/arm64_armv8_linux_clang
   ninja -C aarch64-build-clang

Building for an ARM64 SoC on an ARM64 Build Machine
===================================================

If you wish to build on an ARM64 build machine for a different ARM64 SoC, 
you don’t need a separate cross toolchain, just a different set of configuration
options. To build for an ARM64 SoC, use the ``-Dplatform`` meson option:

.. code-block:: bash

   meson setup soc_build -Dplatform=<target_soc>

Substitute <target_soc> with one of the supported SoCs, such as 'generic', 'armada', 'bluefield', 'centriq2400', 'cn9k', 'cn10k', 'dpaa', 'emag', 'ft2000plus', 'tys2500', 'graviton2', 'graviton3', 'kunpeng920', 'kunpeng930', 'n1sdp', 'n2', 'stingray', 'thunderx2', 'thunderxt88', 'thunderxt83'.