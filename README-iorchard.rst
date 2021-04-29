Build drbd-utils
==================

This is a guide to build drbd-utils package for debian 11 (bullseye).

Install pre-requisite package.::

   $ sudo apt install -y po4a

Get the drbd-utils and drbd-headers source (drbd-utils depends on drbd-headers
when it is compiled.).::

   $ git clone https://github.com/iorchard/drbd-utils.git
   $ cd drbd-utils

Run autogen.sh.::

   $ ./autogen.sh


   suggested configure parameters:
   # for windrbd (on a cygwin host, assuming C:\windrbd is your windrbd root)
   ./configure --prefix=/cygdrive/c/windrbd/usr --localstatedir=/cygdrive/c/windrbd/var --sysconfdir=/cygdrive/c/windrbd/etc --without-83support --without-84support --without-drbdmon --with-windrbd
   # prepare for rpmbuild, only generate spec files
   ./configure --enable-spec
   # or prepare for direct build
   ./configure --prefix=/usr --localstatedir=/var --sysconfdir=/etc

Build drbd-utils debian package.::

   $ DEB_BUILD_OPTIONS="noprebuiltman" debuild -b -us -uc

Caveat) I need to give noprebuiltman option or compilation is failed.

It takes a long time to build.

The artifacts are in upper directory.::

   $ cd ..
   $ ls drbd-utils*.deb
   drbd-utils_9.17.0-1_amd64.deb  drbd-utils-dbgsym_9.17.0-1_amd64.deb

