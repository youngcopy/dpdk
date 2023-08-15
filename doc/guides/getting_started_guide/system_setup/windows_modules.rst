..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2025 Intel Corporation.

.. _windows_modules:

Installing Windows Modules
==========================

Before running DPDK applications on Windows, certain kernel-mode drivers must be 
installed. These drivers are not signed, so signature enforcement must be disabled.
However, be aware that disabling driver signature enforcement can weaken OS security
and is generally discouraged in production environments.

Install Drivers
---------------

Certain kernel-mode drivers are essential to run DPDK applications:

- **virt2phys**: Provides access to physical addresses and is mandatory for allocating physically-contiguous memory, required by hardware PMDs. When loaded successfully, this driver appears in the Device Manager as ``Virtual to physical address translator device`` under the Kernel bypass category. If DPDK cannot communicate with the driver, a warning is printed during initialization.
  
- **NetUIO**: Provides access to device hardware resources and is mandatory for all hardware PMDs, except for the mlx5 PMD. Devices supported by NetUIO are listed in ``netuio.inf``. This list can be extended to try running DPDK with new devices.

After setting up the necessary drivers, proceed to :ref:`windows_run_apps`.