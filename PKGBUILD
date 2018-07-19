pkgname=libsecp256k1-zkp-eos
pkgver=20150529
pkgrel=1
pkgdesc="Optimized C library for EC operations on curve secp256k1 with support for pedersen commitments and range proofs."
arch=('x86_64')
url="https://github.com/cryptonomex/secp256k1-zkp"
makedepends=('autoconf' 'automake' 'git' 'm4' 'make' 'pkg-config')
license=('MIT')
source=(${pkgname%}::git+https://github.com/cryptonomex/secp256k1-zkp)
sha256sums=('SKIP')
provides=('libsecp256k1')
conflicts=('libsecp256k1')

pkgver() {
  cd ${pkgname%}
  git log -1 --format="%cd" --date=short --no-show-signature | sed "s|-||g"
}

build() {
  cd ${pkgname%}

  msg2 'Building...'
  ./autogen.sh
  ./configure \
    --prefix=/usr \
    --sbindir=/usr/bin \
    --libexecdir=/usr/lib/libsecp256k1 \
    --sysconfdir=/etc \
    --sharedstatedir=/usr/share/libsecp256k1 \
    --localstatedir=/var/lib/libsecp256k1 \
    --enable-module-recovery \
    --enable-experimental \
    --enable-module-ecdh \
    --enable-module-schnorr \
    --disable-tests \
    --with-gnu-ld
  make
}

package() {
  cd ${pkgname%}

  msg2 'Installing license...'
  install -Dm 644 COPYING -t "$pkgdir/usr/share/licenses/libsecp256k1"

  msg2 'Installing documentation'
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/libsecp256k1"

  msg2 'Installing...'
  make DESTDIR="$pkgdir" install

  msg2 'Cleaning up pkgdir...'
  find "$pkgdir" -type d -name .git -exec rm -r '{}' +
  find "$pkgdir" -type f -name .gitignore -exec rm -r '{}' +
}
