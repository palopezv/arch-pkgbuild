# Original maintainer: td123 <gostrc at gmail.com>
# Previous maintainer: phoenixlzx < phoenixlzx at phoenixsec.org >
# Maintainer: Vorbote <palopezv at gmail.com>

# This file is provided to under the terms of the BSD 2-clause
# licence. <http://opensource.org/licenses/BSD-2-Clause>

# Patches welcome. Send pull requests to
# https://github.com/vorbote/archlinux-vuze

pkgname=vuze
pkgver=5.0.0.0
pkgrel=3
_ver=${pkgver//./}
_extra=
pkgdesc="The bittorrent kitchen-sink servlet."
provides=("azureus")
arch=('i686' 'x86_64')
url="http://azureus.sf.net/"
license=('GPL')
depends=('java-runtime' 'desktop-file-utils')
optdepends=(
	'xulrunner192: for vuze channels GUI. Long compile ahead.'
	'webkitgtk2: for vuze channels GUI instead of xulrunner192. Crash prone.'
	)
install=vuze.install
options=(!strip)
noextract=("Vuze_"$_ver""$_extra".jar" "azrating_1.4.2.jar")

source=(
  "http://downloads.sourceforge.net/azureus/vuze/Vuze_"$_ver"/Vuze_"$_ver""$_extra"_linux.tar.bz2"
  "http://downloads.sourceforge.net/azureus/vuze/Vuze_"$_ver"/Vuze_"$_ver""$_extra".jar"
  "http://plugins.vuze.com/plugins/azrating_1.4.2.jar")

package() {
  cd "$srcdir/$pkgname"

  #install systemwide plugins
  mkdir -p "$pkgdir"/usr/share/vuze
  cp -a "$srcdir/$pkgname"/plugins "$pkgdir"/usr/share/vuze/

  # Add magnet mimetype to desktop file.
  # This works as shoot-from-the-hip hack but I feel so dirty,
  # I'll go get a shower now.
  #
  # And I missed the magic %U. Thanks j_r0dd for the prodding.
  #
  sed -i.bak -e 's#\(x-bittorrent\)#\1;x-scheme-handler/magnet;#' \
    -e 's#^\(Exec=vuze \)%f#\1%U#' vuze.desktop


  #install desktop entries
  install -Dm644 vuze.desktop  "$pkgdir"/usr/share/applications/vuze.desktop
  install -Dm644 vuze.png "$pkgdir"/usr/share/pixmaps/vuze.png
  install -Dm644 vuze.torrent.png "$pkgdir"/usr/share/pixmaps/vuze.torrent.png
  install -Dm644 vuze.schemas "$pkgdir"/usr/share/gconf/schemas/vuze.schemas

  # install SWT
  if [[ $CARCH == i686 ]] ; then
    install -Dm644 swt/swt32.jar "$pkgdir"/usr/share/vuze/swt32.jar
  elif [[ $CARCH == x86_64 ]] ; then
    install -Dm644 swt/swt64.jar "$pkgdir"/usr/share/vuze/swt64.jar
  fi

  # install vuze
  install -Dm755 vuze "${pkgdir}"/usr/bin/vuze
  sed -i 's|#PROGRAM_DIR="/home/username/apps/azureus"|PROGRAM_DIR="/usr/share/vuze"|' "$pkgdir"/usr/bin/vuze
  # Java and Ruby people are IDIOTS when it comes to creating proper releases.
  #install -Dm644 Azureus2.jar "$pkgdir"/usr/share/vuze/Azureus2.jar
  install -Dm644 "$srcdir"/Vuze_"$_ver""$_extra".jar "$pkgdir"/usr/share/vuze/Azureus2.jar
  # Truly blabbering, stuttering MORONS.
  install -Dm644 "$srcdir"/azrating_1.4.2.jar "$pkgdir"/usr/share/vuze/plugins/azrating/
  
  # Drop garbage
  rm -f "$pkgdir"/usr/share/vuze/plugins/azplugins/azplugins_2.1.6.jar
  rm -f "$pkgdir"/usr/share/vuze/plugins/azupnpav/azupnpav_0.4.4.jar
  rm -f "$pkgdir"/usr/share/vuze/plugins/azrating/azrating_1.3.1.jar
}

sha256sums=('720f51155dbf95674e833d964fe4d2d3356588fe46d8a1df9735d8f29fe5d906'
            '037587fe5180d2488d7db4257afbe8ad32d9dc66a7ad3d1de7b56eb73e9b6569'
            '393b7fd8fec99f799c00b51ea49c0d8b36dce423b32308eeff7c40a9d892b7de')
