# Maintainer: MithicSpirit <rpc01234 at gmail dot com>
# Contributor: Alexander Seiler <seileralex@gmail.com>

_pkgname=sioyek
pkgname="$_pkgname-mupdf-fix"
pkgver=2.0.0
pkgrel=1
pkgdesc='PDF viewer for research papers and technical books'
arch=('x86_64')
license=('GPL3')
url="https://github.com/ahrm/$_pkgname"
depends=('qt5-base' 'zlib' 'harfbuzz' 'libglvnd' 'glibc' 'gcc-libs')
makedepends=('git' 'python' 'unzip' 'qt5-3d' 'glu' 'libxrandr')
conflicts=("$_pkgname" "$_pkgname-git" "$_pkgname-appimage")
provides=("$_pkgname")
source=("$_pkgname::git+https://github.com/ahrm/$_pkgname.git#tag=v$pkgver")
sha256sums=(SKIP)

prepare() {
	cd "$srcdir/$_pkgname"
	sed -i '/#define LINUX_STANDARD_PATHS/s|^//||' pdf_viewer/main.cpp
	git submodule update --init --recursive --jobs "$(nproc)"
	#sed -i 's/-lmupdf-threads/-lfreetype -lgumbo -ljbig2dec -lopenjp2 -ljpeg/' pdf_viewer_build_config.pro
}

build() {
	cd "$srcdir/$_pkgname"
	./build_linux.sh
}

package() {
	cd "$srcdir/$_pkgname"
	install -D "build/$_pkgname" -t "$pkgdir/usr/bin/"
	install -Dm644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname/"
	install -Dm644 "resources/$_pkgname-icon-linux.png" -t "$pkgdir/usr/share/icons/"
	install -Dm644 "resources/$_pkgname.desktop" -t "$pkgdir/usr/share/applications/"
	install -Dm644 build/shaders/* -t "$pkgdir/usr/share/$_pkgname/shaders/"
	install -Dm644 -t "$pkgdir/etc/sioyek/" build/keys.config build/prefs.config
	install -Dm644 -t "$pkgdir/usr/share/man/man1" "resources/$_pkgname.1"
	install -Dm644 -t "$pkgdir/usr/share/$_pkgname" build/tutorial.pdf
}
