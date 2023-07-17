..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2014 Intel Corporation.

Drivers
=======

The process of setting up drivers for DPDK varies depending on the operating system you're using. Below, you'll find detailed instructions for each operating system.

Linux Drivers
-------------

If you're using Linux, you'll need to bind and unbind network ports to/from the kernel modules. Depending on the Poll Mode Driver (PMD) being used, a corresponding kernel driver should be loaded, and network ports should be bound to that driver. The utility script dpdk-devbind.py is provided in the usertools subdirectory of DPDK to help with this. For detailed instructions, please refer to the :doc:`Linux Drivers <../linux_gsg/linux_drivers>` page.

FreeBSD Drivers
---------------

The specific page for loading the DPDK contigmem Module and DPDK nic_uio Module for FreeBSD is not available at the moment. Please refer to the general FreeBSD Getting Started Guide for more information.

Windows Drivers
---------------

Please refer to the general Windows Getting Started Guide for more information.
Please note that the process of setting up drivers may require root privileges or equivalent, depending on your operating system. Always make sure you have the necessary permissions before attempting to modify system drivers.
