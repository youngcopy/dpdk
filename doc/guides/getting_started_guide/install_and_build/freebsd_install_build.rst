..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2015 Intel Corporation.

.. _freebsd_install_build:

FreeBSD DPDK Build
==================

The easiest way to get up and running with DPDK on FreeBSD is to install it using the FreeBSD ``pkg`` utility or from the ports collection. 

Installing the DPDK Package for FreeBSD
---------------------------------------

DPDK can be installed on FreeBSD via the ``pkg`` package management tool. To find the available versions of the DPDK package in your repositories, run the following command::

    pkg search dpdk

This will list all available DPDK packages. Each entry in the list represents a version of DPDK you can install. Note the full name of the version you want to install.

To install a specific version of DPDK, use the `pkg install` command, followed by the full name of the package you noted in the previous step. Here's the general form of the command::

    pkg install <package-name>

Replace `<package-name>` with the name of the DPDK package you want to install. For example, if you want to install version `dpdk20.11.8`, replace `<package-name>` with `dpdk20.11.8`.

Remember to update your repositories regularly with `pkg update` so you have access to the latest versions.

After the installation of the DPDK package, instructions will be printed on how to install the kernel modules required to use the DPDK. A more complete version of these instructions can be found in the sections `Loading the DPDK contigmem Module`_ and `Loading the DPDK nic_uio Module`_. Normally, lines like those below would be added to the file ``/boot/loader.conf``.

::

        # Reserve 2 x 1G blocks of contiguous memory using contigmem driver:
        hw.contigmem.num_buffers=2
        hw.contigmem.buffer_size=1073741824
        contigmem_load="YES"
        # Identify NIC devices for DPDK apps to use and load nic_uio driver:
        hw.nic_uio.bdfs="2:0:0,2:0:1"
        nic_uio_load="YES"

Installing the DPDK FreeBSD Port
--------------------------------

If so desired, the user can install DPDK using the ports collection rather than from a pre-compiled binary package. On a system with the ports collection installed in ``/usr/ports``, the DPDK can be installed using the commands::

        cd /usr/ports/net/dpdk
        make install

Compiling and Running the Example Applications
----------------------------------------------

When the DPDK has been installed from the ports collection it installs its example applications in ``/usr/local/share/dpdk/examples``. These examples can be compiled and run as described in `Compiling and Running Sample Applications`_.

.. note::

    DPDK example applications must be complied using gmake rather than BSD make. To detect the installed DPDK libraries, ``pkg-config`` should also be installed on the system.

.. note::

    To install a copy of the DPDK compiled using ``gcc``, please download the official DPDK package from https://core.dpdk.org/download/ and install manually using the instructions given in the next chapter, `Compiling the DPDK Target from Source`_.

An example application can therefore be copied to a user’s home directory and compiled and run as below, where we have 2 memory blocks of size 1G reserved via the contigmem module, and 4 NIC ports bound to the ``nic_uio`` module::

        cp -r /usr/local/share/dpdk/examples/helloworld .
        cd helloworld/
        gmake

.. note::

    To run a DPDK process as a non-root user, adjust the permissions on the ``/dev/contigmem`` and ``/dev/uio`` device nodes as described in section `Running DPDK Applications Without Root Privileges`_.

.. note::

    For an explanation of the command-line parameters that can be passed to an DPDK application, see section `Running a Sample Application`_.
