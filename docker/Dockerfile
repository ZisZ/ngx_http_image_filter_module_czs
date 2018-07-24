# base image
FROM centos:7

# MAINTAINER
MAINTAINER zky@msn.cn

# put nginx-1.12.2.tar.gz into /usr/local/src and unpack nginx
ADD nginx-1.12.2.tar.gz /usr/local/src

# running required command
RUN yum install -y gcc gcc-c++ glibc make autoconf
RUN yum install -y openssl openssl-devel gd gd-devel
RUN yum install -y curl patch

RUN useradd -M -s /sbin/nologin nginx

# change dir to /usr/local/src/nginx-1.12.2
WORKDIR /usr/local/src/nginx-1.12.2
# get patches
RUN mkdir patches
ADD czs.tar.gz patches
RUN mv patches/*/*.patch patches
RUN patch -p1 < patches/ngx_http_image_filter_crop_strategy.patch
RUN patch -p1 < patches/ngx_http_image_filter_zoom.patch
RUN patch -p1 < patches/ngx_http_image_filter_stretch.patch

# execute command to compile nginx
RUN ./configure\
     --user=nginx\
     --group=nginx\
     --prefix=/usr/local/nginx\
     --with-http_image_filter_module\
    && make && make install

ADD nginx.conf /usr/local/nginx/conf
RUN mkdir /usr/local/nginx/img
RUN curl http://nginx.org/nginx.png -o /usr/local/nginx/img/nginx.png

ENV PATH /usr/local/nginx/sbin:$PATH

EXPOSE 80
