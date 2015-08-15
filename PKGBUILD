# Maintainer: Agnotek <agnostic.sn at gmail.com>
# updated from dropbox-experimental

pkgname=dropbox-experimental-agnotek
_pkgname=dropbox
pkgver=3.2.2
pkgrel=0
pkgdesc="A free service that lets you bring your photos, docs, and videos anywhere and share them easily. (Experimental build)"
arch=("i686" "x86_64")
url="http://www.dropbox.com"
license=(custom)
depends=("dbus-glib" "qt5-base" "libsm")
optdepends=(
    'ufw-extras: ufw rules for dropbox'
    'perl-file-mimeinfo: opening dropbox folder on some desktop environments'
)
provides=("dropbox")
conflicts=("dropbox")
options=('!strip' '!upx')

_source_arch="x86"
[ "$CARCH" = "x86_64" ] && _source_arch="x86_64"

sha256sums=('0753e12fecd1af70688d23db2ede6b98bfc2e256d0210139fe08a3c8352f271a'
            'e7d245f5d1a3d5322614b61400ae2913a8caef44bc86717ff7d8197a15dd7f01'
            'dd8fdb362c0bba8d789010594f021671ff00e535fc75e13da855f43bc7a4b3aa'
            '513d7b8395ade6f573b1397acf300326c8dc97e868bca0bc219fb3336b0d4533'
            '2dc647035f4537b7286adb39a71c629353a57f8df03ab81283a3f110579a80aa'
            '1db4b5c19121932d606142642109af4703f211393afe58566c7ec43499d25169')
[ "$CARCH" = "x86_64" ] && sha256sums[0]='1cf30e1841d777b637742607807c6de8f5fffab231cad3db6705774b8f010b3f'

source=("https://d1ilhw0800yew8.cloudfront.net/client/$_pkgname-lnx.$_source_arch-$pkgver.tar.gz"
        "dropbox.png"
        "dropbox.desktop"
        "terms.txt"
        "dropbox.service"
        "dropbox@.service")

package() {
	install -d "$pkgdir"/opt
	cp -R "$srcdir"/.dropbox-dist/dropbox-lnx.$_source_arch-$pkgver "$pkgdir"/opt/dropbox

	find "$pkgdir"/opt/dropbox/ -type f -exec chmod 644 {} \;
	chmod 755 "$pkgdir"/opt/dropbox/dropboxd
	chmod 755 "$pkgdir"/opt/dropbox/dropbox

	install -d "$pkgdir"/usr/bin
	ln -s ../../opt/dropbox/dropboxd "$pkgdir"/usr/bin/dropboxd

	install -Dm644 "$srcdir"/dropbox.desktop "$pkgdir"/usr/share/applications/dropbox.desktop
	install -Dm644 "$srcdir"/dropbox.png "$pkgdir"/usr/share/pixmaps/dropbox.png
	install -Dm644 "$srcdir"/terms.txt "$pkgdir"/usr/share/licenses/$pkgname/terms.txt
	install -Dm644 "$srcdir"/dropbox.service "$pkgdir"/usr/lib/systemd/user/dropbox.service
	install -Dm644 "$srcdir"/dropbox@.service "$pkgdir"/usr/lib/systemd/system/dropbox@.service

	rm -f "$pkgdir"/opt/dropbox/library.zip
	ln -s dropbox "$pkgdir"/opt/dropbox/library.zip
}
