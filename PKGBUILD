# Maintainer: Brad Fanella <cesura@archlinux.org>
# Contributor: Martin Wimpress <code@flexion.org>
# Frogged by Georg Lehmann
pkgname=pluma-dad
_pkgname=pluma
pkgver=1.26.0
pkgrel=1
pkgdesc="A powerful text editor for MATE"
url="https://mate-desktop.org"
arch=('x86_64')
license=('GPL')
depends=('iso-codes' 'mate-desktop' 'zenity' 'gtksourceview4' 'libpeas' 'python' 'gettext')
makedepends=('itstool' 'gobject-introspection' 'python' 'mate-common' 'yelp-tools' 'autoconf-archive')
optdepends=('python-gobject: to use the python plugins')
groups=('mate-extra')
conflicts=('pluma-gtk3' $_pkgname)
replaces=('pluma-gtk3' $_pkgname)
source=("https://pub.mate-desktop.org/releases/${pkgver%.*}/${_pkgname}-${pkgver}.tar.xz"
		"newline.patch"
		"3-space.patch")
sha512sums=('a6c0cee7110f4863e44af51b19bb528f0f3570eab8db98038152bf142eedde97ac13b896deff7051b941a0f43c6fe14e316a97eba40fe5d4854d76038450245f'
            'f2a95f72f4030b354e0267857dcd27e0f4717b7facb8bdcecdb399402b7ee6d89c0c76468328a001eecdb2620ad86ac828e1dd62c89a9f60aec55291523aa5d3'
            '48d2d4470706b812fef6d65490eb9f9147685c4b7f1648b8e2667eb54453d7d7ae07b95078b6002dc6a3b50600fd9a55c13abad6adce90fef16638630f9db0c7')

build() {
    	cd "${_pkgname}-${pkgver}"

    	patch -Np1 < "$srcdir"/newline.patch
    	patch -Np1 < "$srcdir"/3-space.patch

    	./autogen.sh
    	PYTHON=/usr/bin/python ./configure \
        	--prefix=/usr \
        	--libexecdir=/usr/lib/${_pkgname} \
        	--enable-gtk-doc=no \
        	--enable-python

    	#https://bugzilla.gnome.org/show_bug.cgi?id=656231
    	sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool

    	make
}

package() {
    	cd "${_pkgname}-${pkgver}"
    	make DESTDIR="${pkgdir}" install
}
