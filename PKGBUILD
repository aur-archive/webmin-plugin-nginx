# Maintainer: Madalin Ignisca <madalin.ignisca@gmail.com>
# ExMaintainer: Eduard Kracmar <edke.kraken[at]gmail[dot]com>
# Contributor: vbPadre <vbpadre at gmail dot com>

pkgname=webmin-plugin-nginx
pkgver=0.08
pkgrel=1
pkgdesc="Justin Hoffman's Nginx plugin for Webmin"
_pluginname="nginx"
url="http://www.justindhoffman.com/blog/nginx-module/"
license=('gpl')
arch=('i686' 'x86_64')
depends=('webmin')
install=webmin-plugin-${_pluginname}.install
source=(http://www.justindhoffman.com/sites/justindhoffman.com/files/nginx-0.08.wbm__0.gz)
md5sums=('221b8c70d8a04fc9e8a6c51f2cbcaa67')

build() {
    msg "Preparing folders..."
    cd ${srcdir} || return 1
    mkdir -p ${pkgdir}/opt/webmin
    mkdir -p ${pkgdir}/etc/webmin/${_pluginname}
    msg "Copying plugin..."
    cp -rf ${srcdir}/${_pluginname}/ ${pkgdir}/opt/webmin
    msg "Creating config files..."
    touch ${pkgdir}/etc/webmin/${_pluginname}/config
    touch ${pkgdir}/etc/webmin/${_pluginname}/version
    (cat <<EOF
config_dir=/etc/nginx
nginx=nginx
virt_name=
link_dir=/etc/nginx/conf/sites-enabled
mime_types=/etc/nginx/conf/mime.types
stop_cmd=rc.d stop nginx
pid_file=/var/run/nginx.pid
test_nginx=0
virt_dir=/etc/nginx/conf/sites-available
show_order=0
start_cmd=rc.d start nginx
nginx_version=
nginx_dir=/etc/nginx/conf
nginx_conf=/etc/nginx/conf/nginx.conf
test_config=0
apply_cmd=
nginx_path=/usr/sbin/nginx
EOF
) > ${pkgdir}/etc/webmin/${_pluginname}/config
    msg "Aplying Arch Linux fixes..."
    sed -e 's|name=nginx|name=Nginx|g' -i $pkgdir/opt/webmin/${_pluginname}/module.info
    sed -e 's|desc=nginx webserver|desc=Nginx webserver|g' -i $pkgdir/opt/webmin/${_pluginname}/module.info
    sed -e 's|debian-linux|generic-linux|g' -i $pkgdir/opt/webmin/${_pluginname}/module.info
}
