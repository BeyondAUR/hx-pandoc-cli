# Maintainer: Evan Greenup <_>

_name=pandoc
pkgname=hx-pandoc-cli
pkgver=3.1.12.3
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
sha256sums=('999b119171b92a5f6697d2dec89df49b629506d0f34976a94fdf35e9ae4c5d0d')

build() {
  cd "$srcdir/$_name-$pkgver"

  stack build pandoc-cli:exe:pandoc
}

check() {
  cd "$srcdir/$_name-$pkgver"

  stack test pandoc-cli:exe:pandoc
}

package() {
  cd "$srcdir/$_name-$pkgver"
  mkdir -m755 -p "${pkgdir}/usr/bin/"
  install -m755 "$(stack path --local-install-root)/bin/pandoc" "${pkgdir}/usr/bin/pandoc"
  install -D -m644 COPYING.md -t "$pkgdir"/usr/share/licenses/$pkgname/

  "${pkgdir}/usr/bin/pandoc" --bash-completion > pandoc-completion.bash
  install -Dm644 pandoc-completion.bash "$pkgdir"/usr/share/bash-completion/completions/pandoc
}

