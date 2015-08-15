# Contributor: Emanuele Rossi newdna1510@yahoo.it
# Contributor: Odites odites@gmal.com
# Contributor: cruznick <cruznick@archlinux.us>
# Contributor: fsckd <fsckdaemon@gmail.com>
# Contributor: XVicarious <bmaurer42@xvicario.us>

pkgname=buc
pkgver=0.5.2
pkgrel=4
pkgdesc="BUC is the program which transforms common bash script in GUI applications written in QT"
arch=('i686' 'x86_64')
url="http://buc.billeragroup.net"
license=('GPL')
groups=('devel')
install=buc.install
depends=('libpng' 'qt4')
source=("http://buc.intilinux.com/download/${pkgname}-${pkgver}_src_full.tar.gz"
        'gcc-fixes.patch'
        'path-fixes.patch'
	'buc-fix.patch')
sha256sums=('9e8951558f838dd655bfb534eabf444274870a6cf7c549bd56e3e11f2ae285d1'  # src
            'a4d384345f659652d40fed9047c262ec03229fd20ec434ae0948c5a1500b1ed7'  # gcc-fixes.patch
            '384efde9a66a7c634830af69a9dc771d03fc0fd290d5b377d437f7091bc5ac5d'  # path-fixes.patch
            'd730e0d3546ce6ad98f9f38c822cad298d6f4a6b8b689144cdb48f3a4bb9a01d'  # buc-fix.patch
)

build() {
   cd "${srcdir}/zip/"

   # removing unnecesary stuff
   rm -v bucd/usr/local/buc/libQtCore.so.4
   rm -v bucd/usr/local/buc/libQtGui.so.4
   rm -v bucd/usr/local/buc/buc

   # patch to facilitate compilation
   patch -Np1 -i  "${srcdir}/gcc-fixes.patch"

   # patch to fix paths (usr/local to usr/share)
   patch -Np1 -i  "${srcdir}/path-fixes.patch"

   # patch to fix dep error in frmMain.cpp (unistd.h)
   patch -Np1 -i  "${srcdir}/buc-fix.patch"

   /usr/lib/qt4/bin/qmake 
   make

   # create dirs and move things to right places
   mkdir -p "${pkgdir}/usr/bin"
   mkdir -p "${pkgdir}/usr/share/buc"

   cp -Rv bucd/usr/share/* "${pkgdir}/usr/share"
   cp -Rv bucd/usr/local/buc/ "${pkgdir}/usr/share"
   cp -Rv bucd/usr/local/bin/ "${pkgdir}/usr/"
   cp -Rv buc "${pkgdir}/usr/share/buc/"
}
