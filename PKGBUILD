# Maintainer: Arch Haskell Team <arch-haskell@haskell.org>
_hkgname=open-pandoc
pkgname=haskell-open-pandoc
pkgver=1.5.1.1
pkgrel=3
pkgdesc="Conversion between markup formats"
url="http://hackage.haskell.org/package/${_hkgname}"
license=('GPL')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-http=4000.0.9' 'haskell-bytestring=0.9.1.7' 'haskell-containers=0.3.0.0' 'haskell-directory=1.0.1.1' 'haskell-extensible-exceptions=0.1.1.1' 'haskell-filepath=1.1.0.4' 'haskell-mtl>=1.1' 'haskell-network=2.2.1.7' 'haskell-old-time=1.0.0.5' 'haskell-parsec=2.1.0.1' 'haskell-pretty=1.0.1.1' 'haskell-process=1.0.1.3' 'haskell-syb=0.1.0.2' 'haskell-texmath' 'haskell-utf8-string>=0.3' 'haskell-xhtml=3000.2.0.1' 'haskell-xml<1.4' 'haskell-zip-archive>=0.1.1.4')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
}
md5sums=('1f70c4938907e6a09e5706c56deec997')
