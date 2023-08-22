..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2025 Intel Corporation.

.. _device_setup:

.. |reg| unicode:: U+000AE

Device Setup
============

Below are instructions for VFIO (Linux) and loading the contigmem module (FreeBSD).

VFIO
----

VFIO is a robust and secure driver that relies on IOMMU protection.
To make use of VFIO on Linux, the ``vfio-pci`` module must be loaded:

.. code-block:: console

    sudo modprobe vfio-pci

VFIO kernel is usually present by default in all distributions,
however please consult your distributions documentation to make sure that is the case.

To make use of full VFIO functionality,
both kernel and BIOS must support and be configured
to use IO virtualization (such as Intel\ |reg| VT-d).

.. note::

   In most cases, specifying "iommu=on" as kernel parameter should be enough to
   configure the Linux kernel to use IOMMU.

For proper operation of VFIO when running DPDK applications as a non-privileged user,
correct permissions should also be set up.
For more information, refer to :ref:`running_dpdk_apps_without_root`.

Refer to :ref:`vfio_no_iommu_mode` when there is no IOMMU available on the system.

Binding and Unbinding Network Ports to/from VFIO-PCI Module
-----------------------------------------------------------

To bind or unbind network ports to/from the `vfio-pci` module on Linux, follow these steps:

Replace ``<module_id>`` with the appropriate module identifier.

**Unbind from Current module**:
   If a device is bound to a kernel driver, unbind it:

   .. code-block:: bash

      dpdk-devbind.py -u <module_id>

**Bind to vfio-pci module**:
   Bind the device to the `vfio-pci` module:

   .. code-block:: bash

      dpdk-devbind.py -b vfio-pci <module_id>

.. _loading_nic_uio_module:

Loading the DPDK nic_uio Module
-------------------------------

After :ref:`loading_contigmem_module` on FreeBSD, the ``nic_uio`` module must also be loaded into the running kernel prior to running any DPDK application, e.g. using::

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

.. _binding_network_ports_nic_uio:

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