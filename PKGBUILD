# Contributor: phoenixlzx < phoenixlzx at phoenixsec.org >
# Contributor: vorbote

pkgname=vuze
pkgver=4.8.1.2
pkgrel=1
pkgdesc="One of the most powerful bitTorrent client with GUI in the world, written in Java."
arch=('i686' 'x86_64')
url="http://azureus.sf.net/"
license=('GPL')
depends=('java-runtime' 'desktop-file-utils')
optdepends=('libgnomeui: for vuze GUI')
install=vuze.install
options=(!strip)

source=(
  "http://downloads.sourceforge.net/azureus/Vuze_${pkgver:0:1}${pkgver:2:1}${pkgver:4:1}${pkgver:6:1}_linux.tar.bz2")

package() {
  cd "${srcdir}/${pkgname}"

  #install systemwide plugins
  mkdir -p "${pkgdir}/usr/share/vuze"
  cp -a "${srcdir}/${pkgname}/plugins" "${pkgdir}/usr/share/vuze/"
  chown -R root:root "${pkgdir}/usr/share/vuze/plugins"

  #install desktop entries
  install -Dm644 vuze.desktop  "${pkgdir}/usr/share/applications/vuze.desktop"
  install -Dm644 vuze.png "${pkgdir}/usr/share/pixmaps/vuze.png"
  install -Dm644 vuze.torrent.png "${pkgdir}/usr/share/pixmaps/vuze.torrent.png"
  install -Dm644 vuze.schemas "${pkgdir}/usr/share/gconf/schemas/vuze.schemas"

  # install SWT
  if [[ $CARCH == i686 ]] ; then
    install -Dm644 swt/swt32.jar "${pkgdir}/usr/share/vuze/swt32.jar"
  elif [[ $CARCH == x86_64 ]] ; then
    install -Dm644 swt/swt64.jar "${pkgdir}/usr/share/vuze/swt64.jar"
  fi

  # install vuze
  install -Dm755 vuze "${pkgdir}/usr/bin/vuze"
  sed -i 's|#PROGRAM_DIR="/home/username/apps/azureus"|PROGRAM_DIR="/usr/share/vuze"|' ${pkgdir}/usr/bin/vuze
  install -Dm644 Azureus2.jar "${pkgdir}/usr/share/vuze/Azureus2.jar"
}

sha256sums=('47f94e713920c82c334da9d2998e8baa8895582a59c593a97abd8c5d7aa92aa8')
