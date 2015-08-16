# Contributor: fnord0 < fnord0 AT riseup DOT net >

pkgname=jssfx
pkgver=14
pkgrel=3
pkgdesc="Tool for creating self-extracting compressed JavaScript"
arch=('i686' 'x86_64')
url="http://code.google.com/p/jssfx/"
license=('BSD')
depends=('python2')
_svntrunk="http://jssfx.googlecode.com/svn/trunk/"
provides=('jssfx-svn')

build() {
	  if [ -d ${srcdir}/.svn ]; then
	    msg 'Updating...'
	    svn up ${srcdir}
	  else
	    msg 'Checking out...'
	    svn co ${_svntrunk} ${srcdir}
	  fi
	  mkdir -p ${pkgdir}/usr/{bin,src} || return 1
	  install -d ${pkgdir}/usr/share/licenses/jssfx || return 1
	  cd ${pkgdir}/usr/src
          svn export ${srcdir} ${pkgname} || return 1
	  install -Dm644 ${pkgname}/COPYRIGHT.txt ${pkgdir}/usr/share/licenses/${pkgname}/ || return 1

  #create startup app
  echo "#!/bin/sh" > ${pkgdir}/usr/bin/${pkgname}
  echo "#cd /usr/src/jssfx" >> ${pkgdir}/usr/bin/${pkgname}
  echo "python2 /usr/src/jssfx/JsSfx.py \"\$@\"" >> ${pkgdir}/usr/bin/${pkgname}
  echo "#cd -" >> ${pkgdir}/usr/bin/${pkgname}
  chmod +x ${pkgdir}/usr/bin/${pkgname}
}
# vim:syntax=sh
