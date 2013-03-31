# Maintainer: Braden Pellett <aur@dabrado.net>

pkgname=simpleopenni-kinect
pkgver=0.27
pkgrel=1
pkgdesc="Processing library for OpenNI and Kinect, including all dependencies."
arch=('i686' 'x86_64')
url="http://code.google.com/p/simple-openni"
license=('GPL2')
depends=('processing' 'openni-git' 'primesense-nite' 'sensorkinect-git')
# java?

source=("http://simple-openni.googlecode.com/files/SimpleOpenNI-${pkgver}.zip" "${pkgname}.install")
sha256sums=('cd0f9d74606c13fa125f45366a15d80b57db61146c676bb631521f9f88ae1fbf'
  'c8f8e6f14399d9a2e417afc00fe82c69bea43966774e76d5125ac9dca8d83536')
install="${pkgname}.install"
if [[ $CARCH == 'i686' ]]; then
  archnum=32
  source+=("http://simple-openni.googlecode.com/files/OpenNI_NITE_Installer-Linux${archnum}-${pkgver}.zip")
  sha256sums+=('21535834990237d754519ec9b305c8bb5cfa81e6e3813942b4d850ad81632d27')
elif [[ $CARCH == 'x86_64' ]]; then
  archnum=64
  source+=("http://simple-openni.googlecode.com/files/OpenNI_NITE_Installer-Linux${archnum}-${pkgver}.zip")
  sha256sums+=('5bc5d87fbc83758ed9d6db12a5d06d71e3bb606c06b7c98dfd9b1a79246c8b65')
fi

package() {
  cd "$srcdir/OpenNI_NITE_Installer-Linux${archnum}-${pkgver}"/OpenNI-Bin-Dev-Linux-*
  install -t "$pkgdir/usr/share/java" Jar/*
  cd "$srcdir/OpenNI_NITE_Installer-Linux${archnum}-${pkgver}"/NITE-Bin-Dev-*
  local nitever="1_5_2"
  install -t "$pkgdir/usr/share/java" Bin/com.primesense.NITE.jar
  install -d "$pkgdir"/etc/primesense/{Features/Data,Hands}
  install -m 644 -t "$pkgdir"/etc/primesense/Features Features_$nitever/Data/*.{ini,dat}
  install -m 644 -t "$pkgdir"/etc/primesense/Features/Data Features_$nitever/Data/Data/*
  install -m 644 -t "$pkgdir"/etc/primesense/Hands Hands_$nitever/Data/*
  cd "$srcdir/OpenNI_NITE_Installer-Linux${archnum}-${pkgver}"/kinect/Sensor-Bin-Linux-*
  install -d "$pkgdir/etc/modprobe.d"
  install -m 644 -t "$pkgdir/etc/modprobe.d" Install/blacklist-gspca-kinect.conf
  cd "$srcdir"
  install -d "$pkgdir"/usr/share/processing/modes/java/libraries
  cp -a SimpleOpenNI "$pkgdir"/usr/share/processing/modes/java/libraries/
}
