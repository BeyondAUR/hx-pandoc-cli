# Maintainer: Evan Greenup <_>

_name=pandoc
pkgname=hx-pandoc-cli
pkgver=3.1.12.1
pkgrel=1
pkgdesc="Conversion between documentation formats"
url="https://pandoc.org"
license=("GPL-2.0-or-later")
arch=('x86_64')
provides=('pandoc' 'pandoc-cli')
conflicts=('pandoc' 'pandoc-cli')
replaces=('pandoc' 'pandoc-cli')
depends=()
makedepends=('stack')
source=("https://github.com/jgm/pandoc/archive/refs/tags/3.1.12.1.tar.gz")
sha256sums=('082ae6d88e1df6c0a7c0d60a35d0f63453e41c7e71586a8e86dc3924a6f4cef6')

build() {
  cd "$srcdir/$_pkgname-$pkgver"

  stack build 
}

check() {
  cd $pkgname-$pkgver
  runhaskell Setup test --show-details=direct
}

package() {
  cd $pkgname-$pkgver
  runhaskell Setup copy --destdir="$pkgdir"
  install -D -m644 COPYING.md -t "$pkgdir"/usr/share/licenses/$pkgname/
  rm -f "$pkgdir"/usr/share/doc/$pkgname/COPYING.md

  LD_LIBRARY_PATH="$PWD/dist/build" dist/build/pandoc/pandoc --bash-completion > pandoc-completion.bash
  install -Dm644 pandoc-completion.bash "$pkgdir"/usr/share/bash-completion/completions/pandoc
}

