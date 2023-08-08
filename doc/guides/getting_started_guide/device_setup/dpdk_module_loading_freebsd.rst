..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2025 Intel Corporation.

.. _dpdk_module_loading:

Loading the DPDK Modules (FreeBSD)
==================================

This document provides instructions on how to load the DPDK `contigmem` and `nic_uio`
modules.

Loading the DPDK contigmem Module
---------------------------------

To run a DPDK application, physically contiguous memory is required. In the absence of
non-transparent superpages, the included sources for the `contigmem` kernel module
provides the ability to present contiguous blocks of memory for the DPDK to use. 
The ``contigmem`` module must be loaded into the running kernel before any DPDK is run.
Once DPDK is installed on the system, the module can be found in the ``/boot/modules``
directory.

The amount of physically contiguous memory along with the number of physically
contiguous blocks to be reserved by the module can be set at runtime prior to module
loading using::

    kenv hw.contigmem.num_buffers=n
    kenv hw.contigmem.buffer_size=m

The kernel environment variables can also be specified during boot by placing the
following in ``/boot/loader.conf``::

    hw.contigmem.num_buffers=n
    hw.contigmem.buffer_size=m

The variables can be inspected using the following command::

    sysctl -a hw.contigmem

The module can then be loaded using ``kldload``::

    kldload contigmem

Loading the DPDK nic_uio Module
-------------------------------

After loading the ``contigmem`` module, the ``nic_uio`` module must also be loaded into
the running kernel prior to running any DPDK application, e.g. using::

    kldload nic_uio

By default, the ``nic_uio`` module will take ownership of network ports if they are
recognized DPDK devices and are not owned by another module. 
However, since the FreeBSD kernel includes support, either built-in, 
or via a separate driver module, for most network card devices,
it is likely that the ports to be used are already bound to a driver other than
``nic_uio``.

To re-bind the ports to the `nic_uio` module upon loading, use the following command::

    kenv hw.nic_uio.bdfs="b:d:f,b:d:f,..."

Where a comma-separated list of selectors is set, the list must not contain any
whitespace.

The variable can also be specified during boot by placing the following into
``/boot/loader.conf``, before the previously-described ``nic_uio_load`` line::

    hw.nic_uio.bdfs="2:0:0,2:0:1"
    nic_uio_load="YES"

Binding Network Ports Back to their Original Kernel Driver
----------------------------------------------------------

If the original driver for a network port has been compiled into the kernel, 
it is necessary to reboot FreeBSD to restore the original device binding. 
Before doing so, update or remove the ``hw.nic_uio.bdfs`` in ``/boot/loader.conf``.

If rebinding to a driver that is a loadable module, the network port binding can be
reset without rebooting. To do so, unload both the target kernel module and the
``nic_uio`` module, modify or clear the ``hw.nic_uio.bdfs`` kernel environment
(``kenv``) value, and reload the two drivers - first the original kernel driver,
and then the ``nic_uio`` driver.

Example commands to perform these steps are shown below::

    kldunload nic_uio
    kldunload <original_driver>
    kenv -u hw.nic_uio.bdfs
    kldload <original_driver>
    kldload nic_uio  # optional