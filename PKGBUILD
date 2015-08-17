# Maintainer: Devin J. Pohly <djpohly+arch@gmail.com>
pkgname=sbsms
pkgver=2.0.1
pkgrel=3
pkgdesc="Library for time stretching and pitch scaling of audio"
arch=('i686' 'x86_64')
url="http://sbsms.sourceforge.net/"
license=('GPL')
options=()
source=("http://downloads.sourceforge.net/project/sbsms/$pkgname/$pkgver/lib$pkgname-$pkgver.tar.gz")
md5sums=('409fb6f4f64e48ff1a7bc18621b952fb')

build() {
	cd "$srcdir/lib$pkgname-$pkgver"
	# The `-include stdlib.h' is a workaround to fix upstream.
	./configure --prefix=/usr \
		CXXFLAGS="$CXXFLAGS -include stdlib.h"
	make

	cd test
	# The `-include string.h -pthread' are workarounds to fix upstream.
	./configure --prefix=/usr \
		SBSMS_CFLAGS="-I$srcdir/lib$pkgname-$pkgver/include" \
		SBSMS_LIBS="-L$srcdir/lib$pkgname-$pkgver/src -lsbsms" \
		CXXFLAGS="$CXXFLAGS -I$srcdir/lib$pkgname-$pkgver/include -include string.h -pthread" \
		LDFLAGS="$LDFLAGS -pthread"
	make
}

package() {
	cd "$srcdir/lib$pkgname-$pkgver"
	make DESTDIR="$pkgdir/" install
	make -C test DESTDIR="$pkgdir/" install
	rm "$pkgdir"/usr/lib/libsbsmsx*
}
