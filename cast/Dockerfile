FROM ubuntu:16.04

RUN apt-get update -y && \
    apt-get install -y make clang vim ffmpeg wget libpcre3 libpcre3-dev openssl libssl-dev && \
    mkdir -p /var/nginx/modules /var/log/nginx/hls /var/lib/nginx/body /var/lib/nginx/proxy /var/lib/nginx/fastcgi && \
    cd /tmp && wget https://github.com/cubicdaiya/nginx-build/releases/download/v0.9.15/nginx-build-linux-amd64-0.9.15.tar.gz && \
    cd /tmp && tar xzf nginx-build-linux-amd64-0.9.15.tar.gz && \
    mv /tmp/nginx-build /usr/local/bin && \
    cd /tmp && wget https://github.com/arut/nginx-rtmp-module/archive/v1.1.11.tar.gz && \
    cd /tmp && tar xzf v1.1.11.tar.gz && \
    mv /tmp/nginx-rtmp-module-1.1.11 /var/nginx/modules && \
    nginx-build -d /tmp/work \
                --sbin-path=/usr/sbin/nginx \
                --conf-path=/etc/nginx/nginx.conf \
                --error-log-path=/var/log/nginx/error.log \
                --pid-path=/var/run/nginx.pid \
                --lock-path=/var/lock/nginx.lock \
                --http-log-path=/var/log/nginx/access.log \
                --http-client-body-temp-path=/var/lib/nginx/body \
                --http-proxy-temp-path=/var/lib/nginx/proxy \
                --with-http_stub_status_module \
                --http-fastcgi-temp-path=/var/lib/nginx/fastcgi \
                --with-debug \
                --with-http_gzip_static_module \
                --with-http_v2_module \
                --with-http_ssl_module \
                --with-pcre-jit \
                --add-module=/var/nginx/modules/nginx-rtmp-module-1.1.11 \
                --with-http_ssl_module && \
    cd /tmp/work/nginx/1.11.11/nginx-1.11.11 && make install

EXPOSE 80 1935

CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
