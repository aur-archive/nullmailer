# Maintainer : Martin Wimpress <code@flexion.org>
# Contributor: Kurt J. Bosch <kjb-temp-2009 at alpenjodel.de>
# Contributor: Roberto Alsina <ralsina at kde.org>

pkgname=nullmailer
pkgver=1.13
pkgrel=2
pkgdesc="Simple relay-only mail transport agent."
arch=('i686' 'x86_64')
url="http://www.untroubled.org/nullmailer/"
license=("GPL")
provides=('smtp-forwarder')
conflicts=('smtp-forwarder' 'smtp-server')
depends=('gcc-libs' 'gnutls')
install=nullmailer.install
changelog=nullmailer.changelog
source=("http://www.untroubled.org/nullmailer/archive/${pkgname}-${pkgver}.tar.gz"
        nullmailer.service)
md5sums=('aaeb8746fbc082917b26d0827ccc9270'
         '300f17c52422d4156583f207f2405930')

build() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    ./configure --prefix=/usr \
                --libexecdir=/usr/lib/${pkgname} \
                --sysconfdir=/etc \
                --localstatedir=/var \
                --sbindir=/usr/bin \
                --enable-tls
    make
}

package() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    make DESTDIR="${pkgdir}" install
    install -D -m 0644 ../nullmailer.service "${pkgdir}/usr/lib/systemd/system/nullmailer.service"
    
    # Remove pipe and create on install to work around makepkg hang on grep -R
    rm -f "${pkgdir}/var/nullmailer/trigger"
}
