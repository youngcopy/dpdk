..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2015 Intel Corporation.

.. _freebsd_drivers:

FreeBSD Drivers
===============

Before you begin installing and configuring DPDK on FreeBSD, it’s important to make sure your system meets the necessary requirements.

Loading the DPDK contigmem Module
---------------------------------

To run a DPDK application, physically contiguous memory is required. The included sources for the contigmem kernel module provides the ability to present contiguous blocks of memory for the DPDK to use. The contigmem module must be loaded into the running kernel before any DPDK is run. The module is found in the kmod sub-directory of the DPDK target directory.

For more details on how to load the DPDK contigmem module, refer to the `DPDK FreeBSD Getting Started Guide <https://doc.dpdk.org/guides/freebsd_gsg/build_dpdk.html#loading-the-dpdk-contigmem-module>`_.

Loading the DPDK nic_uio Module
-------------------------------

After loading the ``contigmem`` module, the ``nic_uio`` module must also be loaded into the running kernel prior to running any DPDK application. This module must be loaded using the ``kldload`` command as shown below (assuming that the current directory is the DPDK target directory).
::
        kldload ./kmod/nic_uio.ko

For more details on how to load the DPDK nic_uio module, refer to the `DPDK FreeBSD Getting Started Guide <https://doc.dpdk.org/guides/freebsd_gsg/build_dpdk.html#loading-the-dpdk-nic-uio-module>`_.

Binding Network Ports to the nic_uio Module
-------------------------------------------

Device ownership can be viewed using the ``pciconf -l`` command. By default, the FreeBSD kernel will include built-in drivers for the most common devices; a kernel rebuild would normally be required to either remove the drivers or configure them as loadable modules.

To avoid building a custom kernel, the ``nic_uio`` module can detach a network port from its current device driver. This is achieved by setting the ``hw.nic_uio.bdfs`` kernel environment variable prior to loading ``nic_uio``.

For more details on how to bind network ports to the ``nic_uio`` module, refer to the `DPDK FreeBSD Getting Started Guide <https://doc.dpdk.org/guides/freebsd_gsg/build_dpdk.html#binding-network-ports-to-the-nic-uio-module>`_.

Binding Network Ports Back to their Original Kernel Driver
----------------------------------------------------------

If the original driver for a network port has been compiled into the kernel, it is necessary to reboot FreeBSD to restore the original device binding. Before doing so, update or remove the ``hw.nic_uio.bdfs`` in ``/boot/loader.conf``.

For more details on how to bind network ports back to their original kernel driver, refer to the `DPDK FreeBSD Getting Started Guide <https://doc.dpdk.org/guides/freebsd_gsg/build_dpdk.html#binding-network-ports-back-to-their-original-kernel-driver>`_.
