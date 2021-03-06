.. highlight:: sh

Fedora
======

.. contents:: Table of Contents
  :local:

Installation
------------

If you want to use ZFS as your root filesystem, see the `Root on ZFS`_
links below instead.

Currently, due to Fedora's unstable fast-paced kernel ABI (kABI), only DKMS style packages can be provided.
As of right now, the following configurations are supported:
  
| **Fedora Releases**: 31, 32
| **Architectures**: x86_64 (amd64)

.. note::
   Due to the release cycle of OpenZFS and Fedora adoption of new kernels in current distribution release, it may happen that you won’t be able to build DKMS package on the most recent kernel update. For example, Fedora 32 was released with kernel 5.6 but it is expected that it will update to 5.7. OpenZFS was released with support for kernel 5.6 but not for 5.7 and there will be no update right after 5.7 will hit Fedora repository. This means that you have to take into account that you will have to either versionlock/pin your kernel and/or build ZFS On Linux from source code (not recommended for beginners). 
   To simplify installation of OpenZFS, a zfs-release package is provided. This package includes a zfs.repo configuration file and the ZFS on Linux public signing key. All official ZFS on Linux packages are signed using this key, and by default, dnf will verify a packages signature before allowing it to be installed unless specified otherwise using ``--nogpgcheck`` or through the ``gpgcheck`` configuration option in dnf.conf or in the repo. Users are strongly encouraged to not disable this feature and to verify the authenticity of the ZFS on Linux public key using the fingerprint listed here.
.. warning::
   The OpenZFS team is not responsible for any damages caused by using ZFS On Linux. By using this software, you are responsible for any and all data loss that occurs. While we may provide user support and bug reporting channels, we are not obliged to help you whatsoever. Please be cautious and understand what you are doing before using OpenZFS.
.. note::
   Please note that on Fedora Rawhide, you MUST use the nodebug kernels. Note that modifying of the OpenZFS source code to spoof GPL is not supported.
 
 You may install the zfs repository using the below commands:
 
.. code:: sh

   $ sudo dnf install http://download.zfsonlinux.org/fedora/zfs-release$(rpm -E %dist).noarch.rpm
   $ gpg --quiet --with-fingerprint /etc/pki/rpm-gpg/RPM-GPG-KEY-zfsonlinux
   pub  2048R/F14AB620 2013-03-21 ZFS on Linux <zfs@zfsonlinux.org>
       Key fingerprint = C93A FFFD 9F3F 7B03 C310  CEB6 A9D5 A1C0 F14A B620
       sub  2048R/99685629 2013-03-21

.. warning::
   If you do not get the same key fingerprint. **STOP**. Your download was most likely corrupt or comprimised. Instead **REMOVE THE ZFS-RELEASE RPM IMMEDIATELY** and try redownloading it and installing or wait for a few days.

The ZFS on Linux packages should be installed with ``dnf`` on Fedora.
Note that it is important to make sure that the matching *kernel-devel*
package is installed for the running kernel since DKMS requires it to
build ZFS.

.. code:: sh

   $ sudo dnf install kernel-devel-$(uname -r) zfs

If the Fedora provided *zfs-fuse* package is already installed on the
system, you must use the ``dnf swap`` command to replace the
existing FUSE packages with the ZFS on Linux packages.

.. code:: sh

   $ sudo dnf swap zfs-fuse zfs

On Fedora, the zfs dracut module must be installed if you wish to use a Root on ZFS configuration.

.. code:: sh

   $ sudo dnf install zfs-dracut

Root on ZFS
-----------
.. toctree::
   :maxdepth: 1
   :glob:

   *


