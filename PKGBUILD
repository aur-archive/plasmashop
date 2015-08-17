# Maintainer: Florian Meißner <developer at mystler dot eu>
pkgname=plasmashop
pkgver=20121203
_commit=ef7f8a48b183b63429beecbc2ce59686fab77009
pkgrel=2
pkgdesc="Swiss army knife for Plasma file hacking"
arch=(any)
url="https://github.com/H-uru/PlasmaShop"
license=('GPL')
depends=('libhsplasma' 'qt' 'glu')
makedepends=('cmake' 'git' 'python2')
install=plasmashop.install
_reponame="PlasmaShop"
_repourl="git://github.com/H-uru/PlasmaShop.git"

build() {
  cd $srcdir
  mkdir python && cd python
  ln -s /usr/bin/python2 python
  export PATH=`pwd`:$PATH

  cd $srcdir
  if [ -d ${_reponame} ]; then
    cd ${_reponame}
    git checkout master
    git fetch origin && git merge origin/master
  else
    git clone ${_repourl} ${_reponame}
    cd ${_reponame}
    git submodule init
  fi

  git reset --hard ${_commit}
  git submodule update

  if [ -d build ]; then
    cd build
    make clean
  else
    mkdir build && cd build
  fi

  cmake -DCMAKE_INSTALL_PREFIX=/usr ..
  make
  rm -R $srcdir/python
}

package() {
  cd $srcdir/${_reponame}/build
  make DESTDIR="$pkgdir/" install
}

# vim:set ts=2 sw=2 et:
