..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2014 Intel Corporation.

Enabling Additional Functionality
=================================

Enabling additional functionality in DPDK can enhance its performance and usability. This section provides information on how to enable additional functionality on Linux.

Enabling Additional Functionality (Linux specific)
--------------------------------------------------

On Linux, there are several additional functionalities that can be enabled to optimize the performance and usability of DPDK. These include:

- Running DPDK Applications Without Root Privileges: This involves configuring hugepages, adjusting resource limits, and controlling device access. For detailed instructions, please refer to the Running DPDK Applications Without Root Privileges section.

- Power Management and Power Saving Functionality: This involves enabling Enhanced Intel SpeedStep® Technology and C3 and C6 states in the BIOS. For detailed instructions, please refer to the Power Management and Power Saving Functionality section.

- Using Linux Core Isolation to Reduce Context Switches: This involves using Linux kernel parameters to isolate cores from general Linux scheduler tasks. For detailed instructions, please refer to the Using Linux Core Isolation to Reduce Context Switches section.

- High Precision Event Timer (HPET) Functionality: This involves enabling HPET in the BIOS and kernel, and enabling DPDK support for HPET. For detailed instructions, please refer to the High Precision Event Timer (HPET) Functionality section.

Please note that enabling these functionalities may require root privileges or equivalent, depending on your operating system and the specific DPDK features you are enabling. Always make sure you have the necessary permissions before attempting to modify system settings.
