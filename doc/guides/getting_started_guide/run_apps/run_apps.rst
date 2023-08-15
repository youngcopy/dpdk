..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2025 Intel Corporation.

.. _run_apps:

Running Applications
====================

The following instructions apply to Linux, FreeBSD, and Windows.

Compiling a Sample Application
-------------------------------

The DPDK example applications make use of the pkg-config file installed on the system
when DPDK is installed, and so can be built using GNU make. 
BSD make cannot be used to compile the DPDK example applications. 
GNU make can be installed using ``pkg install gmake`` if not already installed on the
FreeBSD system.

Here's how to compile the helloworld example app::

    export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
    cd examples/helloworld/
    gmake

Running a Sample Application
----------------------------

The :ref:`contigmem <loading_contigmem_module>` and :ref:`nic_uio modules <loading_nic_uio_module>` must be set up prior to running an application. 
Any ports to be used by the application must be already bound to the nic_uio module, 
as described in section :ref:`Binding Network Ports to the nic_uio Module <binding_network_ports_nic_uio>`, 
prior to running the application.

The application is linked with the DPDK target environment’s Environment Abstraction
Layer (EAL) library, which provides some options that are generic to every DPDK
application.

A large number of options can be given to the EAL when running an application. 
A full list of options can be got by passing ``--help`` to a DPDK application. 
Some of the EAL options for FreeBSD are as follows:

- ``-c COREMASK`` or ``-l CORELIST``: A hexadecimal bit mask of the cores to run on. Note that core numbering can change between platforms and should be determined beforehand. The corelist is a list of cores to use instead of a core mask.
- ``-b <domain:bus:devid.func>``: Blocklisting of ports; prevent EAL from using specified PCI device (multiple -b options are allowed).
- ``--use-device``: Use the specified Ethernet device(s) only. Use comma-separate [domain:]bus:devid.func values. Cannot be used with -b option.
- ``-v``: Display version information on startup.
- ``-m MB``: Memory to allocate from hugepages, regardless of processor socket.
