# Maintainer: DrZaius <lou[at]fakeoutdoorsman[dot]com>

pkgname=fdk-aac-git
pkgver=20121222
pkgrel=1
pkgdesc="Fraunhofer FDK AAC codec library"
arch=('i686' 'x86_64')
url="http://sourceforge.net/projects/opencore-amr/"
license=('custom')
depends=('glibc')
options=('!libtool')
conflicts=('fdk-aac')

_gitroot="git://github.com/mstorsjo/fdk-aac.git"
_gitname="fdk-aac"

build() {
  cd "${srcdir}"
  msg "Connecting to the Git repository..."
  
  if [[ -d "${srcdir}/${_gitname}" ]] ; then
    cd "${_gitname}"
    git pull origin
  else
    git clone "${_gitroot}"
  fi
  
  msg "Git clone done"
  msg "Starting make..."
  
  rm -rf "${srcdir}/${_gitname}-build"
  git clone "${srcdir}/${_gitname}" "${srcdir}/${_gitname}-build"
  
  cd "${srcdir}/${_gitname}-build"

  autoreconf -fiv
  ./configure --prefix=/usr
  make
}

package() {
  cd "${srcdir}/${_gitname}-build"
  make DESTDIR="${pkgdir}" install
  install -Dm644 NOTICE "${pkgdir}/usr/share/licenses/${pkgname}/NOTICE"
}
