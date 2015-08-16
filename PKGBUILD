# Maintainer: Thibault Suzanne <thi [DOT] suzanne [AT] gmail [DOT] com>

pkgname=mlorg-git
pkgver=20120801
pkgrel=4
pkgdesc="mlorg is a parser for org-mode files written in OCaml"
arch=('any')
url="https://gitorious.org/mlorg"
license=('GPL')
depends=('ocaml' 'ocaml-batteries-git')
makedepends=('git')

_gitroot="https://git.gitorious.org/mlorg/mlorg.git"
_gitname="mlorg"

build () {
  cd $srcdir
  
  msg "Connecting to GIT server..."

  if [[ -d "$srcdir/$_gitname" ]]; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot
  fi

  msg "GIT checkout done or server timeout"

  cd "$srcdir/$_gitname"

  # configure
  ocaml setup.ml -configure --prefix "/usr" --destdir "$pkgdir"

  # build
  ocaml setup.ml -build
}

package () {
  cd "$srcdir/$_gitname"
  
  mkdir ${pkgdir}/usr{,/lib{,/ocaml}}
  OCAMLFIND_DESTDIR="$pkgdir$(ocamlfind printconf destdir)" ocaml setup.ml -install
}
