..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2015 Intel Corporation.

.. _freebsd_run_apps:

Running Applications on FreeBSD
===============================

The following provides instructions on how to run DPDK applications on FreeBSD.

Compiling a Sample Application
-------------------------------

The DPDK example applications make use of the pkg-config file installed on the system when DPDK is installed, and so can be built using GNU make. BSD make cannot be used to compile the DPDK example applications. GNU make can be installed using ``pkg install gmake`` if not already installed on the FreeBSD system.

Here's how to compile the helloworld example app::

    export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
    cd examples/helloworld/
    gmake

Running a Sample Application
----------------------------

The contigmem and nic_uio modules must be set up prior to running an application. Any ports to be used by the application must be already bound to the nic_uio module, as described in section Binding Network Ports to the nic_uio Module, prior to running the application.

The application is linked with the DPDK target environment’s Environment Abstraction Layer (EAL) library, which provides some options that are generic to every DPDK application.

A large number of options can be given to the EAL when running an application. A full list of options can be got by passing ``--help`` to a DPDK application. Some of the EAL options for FreeBSD are as follows:

- ``-c COREMASK`` or ``-l CORELIST``: A hexadecimal bit mask of the cores to run on. Note that core numbering can change between platforms and should be determined beforehand. The corelist is a list of cores to use instead of a core mask.
- ``-b <domain:bus:devid.func>``: Blocklisting of ports; prevent EAL from using specified PCI device (multiple -b options are allowed).
- ``--use-device``: Use the specified Ethernet device(s) only. Use comma-separate [domain:]bus:devid.func values. Cannot be used with -b option.
- ``-v``: Display version information on startup.
- ``-m MB``: Memory to allocate from hugepages, regardless of processor socket.

Running DPDK Applications Without Root Privileges
-------------------------------------------------

Although applications using the DPDK use network ports and other hardware resources directly, with a number of small permission adjustments, it is possible to run these applications as a user other than “root”. To do so, the ownership, or permissions, on the following file system objects should be adjusted to ensure that the user account being used to run the DPDK application has access to them:

- The userspace-io device files in ``/dev``, for example, ``/dev/uio0``, ``/dev/uio1``, and so on
- The userspace contiguous memory device: ``/dev/contigmem``

Please refer to the `DPDK Release Notes <https://doc.dpdk.org/guides/rel_notes/index.html>`_ for supported applications.