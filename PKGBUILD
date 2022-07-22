# Maintainer: Alexander Seiler <seileralex@gmail.com>
pkgname=sioyek
pkgver=1.4.0
pkgrel=2
pkgdesc="PDF viewer for research papers and technical books."
arch=('x86_64')
license=('GPL3')
url="https://github.com/ahrm/sioyek"
depends=(
	'gumbo-parser'
	'harfbuzz'
	'jbig2dec'
	'libmupdf'
	'openjpeg2'
	'qt5-3d'
	'qt5-base'
	'zlib')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz" "mupdf-1.20.patch")
sha256sums=('44d49aec28e49bb79c2d0fb7cefd26aecc53b60136bf02dfec9863ac586aacd0' 'ab9fdffca70d43f1e6d2ba347c546430a79c51452178f05efb086589e247054b')

prepare() {
	cd "$pkgname-$pkgver"
	patch --forward --strip=1 --input="${srcdir}/mupdf-1.20.patch"
	sed -i 's/-lmupdf-threads/-lfreetype -lgumbo -ljbig2dec -lopenjp2 -ljpeg/' pdf_viewer_build_config.pro
	sed -i '/#define LINUX_STANDARD_PATHS/s/\/\///' pdf_viewer/main.cpp
}

build() {
	cd "$pkgname-$pkgver"
	./build_linux.sh
}

package() {
	cd "$pkgname-$pkgver"
	install -D build/sioyek -t "$pkgdir/usr/bin/"
	install -Dm644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname/"
	install -Dm644 resources/sioyek-icon-linux.png -t "$pkgdir/usr/share/icons/"
	install -Dm644 resources/$pkgname.desktop -t "$pkgdir/usr/share/applications/"
	install -Dm644 build/shaders/* -t "$pkgdir/usr/share/$pkgname/shaders/"
	install -Dm644 -t "$pkgdir/etc/sioyek/" build/keys.config build/prefs.config
	install -Dm644 -t "$pkgdir/usr/share/man/man1" resources/sioyek.1
    install -Dm644 -t "$pkgdir/usr/share/sioyek" build/tutorial.pdf
}
