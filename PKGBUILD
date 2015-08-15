# Maintainer: bzt <unmacaque at gmail dot com>
# Contributor: bzt <unmacaque at gmail dot com>

pkgname=gnome-xcf-thumbnailer
pkgver=1.0
pkgrel=4
pkgdesc="A thumbnailer for GIMP's own format, XCF files."
arch=('i686' 'x86_64')
url="http://packages.debian.org/sid/gnome-xcf-thumbnailer"
license=('GPL')
depends=('gconf' 'glib2>=2.16' 'libpng12>=1.2.13')
optdepends=('gimp: Required to create thumbnails')
source=("http://ftp.acc.umu.se/pub/gnome/sources/gnome-xcf-thumbnailer/${pkgver}/gnome-xcf-thumbnailer-${pkgver}.tar.bz2"
        "gnome-xcf-thumbnailer.thumbnailer")
install=gnome-xcf-thumbnailer.install
md5sums=('5853d69a19271aa102f1df84e7ccebb6'
         '8c4c02caccc4660881120e6274369ab3')

build() {
  cd ${srcdir}/${pkgname}-${pkgver}
  
  LIBPNG_CFLAGS=-I/usr/include/libpng12 LIBPNG_LIBS=-lpng12 ./configure --prefix=/usr
  
  make
}

package() {
  cd ${srcdir}/${pkgname}-${pkgver}
  
  make DESTDIR=${pkgdir} install
  
  mkdir -p ${pkgdir}/usr/share/thumbnailers
  cp ../gnome-xcf-thumbnailer.thumbnailer ${pkgdir}/usr/share/thumbnailers
  
  install -m755 -d ${pkgdir}/usr/share/gconf/schemas
  gconf-merge-schema ${pkgdir}/usr/share/gconf/schemas/${pkgname}.schemas --domain gnome-xcf-thumbnailer ${pkgdir}/usr/share/${pkgname}/${pkgname}.sc
}
