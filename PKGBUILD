# Maintainer: Alexander Epaneshnikov <alex19ep@archlinux.org>
# Contributor: Brad Fanella <cesura@archlinux.org>
# Contributor: Martin Wimpress <code@flexion.org>
# Frogged by Georg Lehmann
pkgname=pluma-dad
_pkgname=pluma
pkgver=1.28.0
pkgrel=5
pkgdesc="A powerful text editor for MATE"
url="https://mate-desktop.org"
arch=('x86_64')
license=('GPL-2.0-or-later')
depends=('iso-codes' 'mate-desktop' 'zenity' 'gtksourceview4' 'libpeas' 'python' 'gettext' 'enchant' 'libsm')
makedepends=('itstool' 'git' 'glib2-devel' 'gobject-introspection' 'python' 'mate-common' 'yelp-tools' 'autoconf-archive')
optdepends=('python-gobject: to use the python plugins')
groups=('mate-extra')
conflicts=('pluma-gtk3' $_pkgname)
replaces=('pluma-gtk3' $_pkgname)
source=("git+https://github.com/mate-desktop/pluma.git#tag=v${pkgver}"
        git+https://github.com/mate-desktop/mate-submodules.git
        "newline.patch"
        "3-space.patch")
sha512sums=('df72dcd262802d2dbeaf925466fb5aa6d45f04d6db771154804da52351712b8f3f120ed0438a64c1025c3ede69e4fd2228ea55b93402c1b41aa9890f1bf6618a'
            'SKIP'
            '6685e15abcd8ac55d19324b7ffb89a8e6ab5f29347fc9b7a81442d1a0fc7b1b6e9b6a6cad3fa6dbd85235ee52dce3a0e2e113c5a3ad211c00b5b9b7c844ff455'
            'e82bbfed98f406fd1a29b362c736de8de6131f21d1d4674571334db19d247ccc7d8c71fa2064addf2d42d72dbdd789c68325c756bfb76758195381bb2bc42461')

prepare() {
	cd "${_pkgname}"
	
	patch -Np1 < "$srcdir"/newline.patch
	patch -Np1 < "$srcdir"/3-space.patch
	git submodule init
	git config submodule.mate-submodules.url "${srcdir}/mate-submodules"
	git -c protocol.file.allow=always submodule update
	NOCONFIGURE=1 ./autogen.sh
}

build() {
	cd "${_pkgname}"
	./configure \
	            --prefix=/usr \
	            --libexecdir="/usr/lib/${_pkgname}" \
	            --enable-gtk-doc=no \
	            --enable-python
	make
}

package() {
	cd "${_pkgname}"
	make DESTDIR="${pkgdir}" install
}
