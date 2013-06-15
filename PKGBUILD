# Original maintainer: td123 <gostrc at gmail.com>
# Previous maintainer: phoenixlzx < phoenixlzx at phoenixsec.org >
# Maintainer: Vorbote <palopezv at gmail.com>

# This file is provided to under the terms of the BSD 2-clause
# licence. <http://opensource.org/licenses/BSD-2-Clause>

# Patches welcome. Send pull requests to
# https://github.com/vorbote/archlinux-vuze

pkgname=vuze
pkgver=5.0.0.0
pkgrel=5
##_ver=${pkgver//./} # Just for reference, this is how it should be done.
_ver=5000 # So people can download the file from the AUR page directly.
_extra= # Extra version used in debotched releases, usually takes months... Or years.
pkgdesc="The bittorrent kitchen-sink servlet."
provides=("azureus")
arch=('i686' 'x86_64')
url="http://azureus.sf.net/"
license=('GPL')
depends=('java-runtime' 'desktop-file-utils')
makedepends=('unzip')
optdepends=(
	'xulrunner192: for vuze channels GUI. Long compile ahead.'
	'webkitgtk2: for vuze channels GUI instead of xulrunner192. Crash prone.'
	'vuze-plugin-mldht: Talk DHT to uTorrent, Transmission, etc.'
	'vuze-plugin-i2p: Use the i2p darknet.'
	)
install=vuze.install
options=(!strip)

## Bunch'o hacks to work around another shoddy release and idiotic
## patching spree after 24 hours of the release. 
## Do they know the meaning of "release engineering"?
noextract=("Vuze_"$_ver""$_extra".jar" "azrating_1.4.2.jar" "azupnpav_0.4.7.zip")

source=(
	 "http://downloads.sourceforge.net/azureus/vuze/Vuze_"$_ver"/Vuze_"$_ver""$_extra"_linux.tar.bz2"
	 "http://downloads.sourceforge.net/azureus/vuze/Vuze_"$_ver"/Vuze_"$_ver""$_extra".jar"
	 "http://plugins.vuze.com/plugins/azrating_1.4.2.jar"
	 "http://plugins.vuze.com/plugins/azupnpav_0.4.7.zip")

package() {
	cd "$srcdir/$pkgname"

        # Create target directories
        install -dm755 "$pkgdir/usr/bin"
        install -dm755 "$pkgdir/usr/share/vuze"
        install -dm755 "$pkgdir/usr/share/applications"
        install -dm755 "$pkgdir/usr/share/gconf/schemas"
        install -dm755 "$pkgdir/usr/share/pixmaps"
        install -dm755 "$pkgdir/usr/share/licenses/$pkgname"


	#install desktop entries
	install -m644 vuze.desktop -t "$pkgdir/usr/share/applications"

	# Add magnet mimetype to desktop file.
	# And I missed the magic %U. Greets to j_r0dd for the prodding.
	sed -i -e 's#\(x-bittorrent\)#\1;x-scheme-handler/magnet;#' \
		-e 's#^\(Exec=vuze \)%f#\1%U#' "$pkgdir/usr/share/applications/vuze.desktop"

	install -pm644 vuze.png -t "$pkgdir/usr/share/pixmaps"
	install -pm644 vuze.torrent.png -t "$pkgdir/usr/share/pixmaps"
	install -pm644 vuze.schemas -t "$pkgdir/usr/share/gconf/schemas"

	# install SWT
	if [[ $CARCH == i686 ]] ; then
		install -pm644 swt/swt32.jar -t "$pkgdir/usr/share/vuze"
	elif [[ $CARCH == x86_64 ]] ; then
		install -pm644 swt/swt64.jar -t "$pkgdir/usr/share/vuze"
	fi

	# install vuze
	install -m755 vuze -t "$pkgdir/usr/bin"
	# Fix internal directory name
	sed -i 's|#PROGRAM_DIR="/home/username/apps/azureus"|PROGRAM_DIR="/usr/share/vuze"|' "$pkgdir/usr/bin/vuze"
	# Sigh... 
	#install -pm644 Azureus2.jar -t "$pkgdir/usr/share/vuze"

	#install systemwide plugins
	cp -a "$srcdir/$pkgname/plugins" "$pkgdir/usr/share/vuze"

	# install the license
	install -pm644 TOS.txt -t "$pkgdir/usr/share/licenses/$pkgname"

	# We really, really shouldn't need anythin below this line.

	# And we've got another botched release.
	install -Dm644 "$srcdir/Vuze_"$_ver""$_extra".jar" "$pkgdir/usr/share/vuze/Azureus2.jar"
	install -dm755 "$pkgdir/usr/share/vuze/plugins/azrating"
	install -pm644 "$srcdir/azrating_1.4.2.jar" -t "$pkgdir/usr/share/vuze/plugins/azrating"
	unzip -qq -o -d "$pkgdir/usr/share/vuze/plugins/azupnpav" "$srcdir/azupnpav_0.4.7.zip"
 
	# I just want to cry.
	rm -f "$pkgdir/usr/share/vuze/plugins/azplugins/azplugins_2.1.6.jar"
	rm -f "$pkgdir/usr/share/vuze/plugins/azrating/azrating_1.3.1.jar"
	rm -f "$pkgdir/usr/share/vuze/plugins/azupnpav/azupnpav_0.4.4.jar"
	rm -f "$pkgdir/usr/share/vuze/plugins/azupnpav/azupnpav_0.4.6.jar"
}

sha256sums=('720f51155dbf95674e833d964fe4d2d3356588fe46d8a1df9735d8f29fe5d906'
            '037587fe5180d2488d7db4257afbe8ad32d9dc66a7ad3d1de7b56eb73e9b6569'
            '393b7fd8fec99f799c00b51ea49c0d8b36dce423b32308eeff7c40a9d892b7de'
            '5ce4ec2787deb44f693170f962c5aaa7a5ebcbb3f1d725c644b4de9fb3346a11')
