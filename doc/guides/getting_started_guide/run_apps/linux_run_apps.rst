..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2015 Intel Corporation.

.. _linux_run_apps:

Running Applications on Linux
=============================

DPDK provides a variety of sample applications which you can use to understand how to use DPDK for your own applications. These sample applications can be found in the examples directory in the DPDK distribution.

Compiling and Running Sample Applications
------------------------------------------

To compile and run a sample application, navigate to the application's directory in the DPDK distribution and run the ``make`` command. For example, to compile and run the ``helloworld`` application, you would do the following::

    cd examples/helloworld
    make
    ./build/helloworld -l 0-2

The ``-l`` option specifies the list of cores on which to run the application.

Here are some of the sample applications provided by DPDK:

1. **Hello World Sample Application**: This is the simplest DPDK application that can be written. The application simply prints a "hello world" message. More details can be found `here <https://doc.dpdk.org/guides/sample_app_ug/hello_world.html>`_.

2. **Basic Forwarding Sample Application**: This is a simple skeleton example of a forwarding application. It is intended as a demonstration of the basic components of a forwarding application. More details can be found `here <https://doc.dpdk.org/guides/sample_app_ug/skeleton.html>`_.

3. **Command Line Sample Application**: This application demonstrates the use of the command line interface in DPDK.

4. **Ethtool Sample Application**: This application demonstrates the use of the Ethtool API in DPDK.

For a complete list of sample applications and their detailed user guides, please refer to the `DPDK Sample Applications User Guides <https://doc.dpdk.org/guides/sample_app_ug/index.html>`_.

Running DPDK Applications Without Root Privileges
-------------------------------------------------

For security reasons, you may want to run your DPDK applications without root privileges. This involves some additional configuration steps. Please refer to the `Running DPDK Applications Without Root Privileges guide <linux_run_apps_without_root>` for detailed instructions.