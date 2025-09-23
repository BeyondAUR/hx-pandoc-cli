# Maintainer: Evan Greenup <_>

_name=pandoc
pkgname=hx-pandoc-cli
pkgver=3.8
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
sha256sums=('2d375526e7d26d46ebcdaf107564c8bbfd68e40a7af425906e9612889699bcf6')

_stack_resolver=lts-24.9

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

