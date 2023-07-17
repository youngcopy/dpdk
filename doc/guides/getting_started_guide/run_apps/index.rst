..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2014 Intel Corporation.

Running Applications
====================

DPDK provides a variety of sample applications which you can use to understand how to use DPDK for your own applications. These sample applications can be found in the examples directory in the DPDK distribution. For detailed instructions on how to compile and run these sample applications, you'll find detailed instructions for each operating system below.


.. toctree::
    :maxdepth: 2
    :hidden:

    linux_run_apps
    freebsd_run_apps
    windows_run_apps

**Linux**

If you're using Linux, running DPDK applications may require additional permissions or privileges. For detailed instructions, please refer to the :doc:`Running DPDK Applications Without Root Privileges <linux_run_apps>` page.

**FreeBSD**

If you're using FreeBSD, running DPDK applications may require additional permissions or privileges. For detailed instructions, please refer to the :doc:`Running DPDK Applications Without Root Privileges <freebsd_run_apps>` page.

**Windows**

On Windows, running DPDK applications requires the "Lock pages in memory" privilege. This privilege allows the DPDK application to keep data in physical memory, preventing the system from paging the data to virtual memory. This can significantly improve the performance of your DPDK applications. For detailed instructions on how to grant this privilege, please refer to the :doc:`Grant Lock pages in memory Privilege <windows_run_apps>` page.

.. note::
   Please note that running DPDK applications may require additional permissions or privileges, depending on your operating system and the specific DPDK features you are using. Always make sure you have the necessary permissions before attempting to run DPDK applications.
