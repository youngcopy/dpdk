..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2014 Intel Corporation.

Running Applications
====================

Running DPDK applications involves a few different steps depending on the operating system you're using. Below, you'll find detailed instructions for each operating system.

Running Sample Applications (common for all)
--------------------------------------------

DPDK provides a variety of sample applications which you can use to understand how to use DPDK for your own applications. These sample applications can be found in the examples directory in the DPDK distribution. For detailed instructions on how to compile and run these sample applications, please refer to the :doc:`Running Sample Applications <../sample_app_ug/index>` page.

Running DPDK Applications Without Root Privileges (Linux and FreeBSD specific)
------------------------------------------------------------------------------

For security reasons, you may want to run your DPDK applications without root privileges. This involves some additional configuration steps. For detailed instructions, please refer to the :doc:`Running DPDK Applications Without Root Privileges <../linux_gsg/enable_func>` page.

Grant Lock pages in memory Privilege (Windows specific)
-------------------------------------------------------

On Windows, running DPDK applications requires the "Lock pages in memory" privilege. This privilege allows the DPDK application to keep data in physical memory, preventing the system from paging the data to virtual memory. This can significantly improve the performance of your DPDK applications. For detailed instructions on how to grant this privilege, please refer to the :doc:`Grant Lock pages in memory Privilege <../windows_gsg/run_apps>` page.

Please note that running DPDK applications may require additional permissions or privileges, depending on your operating system and the specific DPDK features you are using. Always make sure you have the necessary permissions before attempting to run DPDK applications.

