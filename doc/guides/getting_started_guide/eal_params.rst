..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2014 Intel Corporation.

EAL Parameters
==============

The Environment Abstraction Layer (EAL) provides a set of interfaces and methods for handling the lower-level resources of the host environment. These parameters can be used by any DPDK application running on Linux, FreeBSD, or Windows.

Common EAL Parameters
---------------------

Common EAL parameters are applicable to all platforms supported by DPDK. These parameters include options related to cores, devices, multiprocessing, memory, debugging, and others. For a comprehensive list of common EAL parameters, please refer to the Common EAL Parameters page.

Linux-specific EAL Parameters
-----------------------------

In addition to the common EAL parameters, there are also Linux-specific EAL parameters. These parameters include options related to devices, multiprocessing, memory, and others. For a comprehensive list of Linux-specific EAL parameters, please refer to the :doc:`Linux-specific EAL Parameters <../linux_gsg/linux_eal_parameters>` page.

FreeBSD-specific EAL Parameters
-------------------------------

As of the current DPDK version, there are no FreeBSD-specific EAL parameters. The common EAL parameters are applicable for FreeBSD. For more information, please refer to the :doc:`FreeBSD EAL Parameters <../freebsd_gsg/freebsd_eal_parameters>` page.

Please note that the exact parameters and their usage might vary between different versions of DPDK and the specific operating system in use.
