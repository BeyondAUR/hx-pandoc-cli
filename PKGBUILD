# Maintainer: Evan Greenup <_>

_name=pandoc
pkgname=hx-pandoc-cli
pkgver=3.2
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
source=("${_name}-${pkgver}.tar.gz::https://github.com/jgm/${_name}/archive/refs/tags/${pkgver}.tar.gz")
sha256sums=('063984ad8b410e61e0c0f63e58c68fc1a2a3d79ba1fd73a7a7cc2db4eab0d4d9')

_stack_resolver=lts-22.22

build() {
  cd "$srcdir/$_name-$pkgver"

  stack --resolver=${_stack_resolver} build pandoc-cli:exe:pandoc
}

check() {
  cd "$srcdir/$_name-$pkgver"

  stack --resolver=${_stack_resolver} test pandoc:test:test-pandoc
  stack --resolver=${_stack_resolver} test pandoc-lua-engine:test:test-pandoc-lua-engine
}

package() {
  cd "$srcdir/$_name-$pkgver"
  mkdir -m755 -p "${pkgdir}/usr/bin/"
  install -m755 "$(stack --resolver=${_stack_resolver} path --local-install-root)/bin/pandoc" "${pkgdir}/usr/bin/pandoc"
  install -D -m644 COPYING.md -t "$pkgdir"/usr/share/licenses/$pkgname/

  "${pkgdir}/usr/bin/pandoc" --bash-completion > pandoc-completion.bash
  install -Dm644 pandoc-completion.bash "$pkgdir"/usr/share/bash-completion/completions/pandoc
}

