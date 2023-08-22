..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2025 Intel Corporation.

.. _building_from_sources:

Building and Installing DPDK from Sources
=========================================

This chapter provides a comprehensive guide for building DPDK from sources on both
Linux and FreeBSD platforms. It covers the necessary steps, prerequisites, 
and considerations for different architectures and compilers.

Required Tools
--------------

The following tools are required to build DPDK:

- ``gcc`` (version 5+) or ``clang`` (version 3.6+)
- ``pkg-config`` or ``pkgconf``
- Python 3.6 or later
- ``meson`` (version 0.53.2+) and ``ninja``
 
  - To install meson, use ``pip install meson``
  - To install ninja, use ``pip install ninja``

- ``pyelftools`` (version 0.22+)

For RHEL/Fedora systems, you can install these using the command 
``dnf groupinstall "Development Tools"``. For Ubuntu/Debian systems, 
use ``apt install build-essential``. For Alpine Linux, 
use ``apk add alpine-sdk bsd-compat-headers``.

For FreeBSD, these can be installed using (as root):

.. code-block:: bash

   pkg install meson pkgconf py38-pyelftools

FreeBSD also requires kernel sources, which should be included during the installation of FreeBSD on the development platform.

Building DPDK
-------------

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
This might include setting specific flags or options. For example: “meson setup -Dbuildtype=debugoptimized build”. Then compile using “ninja” and install using “meson install”.

.. code-block:: bash

   ninja -C build
   cd build
   sudo ninja install

For detailed information on Meson build configuration options specific to DPDK, see :ref:`DPDK Meson Build Configuration Options <dpdk_meson_build_options>`.

Cross-Compilation Instructions for Different Architectures
----------------------------------------------------------

For instructions on building DPDK for ARM64, LoongArch, and RISC-V, refer to :ref:`cross_compile_dpdk`.
