..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2025 Intel Corporation.

.. _memory_setup:

Memory Setup
============

Below are instructions for hugepages support (Linux) and loading the contigmem module (FreeBSD).

Hugepages Support
-----------------

DPDK requires the Linux kernel to support hugepages. This is typically enabled by
default on most modern Linux distributions. To check if hugepages are enabled on your
system, you can run the following command::

        grep HugePages_Total /proc/meminfo

If hugepages are not enabled, you will need to enable them by following these steps:

1. Determine the number of hugepages you want to allocate. For example, to allocate 1024 hugepages of 2MB each, you can use the following command::

        echo 1024 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages

2. To make the hugepages configuration persistent across reboots, add the following line to your `/etc/sysctl.conf` file, adjusting the number of hugepages as needed::

        vm.nr_hugepages = 1024

3. Mount the hugepages filesystem by adding the following line to your `/etc/fstab` file::

        nodev /mnt/huge hugetlbfs defaults 0 0

   Then, create the mount directory and mount the filesystem::

        mkdir -p /mnt/huge
        mount -a

.. _loading_contigmem_module:

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