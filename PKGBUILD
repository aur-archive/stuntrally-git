# Maintainer: Jason Melton <jason.melton@gmail.com>
# Contributer: giacomogiorgianni@gmail.com

pkgname=stuntrally-git
pkgver=20140511
[ "1" = "1" ] && pkgver=`date +"%Y%m%d"`
pkgrel=1
pkgdesc="Stunt Rally game with track editor, based on VDrift and OGRE"
arch=('i686' 'x86_64')
license=('GPL3')
url="http://code.google.com/p/vdrift-ogre"
depends=('boost-libs' 'libogg' 'libvorbis' 'mygui' 'sdl'  'sdl2' 'enet')
makedepends=('git' 'cmake' 'boost')
conflicts=('stuntrally')
replaces=('stuntrally-hg')
md5sums=('SKIP')

_gitname="stuntrally"
_gitroot="https://github.com/stuntrally/stuntrally.git"

_gitname2="tracks"
_gitroot2="https://github.com/stuntrally/tracks.git"

#pkgver() {
#  cd "${srcdir}"
#  git describe --always | sed 's|-|.|g'
#}

_source() 
{
    cd ${srcdir}
    
    msg "Pulling stuntrally files"
    if [ -d ${srcdir}/${_gitname} ] ; then
	    cd ${_gitname} && git pull origin || return 1
    else
        git clone ${_gitroot} --depth=1 || return 1
    fi
    cd ${srcdir}/stuntrally/data 

    msg "Pulling tracks"
    if [ -d ${_gitname2} ]; then
       cd ${_gitname2} && git pull origin || return 1
    else
        git clone ${_gitroot2} --depth=1 || return 1
    fi
}

build() 
{
    _source
    cd ${srcdir}
    rm -rf build
    mkdir build && cd build
    cmake -DCMAKE_INSTALL_PREFIX="${pkgdir}/usr" -DSHARE_INSTALL=share/stuntrally/data ../stuntrally
    make 
}

package() 
{
    cd ${srcdir}/build
    make install
}

