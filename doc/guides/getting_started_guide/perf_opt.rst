..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2014 Intel Corporation.

Performance Optimization
========================

Optimizing the performance of DPDK on Intel platforms involves several steps, including hardware and memory requirements, BIOS settings, Linux boot command line configurations, and configurations before running DPDK. This section provides information on how to optimize the performance of DPDK on Linux.

How to get the best performance with NICs on Intel platforms (Linux specific)
-----------------------------------------------------------------------------

For best performance, use an Intel Xeon class server system such as Ivy Bridge, Haswell or newer. Each memory channel should have at least one memory DIMM inserted, and that the memory size for each is at least 4GB. Use a DPDK supported high-end NIC such as the Intel XL710 40GbE. Make sure each NIC has been flashed with the latest version of NVM/firmware. Use PCIe Gen3 slots, such as Gen3 x8 or Gen3 x16 because PCIe Gen2 slots don’t provide enough bandwidth for 2 x 10GbE and above.

In terms of BIOS settings, establish the steady state for the system, consider reviewing BIOS settings desired for best performance characteristic e.g. optimize for performance or energy efficiency. Typically, Performance as the CPU Power and Performance policy is a reasonable starting point. Consider using Turbo Boost to increase the frequency on cores. Disable all virtualization options when you test the physical function of the NIC, and turn on VT-d if you want to use VFIO.

For Linux boot command line configurations, reserve 1G huge pages via grub configurations. Isolate CPU cores which will be used for DPDK. If you want to use VFIO, use the following additional grub parameters: iommu=pt intel_iommu=on.

Before running DPDK, reserve huge pages and check the CPU layout using the DPDK cpu_layout utility or run lscpu to check the cores on each socket. Check your NIC id and related socket id. Check the PCI device related numa node id. Check which kernel drivers need to be loaded and whether there is a need to unbind the network ports from their kernel drivers.

For detailed instructions, please refer to the :doc:`How to get the best performance with NICs on Intel platforms <../linux_gsg/nic_perf_intel_platform>` page.