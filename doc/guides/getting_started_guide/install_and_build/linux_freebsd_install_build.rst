..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2025 Intel Corporation.

.. _linux_freebsd_install_build:

Linux and FreeBSD DPDK Build
============================

.. note::
   The following instructions work for both Linux and FreeBSD, however, if you're using FreeBSD,
   you can also install DPDK from the FreeBSD Ports Collection. 
   See `Installing DPDK from the Ports Collection (FreeBSD)`_ section below for more details.

Grab the DPDK version you want to install and build from ``https://fast.dpdk.org/rel/``.

You can use ``wget`` to grab the DPDK version::

        wget https://fast.dpdk.org/rel/dpdk-<version>.tar.xz

Uncompress the DPDK archive and move to the uncompressed DPDK source directory::

    tar xJf dpdk-<version>.tar.xz
    cd dpdk-<version>

The DPDK source includes several directories such as `doc`, `license`, `lib`, `drivers`, `app`,
`examples`, `config`, `buildtools`, `usertools`, `devtools`, and `kernel`.

DPDK Configuration
------------------

DPDK can be configured, built, and installed on your system using the tools meson and ninja.

To configure a DPDK build, use the following command::

    meson setup <options> build

Here, "build" is the desired output build directory, and "<options>" can be empty or one of a
number of meson or DPDK-specific build options. 

The configuration process will finish with a summary of what DPDK libraries and drivers are to
be built and installed, and for each item disabled, a reason why that is the case.

Building and Installing DPDK System-wide
----------------------------------------

Once configured, to build and then install DPDK system-wide, use the following commands::

    cd build
    ninja
    sudo meson install
    sudo ldconfig

The last two commands generally need to be run as root, or using sudow as shown above.

The ``meson install`` step copies the built objects to their final system-wide locations, 
and the ``ldconfig`` step causes the dynamic loader ``ld.so`` to update its cache to take
account of the new objects.

.. note::
   On some Linux distributions, such as Fedora or Redhat, paths in ``/usr/local`` are not in the
   default paths for the loader. Therefore, on these distributions, ``/usr/local/lib`` and
   ``/usr/local/lib64`` should be added to a file in ``/etc/ld.so.conf.d/`` before running
   ``ldconfig``.

Adjusting Build Options
-----------------------

DPDK has a number of options that can be adjusted as part of the build configuration process.
These options can be listed by running ``meson configure`` inside a configured build folder. 
Many of these options come from the "meson" tool itself and can be seen documented on the
`Meson Website <https://mesonbuild.com/>`_.

For a detailed explanation of the DPDK-specific options, refer to
:doc:`DPDK Meson Build Configuration Options <dpdk_meson_build_options>`.

Installing DPDK from the Ports Collection (FreeBSD)
---------------------------------------------------

DPDK can be installed on FreeBSD via the ``pkg`` package management tool. 
To find the available versions of the DPDK package in your repositories, 
run the following command::

    pkg search dpdk

This will list all available DPDK packages. Each entry in the list represents a version of DPDK
you can install. Note the full name of the version you want to install.

To install a specific version of DPDK, use the ``pkg install`` command, followed by the full
name of the package you noted in the previous step. Here's the general form of the command::

    pkg install <package-name>

Replace `<package-name>` with the name of the DPDK package you want to install. 

For example, if you want to install version `dpdk20.11`, replace `<package-name>` 
with `dpdk20.11`.

Remember to update your repositories regularly with ``pkg update`` so you have access to the
latest versions.

After the installation of the DPDK package, instructions will be printed on how to install the
kernel modules required to use the DPDK. A more complete version of these instructions can be
found in the document :doc:`Loading the DPDK Modules (FreeBSD) <dpdk_module_loading>`.