..  SPDX-License-Identifier: BSD-3-Clause
    Copyright(c) 2010-2025 Intel Corporation.

.. _installing_prebuilt_packages:

Installing Pre-built Packages
=============================

Pre-built packages provide a convenient way to install DPDK without the need to compile
the source code manually. These packages are created and maintained by the DPDK
community or OS vendors and are available for various operating systems and
distributions.

Why Use Pre-built Packages?
---------------------------

- **Ease of Installation**: Pre-built packages simplify the installation process by providing ready-to-use binaries.
- **Compatibility**: Packages are often tested and optimized for specific distributions, ensuring smooth integration with the system.
- **Updates and Maintenance**: Using pre-built packages allows you to benefit from regular updates and maintenance provided by the package maintainers.
- **Time-Saving**: Installing from a pre-built package saves time compared to building from source, especially if you need to install DPDK on multiple systems.

Available Distributions
------------------------

Pre-built DPDK packages are available for several popular Linux distributions,
including but not limited to:

- Alpine

.. code-block:: bash

   sudo apk add dpdk

- Debian and Ubuntu and derivatives

.. code-block:: bash

   sudo apt-get install dpdk

- Fedora and RedHat Enterprise Linux RHEL

.. code-block:: bash

   sudo dnf install dpdk

- FreeBSD

.. code-block:: bash

   sudo pkg install dpdk

- openSUSE

.. code-block:: bash

   sudo zypper install dpdk
