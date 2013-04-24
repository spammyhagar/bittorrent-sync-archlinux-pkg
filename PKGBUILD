pkgname=bittorrent-sync
pkgver=20130424
pkgrel=1
pkgdesc="BitTorrent Sync"
arch=('i686' 'x86_64', 'armv6h')
url="http://labs.bittorrent.com/experiments/sync.html"
license=('custom')
backup=('etc/btsync.conf')
install="${pkgname}.install"
source=("bittorrent-sync.install"
	"bittorrent-sync.service")
sha256sums=("ebf6e87bc4d34612526b8f81993a981a604f3152650d51289c529d236a318d47"
	    "40c16a9d249788494c55362522c7c2760a25758173ee890ea5022f88a1ce1368")

if test "$CARCH" == x86_64; then
	source+=("http://btsync.s3-website-us-east-1.amazonaws.com/btsync_x64.tar.gz")
	sha256sums+=("11d9c1a66134b0aa901fbd578f759f75bb3f3e652a238473240a5c8a7a080c81")
elif test "$CARCH" == i686; then
	source+=("http://btsync.s3-website-us-east-1.amazonaws.com/btsync_i386.tar.gz")
	sha256sums+=("c1d504be14f0a8cc2880a04e4cfeb1786a2bbc923dbc6377a606bf9709887d4e")
elif test "$CARCH" == armv6h; then
	source+=("http://btsync.s3-website-us-east-1.amazonaws.com/btsync_arm.tar.gz")
	sha256sums+=("9a075250460cbc93128a7f4cf353db46165cbc0ebd3b27ed2d05fa6459195c0b")
fi

build() {
	cd "${srcdir}"
	./btsync --dump-sample-config > btsync.conf
}

package() {
	cd "${srcdir}"
	mkdir -p "${pkgdir}/usr/bin"
	mv btsync "${pkgdir}/usr/bin"
  mkdir "${pkgdir}/etc"
	mv btsync.conf "${pkgdir}/etc/btsync.conf"
	mkdir -p "${pkgdir}/usr/lib/systemd/system"
	install -m 644 bittorrent-sync.service "${pkgdir}/usr/lib/systemd/system"
}