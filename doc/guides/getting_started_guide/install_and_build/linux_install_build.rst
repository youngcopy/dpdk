..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2015 Intel Corporation.

.. _linux_install_build:

Linux DPDK Build
================

Before you begin, make sure you've uncompressed the DPDK archive and moved to the uncompressed DPDK source directory::

        tar xJf dpdk-<version>.tar.xz
        cd dpdk-<version>

The DPDK source includes several directories such as `doc`, `license`, `lib`, `drivers`, `app`, `examples`, `config`, `buildtools`, `usertools`, `devtools`, and `kernel`.

DPDK Configuration
------------------

DPDK can be configured, built, and installed on your system using the tools meson and ninja. To configure a DPDK build, use the following command::

        meson setup <options> build

Here, "build" is the desired output build directory, and "<options>" can be empty or one of a number of meson or DPDK-specific build options. The configuration process will finish with a summary of what DPDK libraries and drivers are to be built and installed, and for each item disabled, a reason why that is the case.

Building and Installing DPDK System-wide
----------------------------------------

Once configured, to build and then install DPDK system-wide, use the following commands::

        cd build
        ninja
        sudo meson install
        sudo ldconfig

The last two commands generally need to be run as root. The ``meson install`` step copies the built objects to their final system-wide locations, and the ``ldconfig`` step causes the dynamic loader ``ld.so`` to update its cache to take account of the new objects.

.. note::
   On some Linux distributions, such as Fedora or Redhat, paths in ``/usr/local`` are not in the default paths for the loader. Therefore, on these distributions, ``/usr/local/lib`` and ``/usr/local/lib64`` should be added to a file in ``/etc/ld.so.conf.d/`` before running ldconfig.

Adjusting Build Options
-----------------------

DPDK has a number of options that can be adjusted as part of the build configuration process. These options can be listed by running ``meson configure`` inside a configured build folder. Many of these options come from the "meson" tool itself and can be seen documented on the `Meson Website <https://mesonbuild.com/>`_.

Building Applications Using Installed DPDK
------------------------------------------

When installed system-wide, DPDK provides a ``pkg-config`` file ``libdpdk.pc`` for applications to query as part of their build. It’s recommended that the ``pkg-config`` file be used, rather than hard-coding the parameters (``cflags``/``ldflags``) for DPDK into the application build process.

An example of how to query and use the ``pkg-config`` file can be found in the Makefile of each of the example applications included with DPDK. A simplified example snippet is shown below::

        PKGCONF = pkg-config
        CFLAGS += -O3 $(shell $(PKGCONF) --cflags libdpdk)
        LDFLAGS += $(shell $(PKGCONF) --libs libdpdk)
        $(APP): $(SRCS-y) Makefile
                $(CC) $(CFLAGS) $(SRCS-y) -o $@ $(LDFLAGS)

.. note::
   Unlike with the make build system present in older DPDK releases, the meson system is not designed to be used directly from a build directory. Instead it is recommended that it be installed either system-wide or to a known location in the user’s home directory. The install location can be set using the ``--prefix`` meson option (default: ``/usr/local``).