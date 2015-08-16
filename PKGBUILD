# Contributor: Joseph Pintozzi <joseph.pintozzi@gmail.com>

pkgname=libdlo
pkgver=0.1.2
pkgrel=1
pkgdesc="open-source implementation of DisplayLink USB graphics software"
arch=(i686 x86_64)
url="http://freedesktop.org/wiki/Software/libdlo"
license=('LGPL')
depends=(libusb)
options=(!distcc)
source=(http://people.freedesktop.org/~berniet/libdlo-$pkgver.tar.gz)
md5sums=('a7bb8ec3bdb6ce1d702794de3e4f2112')

build() {
  cd "$srcdir/$pkgname-$pkgver"

  ./configure --prefix=/usr --mandir=/usr/share/man

  sed -i 's#DEFAULT_INCLUDES = -I. -I$(top_builddir)#DEFAULT_INCLUDES = -I. -I$(top_builddir) -I../src#' test/Makefile
  sed -i 's#images/test#/usr/share/libdlo/images/test#' test/test1.c

  make || return 1
  make DESTDIR="$pkgdir/" install || return 1

  mv $pkgdir/usr/bin/test1 $pkgdir/usr/bin/libdlo-test1 && \
  mkdir -p $pkgdir/usr/share/libdlo/ && \
  cp -r test/images $pkgdir/usr/share/libdlo/
}
