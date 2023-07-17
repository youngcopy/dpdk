..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2015 Intel Corporation.

.. _windows_run_apps:

Running Applications on Windows
===============================

Running DPDK applications on Windows involves a few different steps. This guide provides detailed instructions on how to run the helloworld example application, which can be used as a reference for running other DPDK applications.

Grant Lock Pages in Memory Privilege
------------------------------------

Use of hugepages ("large pages" in Windows terminology) requires ``SeLockMemoryPrivilege`` for the user running an application. This privilege allows the DPDK application to keep data in physical memory, preventing the system from paging the data to virtual memory. This can significantly improve the performance of your DPDK applications.

To grant this privilege:

1. Open Local Security Policy snap-in, either through Control Panel / Computer Management / Local Security Policy, or by pressing Win+R, typing ``secpol``, and pressing Enter.
2. Open Local Policies / User Rights Assignment / Lock pages in memory.
3. Add desired users or groups to the list of grantees.

The privilege is applied upon the next logon. If the privilege has been granted to the current user, a logoff is required before it is available. More details can be found in the `Large-Page Support in MSDN <https://docs.microsoft.com/en-us/windows/win32/memory/large-page-support>`_.

Running the helloworld Example
------------------------------

After setting up the drivers, you can run the helloworld example to verify your setup. Here are the steps:

1. Navigate to the examples in the build directory::

        cd C:\\Users\\me\\dpdk\\build\\examples

2. Run the helloworld application::

        dpdk-helloworld.exe -l 0-3

The output should display a hello message from each core, like this:

::

    hello from core 1
    hello from core 3
    hello from core 0
    hello from core 2
