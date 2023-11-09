# $Id$
# Maintainer: BlackIkeEagle <ike DOT devolder AT gmail DOT com>
# Contributor: Philippe Cherel <philippe.cherel@mayenne.org>
# vim: ft=sh:

#  For this to work with kodi using kms which is the expected driver, we can no
#  longer build with RPI support.
#    vc4-kms-v3d exposes CEC through the kernel CEC API (/dev/cec0 and /dev/cec1)
#    vc4-fkms-v3d uses the Pi specific VCHIQ service
#    see https://github.com/raspberrypi/linux/issues/4103

pkgname=libcec-git
epoch=1
pkgver=6.0.2.r4.gf46ecdf
pkgrel=1
pkgdesc="Pulse-Eight's libcec for the Pulse-Eight USB-CEC adapter (Raspberry Pi using kms)"
arch=('armv6h' 'armv7h' 'aarch64')
url="http://libcec.pulse-eight.com/"
license=('GPL')
makedepends=('cmake')
depends=('udev' 'lockdev' 'p8-platform' 'libxrandr')
provides=('libcec')
conflicts=('libcec')
source=('libcec::git+file:////home/nullstring/git/libcec#branch=hacking')
md5sums=('SKIP')

pkgver() {
      cd "$srcdir"/libcec
      git describe --long --tags | sed 's!^libcec-!!;s!\([^-]*-g\)!r\1!;s!-!.!g'
}


build() {
    cd "$srcdir"/libcec

    mkdir -p build
    cd build
    _args=(
#        -DCMAKE_BUILD_TYPE=Release
        -DBUILD_SHARED_LIBS=1
        -DCMAKE_INSTALL_PREFIX=/usr
        -DCMAKE_INSTALL_LIBDIR=/usr/lib
        -DCMAKE_INSTALL_LIBDIR_NOARCH=/usr/lib
        -DHAVE_LINUX_API=1
      )
    cmake "${_args[@]}" ..
    make
}

package() {
    cd "$srcdir"/libcec/build
    make DESTDIR="$pkgdir" install
}
