# Contributor: phoenixlzx < phoenixlzx at phoenixsec.org >
# Contributor: vorbote

pkgname=vuze
pkgver=4.8.0.0
pkgrel=2
pkgdesc="One of the most powerful bitTorrent client with GUI in the world, written in Java."
arch=('i686' 'x86_64')
url="http://azureus.sf.net/"
license=('GPL')
depends=('java-runtime' 'desktop-file-utils')
optdepends=('libgnomeui: for vuze GUI')
install=vuze.install
options=(!strip)

source=(
  "http://downloads.sourceforge.net/azureus/Vuze_${pkgver:0:1}${pkgver:2:1}${pkgver:4:1}${pkgver:6:1}.jar"
  "http://downloads.sourceforge.net/azureus/Vuze_${pkgver:0:1}${pkgver:2:1}${pkgver:4:1}${pkgver:6:1}_linux.tar.bz2")
noextract=("Vuze_${pkgver//./}.jar")

md5sums=('a622e3f99c68dbfa7a8c7993afd03f11'
         '17759c2e09d961803b1e3ccc31ff2036')


package() {
  cd "$srcdir/$pkgname"

  #install systemwide plugins
  install -Dm644 plugins/azplugins/azplugins_2.1.6.jar "$pkgdir/usr/share/vuze/plugins/azplugins/azplugins_2.1.6.jar"
  install -Dm644 plugins/azrating/azrating_1.3.1.jar "$pkgdir/usr/share/vuze/plugins/azrating/azrating_1.3.1.jar"
  install -Dm644 plugins/azupdater/Updater.jar "$pkgdir/usr/share/vuze/plugins/azupdater/Updater.jar"
  install -Dm644 plugins/azupdater/azupdaterpatcher_1.8.17.jar "$pkgdir/usr/share/vuze/plugins/azupdater/azupdaterpatcher_1.8.17.jar"
  install -Dm644 plugins/azupdater/azureus.sig "$pkgdir/usr/share/vuze/plugins/azupdater/azureus.sig"
  install -Dm644 plugins/azupdater/plugin.properties "$pkgdir/usr/share/vuze/plugins/azupdater/plugin.properties"
  install -Dm644 plugins/azupnpav/azupnpav_0.4.3.jar "$pkgdir/usr/share/vuze/plugins/azupnpav/azupnpav_0.4.3.jar"
  install -Dm644 plugins/azupnpav/azureus.sig "$pkgdir/usr/share/vuze/plugins/azupnpav/azureus.sig"
  install -Dm644 plugins/azupnpav/plugin.properties "$pkgdir/usr/share/vuze/plugins/azupnpav/plugin.properties"

  #install desktop entries
  install -Dm644 vuze.desktop  "${pkgdir}/usr/share/applications/vuze.desktop"
  install -Dm644 vuze.png "${pkgdir}/usr/share/pixmaps/vuze.png"
  install -Dm644 vuze.torrent.png "${pkgdir}/usr/share/pixmaps/vuze.torrent.png"
  install -Dm644 vuze.schemas "${pkgdir}/usr/share/gconf/schemas/vuze.schemas"

  # install SWT
  if test $CARCH == i686; then
    install -Dm644 swt/swt32.jar "${pkgdir}/usr/share/vuze/swt32.jar"
  fi
  if test $CARCH == x86_64; then
    install -Dm644 swt/swt64.jar "${pkgdir}/usr/share/vuze/swt64.jar"
  fi

  # install vuze
  install -Dm755 vuze "${pkgdir}/usr/bin/vuze"
  sed -i 's|#PROGRAM_DIR="/home/username/apps/azureus"|PROGRAM_DIR="/usr/share/vuze"|' ${pkgdir}/usr/bin/vuze
  install -Dm644 "${srcdir}/Vuze_${pkgver//./}.jar" "${pkgdir}/usr/share/vuze/Azureus2.jar"
}
