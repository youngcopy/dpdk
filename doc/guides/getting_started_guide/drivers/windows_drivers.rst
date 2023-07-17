..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2015 Intel Corporation.

.. _windows_drivers:

Windows Drivers
===============

Before you begin running DPDK applications on Windows, you'll need to install certain kernel-mode drivers. Please note that these drivers are not signed, so signature enforcement has to be disabled. However, be aware that disabling driver signature enforcement can weaken OS security and is generally discouraged in production environments.

Grant Lock Pages in Memory Privilege
------------------------------------

Use of hugepages ("large pages" in Windows terminology) requires ``SeLockMemoryPrivilege`` for the user running an application. This can be granted through the Local Security Policy snap-in. The privilege is applied upon the next logon. If the privilege has been granted to the current user, a logoff is required before it is available. More details can be found in the `Large-Page Support in MSDN <https://docs.microsoft.com/en-us/windows/win32/memory/large-page-support>`_.

Install Drivers
---------------

The following kernel-mode drivers are required to run DPDK applications:

**virt2phys**: This driver provides access to physical addresses and is mandatory for allocating physically-contiguous memory, which is required by hardware PMDs. When loaded successfully, the driver is shown in Device Manager as ``Virtual to physical address translator device`` under the Kernel bypass category. If DPDK is unable to communicate with the driver, a warning is printed on initialization.

**NetUIO**: This driver provides access to the device hardware resources and is mandatory for all hardware PMDs, except for mlx5 PMD. Devices supported by NetUIO are listed in ``netuio.inf``. The list can be extended in order to try running DPDK with new devices.

For common instructions on system setup, driver build, and installation, refer to the Windows documentation in dpdk-kmods repository <https://github.com/DPDK/dpdk-kmods>_.

Run the helloworld Example
--------------------------

After setting up the drivers, you can run the helloworld example to verify your setup. Navigate to the examples in the build directory and run dpdk-helloworld.exe. The command to run the example is as follows::

    cd C:\\Users\\me\\dpdk\\build\\examples
    dpdk-helloworld.exe -l 0-3

The output should display a hello message from each core.