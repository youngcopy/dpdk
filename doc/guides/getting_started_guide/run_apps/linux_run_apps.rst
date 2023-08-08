..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2015 Intel Corporation.

.. _linux_run_apps:

Running Applications on Linux
=============================

DPDK offers a range of sample applications to help users understand its capabilities.
These applications are located in the examples directory of the DPDK distribution.

Compiling and Running Sample Applications
------------------------------------------

To compile a sample application:

1. Navigate to the application's directory in the DPDK distribution.
2. Execute the ``make`` command.

For instance, to compile the ``helloworld`` application:

::

    cd examples/helloworld
    make

To run the application, use:

::

    ./build/helloworld -l 0-2

The ``-l`` option indicates the cores on which the application should run.

Sample Applications Overview
----------------------------

1. **Hello World**: A basic application that prints a "hello world" message.
2. **Basic Forwarding**: A skeleton example of a forwarding application.
3. **Command Line**: Demonstrates the command line interface in DPDK.
4. **Ethtool**: Showcases the Ethtool API in DPDK.

For a comprehensive list of sample applications and their guides, 
refer to the `DPDK Sample Applications User Guides <https://doc.dpdk.org/guides/sample_app_ug/index.html>`_.

Pre-requisites Before Running Applications
------------------------------------------

Before executing any DPDK application, complete the following:

- Hugepages are set up.
- Relevant Linux modules are loaded.
- Ports used by the application are bound to the appropriate kernel module.

For more details, see :ref:`linux_sys_req` and :ref:`linux_modules`.

EAL Parameters
--------------

Every DPDK application is linked with the DPDK target environment’s 
Environmental Abstraction Layer (EAL) library, which provides generic options. 
Some of these options include:

- ``-c COREMASK`` or ``-l CORELIST``: Specifies the cores to run on.
- ``-n NUM``: Number of memory channels per processor socket.
- ``--socket-mem``: Memory allocation from hugepages on specific sockets.

For a detailed list of EAL options, 
refer to the `EAL parameters section <eal_parameters>`.

Running Without Root Privileges
-------------------------------

TBD
