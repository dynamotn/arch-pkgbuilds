_gitname=lua-pam
pkgname=lua53-pam-git
pkgver=r3.10613f4
pkgrel=1
pkgdesc='Lua module for PAM authentication'
arch=('x86_64')
url='https://github.com/dynamotn/lua-pam'
depends=('pam' 'lua')
makedepends=('git')
source=("git+${url}.git")
sha256sums=('SKIP')
conflicts=('lua-pam' 'lua-pam-git' 'lua51-pam')

pkgver() {
  cd "$_gitname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd "$_gitname"
  make LUA_VERSION=5.3
}

package() {
  cd "$_gitname"
  install -D pam.so "$pkgdir/usr/lib/lua/5.3/pam.so"
}
