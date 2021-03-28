# $Id$
# Maintainer: PhotonX <photon89@googlemail.com>
# Contributor: Jan de Groot <jgc@archlinux.org>

pkgname=libbonobo
pkgver=2.32.1
pkgrel=4
pkgdesc="A set of language and system independant CORBA interfaces for creating reusable components"
arch=('i686' 'x86_64' 'arm' 'armv6h' 'armv7h' 'aarch64')
license=('GPL' 'LGPL')
depends=('orbit2' 'libxml2' 'glib2' 'popt')
makedepends=('intltool' 'pkgconfig' 'python')
backup=('etc/bonobo-activation/bonobo-activation-config.xml')
url="http://www.gnome.org"
source=(https://download.gnome.org/sources/libbonobo/2.32/libbonobo-${pkgver}.tar.bz2
		config.guess
        config.sub
		bonobo-activation-config.xml)
install=libbonobo.install
sha256sums=('9160d4f277646400d3bb6b4fa73636cc6d1a865a32b9d0760e1e9e6ee624976b'
			'7d1e3c79b86de601c3a0457855ab854dffd15163f53c91edac54a7be2e9c931b'
			'0c6489c65150773a2a94eebaa794b079e74a403b50b48d5adb69fc6cd14f4810'
            '081de245c42de10ebeea3cbcd819c5ce5d0a15b9bdde9c2098302b1e14965af2')

prepare() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  sed -i "s#-DG_DISABLE_DEPRECATED##" activation-server/Makefile.in
  cp -vf ${srcdir}/config.guess	${srcdir}/${pkgname}-${pkgver}/
  cp -vf ${srcdir}/config.sub	${srcdir}/${pkgname}-${pkgver}/
}

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --sbindir=/usr/bin --sysconfdir=/etc \
              --localstatedir=/var --disable-static \
	      --libexecdir=/usr/lib/bonobo
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  install -m644 "${srcdir}/bonobo-activation-config.xml" "${pkgdir}/etc/bonobo-activation/"
}
