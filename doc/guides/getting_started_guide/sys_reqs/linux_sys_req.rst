..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2015 Intel Corporation.

.. _linux_sys_req:

Linux System Requirements
=========================

Before you begin installing and configuring DPDK on a Linux-based operating system, it’s important to make sure your system meets the necessary requirements.

Kernel Version
--------------

DPDK requires a Linux kernel version of 4.14 or later. You can check your kernel version by running the following command::

        uname -r

Required Tools
--------------

The following tools are required to install and use DPDK:

- ``gcc`` (version 4.9+) or ``clang`` (version 3.4+)
- ``pkg-config`` or ``pkgconf``
- Python 3.6 or later
- ``meson`` (version 0.53.2+) and ``ninja``
- ``pyelftools`` (version 0.22+)

For RHEL/Fedora systems, you can install these using the command ``dnf groupinstall "Development Tools"``. For Ubuntu/Debian systems, use ``apt install build-essential``. For Alpine Linux, use ``apk add alpine-sdk bsd-compat-headers``.

Hugepages Support
-----------------

DPDK requires the Linux kernel to support hugepages. This is typically enabled by default on most modern Linux distributions. To check if hugepages are enabled on your system, you can run the following command::

        grep HugePages_ /proc/meminfo

If hugepages are not enabled, you will need to enable them. The process for this varies depending on your Linux distribution, so you may need to refer to your distribution's documentation.

UIO or VFIO Support
-------------------

DPDK requires either UIO or VFIO support in the kernel. The ``igb_uio`` or ``vfio-pci`` module is typically used. You can check if these modules are loaded with the following command::

        lsmod | grep -e igb_uio -e vfio_pci

If the modules are not loaded, you will need to load them. This can usually be done with the ``modprobe`` command, but the exact process may vary depending on your Linux distribution.

NIC Compatibility
-----------------

DPDK can work with many different types of Network Interface Cards (NICs), but performance can vary. Check the `DPDK NIC compatibility list <https://core.dpdk.org/supported/>`_ to verify your NIC is supported.

Additional Libraries
--------------------

A number of DPDK components, such as libraries and poll-mode drivers (PMDs), have additional dependencies. These dependencies will be automatically detected during the DPDK build process, enabling or disabling the relevant components appropriately.

For libraries, the additional dependencies include:

- libarchive: for some unit tests using tar to get their resources.
- libelf: to compile and use the bpf library.

For poll-mode drivers, the additional dependencies for each driver can be found in that driver’s documentation in the relevant DPDK guide document, e.g. :doc:`Network Interface Controller Drivers <../../nics/index>`
