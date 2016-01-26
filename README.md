Nginx compile
================
Get the latest stable nginx package http://nginx.org/en/linux_packages.html  
for ubuntu
#### Pre compile
```
sudo add-apt-repository ppa:nginx/stable
sudo apt-get update
sudo apt-get install nginx

# Dependencies resolution
apt-get install build-essential
apt-get install libtool
sudo apt-get build-dep nginx

```

#### Compile
```
git clone https://github.com/ligboy/nginx.git
cd ./nginx/nginx

./configure --with-cc-opt='-g -O2 -fstack-protector --param=ssp-buffer-size=4 -Wformat -Werror=format-security -D_FORTIFY_SOURCE=2' --with-ld-opt='-Wl,-Bsymbolic-functions -Wl,-z,relro' --prefix=/usr/share/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --lock-path=/var/lock/nginx.lock --pid-path=/run/nginx.pid --http-client-body-temp-path=/var/lib/nginx/body --http-fastcgi-temp-path=/var/lib/nginx/fastcgi --http-proxy-temp-path=/var/lib/nginx/proxy --http-scgi-temp-path=/var/lib/nginx/scgi --http-uwsgi-temp-path=/var/lib/nginx/uwsgi --with-debug --with-pcre-jit --with-ipv6 --with-http_ssl_module --with-http_stub_status_module --with-http_realip_module --with-http_addition_module --with-http_dav_module --with-http_flv_module --with-http_geoip_module --with-http_gzip_static_module --with-http_image_filter_module --with-http_mp4_module --with-http_perl_module --with-http_random_index_module --with-http_secure_link_module --with-http_spdy_module --with-http_sub_module --with-http_xslt_module --with-mail --with-mail_ssl_module \
--add-module=../modules/headers-more-nginx-module \
--add-module=../modules/ngx_http_auth_pam_module \
--add-module=../modules/ngx_cache_purge \
--add-module=../modules/nginx-dav-ext-module \
--add-module=../modules/ngx_devel_kit \
--add-module=../modules/echo-nginx-module \
--add-module=../modules/ngx-fancyindex \
--add-module=../modules/nginx-push-stream-module \
--add-module=../modules/lua-nginx-module \
--add-module=../modules/nginx-upload-progress-module \
--add-module=../modules/nginx-upstream-fair \
--add-module=../modules/ngx_http_substitutions_filter_module \
--add-module=../modules/ngx_http_google_filter_module   

make && make install
```  
#### Replace the nginx bin
```
# backup
cp /usr/sbin/nginx /usr/sbin/nginx.bak
# replace 
ln -f /usr/share/nginx/sbin/nginx /usr/sbin/nginx
