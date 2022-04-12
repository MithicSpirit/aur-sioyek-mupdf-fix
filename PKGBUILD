# Maintainer: Alexander Seiler <seileralex@gmail.com>
pkgname=sioyek
pkgver=1.2.0
pkgrel=1
pkgdesc="PDF viewer for research papers and technical books."
arch=('any')
license=('GPL3')
provides=('sioyek')
url="https://github.com/ahrm/sioyek"
depends=('qt5-base' 'qt5-3d' 'harfbuzz' 'gzip' 'libmupdf' 'zlib' 'gumbo-parser' 'openjpeg2' 'jbig2dec')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('28a67c5e4151a7c71d7fef7ee13c64e8cb928f68594e796e921fdfec2d105b58')

prepare() {
	cd "$pkgname-$pkgver"
	sed -i 's/-lmupdf-third -lmupdf-threads -lharfbuzz/-lmupdf-third -lharfbuzz -lfreetype -lgumbo -ljbig2dec -lopenjp2 -ljpeg/' pdf_viewer_build_config.pro
	sed -i 's/\/\/#define LINUX_STANDARD_PATHS/#define LINUX_STANDARD_PATHS/' pdf_viewer/main.cpp
}

build() {
	cd "$pkgname-$pkgver"
	./build_linux.sh
}

package() {
	cd "$pkgname-$pkgver"
	install -Dm755 ./build/sioyek "$pkgdir/usr/bin/sioyek"

	install -Dm755 ./LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

	install -Dm644 ./resources/sioyek-icon-linux.png "$pkgdir/usr/share/icons/$pkgname-icon-linux.png"
	install -Dm644 ./resources/$pkgname.desktop "$pkgdir/usr/share/applications/$pkgname.desktop"

	mkdir -p "$pkgdir/usr/share/sioyek"
	install -Dm644 -t "$pkgdir/usr/share/sioyek" build/tutorial.pdf
	cp -r build/shaders "$pkgdir/usr/share/sioyek"

	mkdir -p "$pkgdir/etc/sioyek"
	install -Dm644 -t "$pkgdir/etc/sioyek" build/keys.config build/prefs.config

	mkdir -p "$pkgdir/usr/share/man/man1"
	install -Dm644 -t "$pkgdir/usr/share/man/man1" resources/sioyek.1
	gzip "$pkgdir/usr/share/man/man1/sioyek.1"
}
