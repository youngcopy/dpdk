..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2025 Intel Corporation.

.. _building_from_sources:

Building and Installing DPDK from Sources
=========================================

This chapter provides a comprehensive guide for building DPDK from sources on both
Linux and FreeBSD platforms. It covers the necessary steps, prerequisites, 
and considerations for different architectures and compilers.

.. note:: For FreeBSD-specific instructions, jump to the `FreeBSD Instructions section <#freebsd-instructions>`_.

Linux Instructions
------------------

Prerequisites
^^^^^^^^^^^^^

- meson
- ninja
- pkg-config

Download the DPDK source code from the official repository 
``https://fast.dpdk.org/rel/``.

Use ``wget`` to grab the DPDK version::

        wget https://fast.dpdk.org/rel/dpdk-<version>.tar.xz

Extract the downloaded archive:

.. code-block:: bash

   tar -xvf dpdk-<version>.tar.gz

Navigate to the DPDK directory:

.. code-block:: bash

   cd dpdk-<version>

Configure the build based on your needs, hardware, and environment. 
This might include setting specific flags or options.

Compile the source code:

.. code-block:: bash

   make

Install the compiled binaries:

.. code-block:: bash

   sudo make install

FreeBSD Instructions
--------------------

Prerequisites
^^^^^^^^^^^^^

- meson
- ninja
- pkgconf
- py38-pyelftools

These can be installed using (as root):

.. code-block:: bash

   pkg install meson pkgconf py38-pyelftools

Building DPDK
^^^^^^^^^^^^^

.. code-block:: bash

   meson setup build
   cd build
   ninja
   ninja install

.. note:: For detailed instructions on binding and unbinding network ports to/from kernel modules, refer to :ref:`Linux Modules <linux_modules>`.

Cross-Compilation Instructions for Different Architectures
----------------------------------------------------------

- **ARM64**: :ref:`Instructions for building DPDK for ARM64 architecture <cross_compile_dpdk_arm64>`.
- **LoongArch**: :ref:`Instructions for building DPDK for LoongArch architecture <cross_compile_dpdk_loongarch>`.
- **RISC-V**: :ref:`Instructions for building DPDK for RISC-V architecture <cross_compile_dpdk_riscv>`.

Basic Guide for Cross-Compilation Using GCC
-------------------------------------------

- Set up the cross-compilation environment.
- Configure the build with specific flags for the target architecture.
- Compile and install.

.. note:: For more detailed cross-compilation instructions, see :ref:`Cross Compilation <cross_compilation>`.

Compiler Considerations
-----------------------

- **GCC**: Guidelines for building DPDK using the GNU Compiler Collection.
- **Clang**: Guidelines for building DPDK using the Clang compiler.

Building with Meson
-------------------

For detailed information on Meson build configuration options specific to DPDK, see :ref:`DPDK Meson Build Configuration Options <dpdk_meson_build_options>`.