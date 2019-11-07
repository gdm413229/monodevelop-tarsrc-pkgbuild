# Maintainer: Rae Mochrie <raemochrie@gmail.com>

pkgname=monodevelop-tarsrc
_pkgver_tar=7.8
pkgver=${_pkgver_tar}.4.1
_tarname=monodevelop-${pkgver}.tar.bz2
pkgrel=1
arch=('x86_64')
provides=('monodevelop' 'monodevelop-debugger-gdb')
conflicts=('monodevelop')
replaces=('monodevelop-debugger-gdb')
depends=('mono' 'mono-addins>=0.6.2' 'gtk-sharp-2' 'fsharp-mono-bin' 'libssh2' 'curl' 'msbuild-git')
makedepends=('rsync' 'cmake' 'git' 'nuget' 'openssl-1.0' 'xterm' 'pkgconf' 'autoconf' 'automake')
license=('MIT')
replaces=('')

source=("https://download.mono-project.com/sources/monodevelop/monodevelop-7.8.4.1.tar.bz2")

prepare() {
    
    
    cd "${srcdir}"
    
    bsdtar xf "${_tarname}"
}

build() {
    cd "monodevelop-${_pkgver_tar}"
    # apply that patch that I just made!
    patch -p1 < ../../fix_openssl_error.patch
    ./configure --prefix=/usr 
}

package() {
    XDG_CONFIG_HOME="$srcdir"/config LD_PRELOAD="" make DESTDIR="$pkgdir" install
    # resolve MIME type conflicts
    find "$pkgdir"/usr/share/mime/ -type f -delete
    
    sed -i "s/export LD_LIBRARY_PATH.*/export LD_LIBRARY_PATH\=\"\/usr\/lib\/monodevelop\/bin\:\$\{LD_LIBRARY_PATH\}\"/g" $pkgdir/usr/bin/monodevelop;
  sed -i "s/EXE_PATH=.*/EXE_PATH=\/usr\/lib\/monodevelop\/bin\/MonoDevelop.exe/g" $pkgdir/usr/bin/monodevelop;
}
