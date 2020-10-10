# Maintainer: Brad Fanella <cesura@archlinux.org>
# Contributor: Martin Wimpress <code@flexion.org>
# Frogged by Georg Lehmann
pkgname=pluma-dad
_pkgname=pluma
pkgver=1.24.1
pkgrel=1
pkgdesc="A powerful text editor for MATE"
url="https://mate-desktop.org"
arch=('x86_64')
license=('GPL')
depends=('iso-codes' 'mate-desktop' 'zenity' 'gtksourceview3' 'libpeas' 'python' 'gettext')
makedepends=('itstool' 'gobject-introspection' 'python' 'mate-common' 'yelp-tools' 'autoconf-archive')
optdepends=('python-gobject: to use the python plugins')
groups=('mate-extra')
conflicts=('pluma-gtk3' $_pkgname)
replaces=('pluma-gtk3' $_pkgname)
source=("https://pub.mate-desktop.org/releases/${pkgver%.*}/${_pkgname}-${pkgver}.tar.xz"
		"newline.patch")
sha512sums=('0cfd6a035fc95993dce3e556c49641e799888f20159b29f2c0712c54ee772aa6df1ce755f329414c94efdb2cb3819ce633b92e6559b0c8cb064dab3c74729ab3'
            '01ffc93510d76cdad5227c59a3825e6a8b1f627ae35417c0fca467f77d626e341b2be7a4b3c5fbf594c6c187bf831223259a52c667d8735506a284436057e4b5')

build() {
    	cd "${_pkgname}-${pkgver}"

    	patch -Np1 < "$srcdir"/newline.patch

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
