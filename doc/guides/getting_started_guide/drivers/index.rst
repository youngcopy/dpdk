..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2014 Intel Corporation.

Drivers
=======

The process of setting up drivers for DPDK varies depending on the operating system you're using. Below, you'll find detailed instructions for each operating system.

.. toctree::
    :maxdepth: 2
    :hidden:

    linux_drivers
    freebsd_drivers
    windows_drivers

**Linux**

If you're using Linux, you'll need to bind and unbind network ports to/from the kernel modules. Depending on the Poll Mode Driver (PMD) being used, a corresponding kernel driver should be loaded, and network ports should be bound to that driver. The utility script dpdk-devbind.py is provided in the usertools subdirectory of DPDK to help with this. For detailed instructions, please refer to the :doc:`Linux Drivers <linux_drivers>` page.

**FreeBSD**

If you're using FreeBSD, you'll need to load the DPDK contigmem Module and DPDK nic_uio Module. For detailed instructions, please refer to the :doc:`FreeBSD Drivers <freebsd_drivers>` page.

**Windows**

Before running DPDK applications on Windows, certain kernel-mode drivers need to be installed. These drivers are not signed, so signature enforcement has to be disabled. However, be aware that disabling driver signature enforcement can weaken OS security and is generally discouraged in production environments. For detailed instructions, please refer to the :doc:`Windows Drivers <windows_drivers>` page.

.. note:
   Please note that the process of setting up drivers may require root privileges or equivalent, depending on your operating system. Always make sure you have the necessary permissions before attempting to modify system drivers.
