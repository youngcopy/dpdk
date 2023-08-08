..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2015 Intel Corporation.

.. _freebsd_sys_req:

FreeBSD System Requirements
===========================

Before you begin installing and configuring DPDK on FreeBSD, it’s important to make sure your system meets the necessary requirements.

System Requirements
-------------------

- FreeBSD version: DPDK requires FreeBSD 13.2 or later.

- Tools: The following tools are required: ``gmake``, ``gcc`` (optional, can use ``clang`` instead), ``dialog4ports``, ``coreutils``.

- Kernel sources: DPDK requires the FreeBSD kernel sources, which should be included during the installation of FreeBSD on the development platform.

- Ports: DPDK requires the use of FreeBSD ports to compile and function. To update and extract the FreeBSD ports tree, issue the following commands::

        portsnap fetch
        portsnap extract

NICs: DPDK can work with many different types of Network Interface Cards (NICs), but performance can vary. Check the `DPDK NIC compatibility list <http://core.dpdk.org/supported/>`_ to verify your NIC is supported.

Installing Required Ports
-------------------------

The FreeBSD ports below need to be installed prior to building the DPDK. 
In general these can be installed using the following set of commands::

        cd /usr/ports/<port_location>
        make config-recursive
        make install
        make clean

Each port location can be found using::

        whereis <port_name>

The ports required and their locations are as follows:

- dialog4ports: ``/usr/ports/ports-mgmt/dialog4ports``
- GNU make(gmake): ``/usr/ports/devel/gmake``
- coreutils: ``/usr/ports/sysutils/coreutils``

For compiling and using the DPDK with gcc, the compiler must be installed from the
ports collection:

- ``gcc``: version 4.9 is recommended ``/usr/ports/lang/gcc49``. 
Verify that ``CPU_OPTS`` is selected (default is ``OFF``).

Loading the DPDK contigmem Module
---------------------------------

To run a DPDK application, physically contiguous memory is required. 
The included sources for the contigmem kernel module provides the ability to present
contiguous blocks of memory for the DPDK to use. The contigmem module must be loaded
into the running kernel before any DPDK is run. The module is found in the kmod
sub-directory of the DPDK target directory.

For more details on how to load the DPDK contigmem module, 
refer to :ref:`Loading the DPDK Modules (FreeBSD) <dpdk_module_loading>`.

Loading the DPDK nic_uio Module
-------------------------------

After loading the ``contigmem`` module, the ``nic_uio`` module must also be loaded into
the running kernel prior to running any DPDK application. This module must be loaded
using the ``kldload`` command as shown below (assuming that the current directory is
the DPDK target directory).
::
        kldload ./kmod/nic_uio.ko

For more details on how to load the DPDK nic_uio module, refer to
:ref:`Loading the DPDK Modules (FreeBSD) <dpdk_module_loading>`.

Binding Network Ports to the nic_uio Module
-------------------------------------------

Device ownership can be viewed using the ``pciconf -l`` command. By default, 
the FreeBSD kernel will include built-in drivers for the most common devices; 
a kernel rebuild would normally be required to either remove the drivers or configure
them as loadable modules.

To avoid building a custom kernel, the ``nic_uio`` module can detach a network port
from its current device driver. This is achieved by setting the ``hw.nic_uio.bdfs``
kernel environment variable prior to loading ``nic_uio``.

For more details on how to bind network ports to the ``nic_uio`` module, refer to
:ref:`Loading the DPDK Modules (FreeBSD) <dpdk_module_loading>`.

Binding Network Ports Back to their Original Kernel Driver
----------------------------------------------------------

If the original driver for a network port has been compiled into the kernel, 
it is necessary to reboot FreeBSD to restore the original device binding. 
Before doing so, update or remove the ``hw.nic_uio.bdfs`` in ``/boot/loader.conf``.

For more details on how to bind network ports back to their original kernel driver,
refer to :ref:`Loading the DPDK Modules (FreeBSD) <dpdk_module_loading>`.