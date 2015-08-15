# Maintainer: Qhor Vertoe <vertoe at qhor dot net>

# Contributor: Noel Maersk <veox at wemakethings dot net>
# Contributor: Florian Léger <florian6 dot leger at laposte dot net>

pkgname=cpuminer-gridseed-git
_gitname=cpuminer
pkgver=291.c57a69a
pkgrel=1
pkgdesc="Multi-threaded CPU miner for Bitcoin and Litecoin (gridseed-git version)"
arch=('any')
url="https://github.com/gridseed/cpuminer"
license=('GPL2')
depends=('curl>=7.34.0' 'jansson')
makedepends=('git' 'autoconf' 'automake' 'yasm')
source=('cpuminer::git+http://github.com/gridseed/cpuminer.git')
md5sums=('SKIP')
backup=(etc/cpuminer.json)

pkgver() {
  cd "${_gitname}"
  echo $(git rev-list --count master).$(git rev-parse --short master)
}

build() {
  cd "$srcdir/${_gitname}"

  # Use in-tree jansson
  # sed -e 's/^AC_CHECK_LIB(jansson, json_loads, request_jansson=false, request_jansson=true)$/request_jansson=true/' -i configure.ac

  autoreconf -fi
  ./configure --prefix=/usr
  make
}

package() {
  cd "$srcdir/${_gitname}"

  make DESTDIR="$pkgdir/" install
  install -Dm600 "example-cfg.json" "$pkgdir/etc/${_gitname}.json"

  find "$pkgdir" -type d -name .git -exec rm -r '{}' +
}
