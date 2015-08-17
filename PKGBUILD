# Maintainer: Troy C < rstrox -ta yahoo -tod com >

pkgname=python2-supernova-git
pkgver=20130429
pkgrel=3
pkgdesc="Use novaclient with multiple OpenStack nova environments the easy way"
arch=('any')
url="http://github.com/rackerhacker/supernova"
license=('GPL')
depends=('python2' 'python2-novaclient' 'python2-keyring')
makedepends=('git' 'python2-setuptools')
provides=('python2-supernova')
conflicts=('python2-supernova')
_gitroot='https://github.com/rackerhacker/supernova.git'
_gitname='supernova'

build() {
        cd "${srcdir}"
        msg "Connecting to GIT server...."

        if [[ -d "${_gitname}" ]]; then
        cd "${_gitname}" && git pull origin
        msg "The local files are updated."
        else
        git clone "${_gitroot}" "${_gitname}"
        fi

        msg "GIT checkout done or server timeout"
        msg "Starting make..."

        rm -rf "$srcdir/$_gitname-build"
        git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
        REV=$(git show-ref --abbrev --heads | cut -f 1 -d\ )
        python2 setup.py build
}
package() {
        cd "$srcdir/$_gitname-build"
        python2 setup.py install --root=${pkgdir}
}

