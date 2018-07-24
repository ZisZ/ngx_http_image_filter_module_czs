#Usage

        curl -O http://nginx.org/download/nginx-1.12.2.tar.gz
        curl <release url of ngx_http_image_filter_module_czs.tar.gz> -o czs.tar.gz
        docker build -t nginx_http_image_filter:czs .
        docker run -d -p:8080:80 nginx_http_image_filter:czs /usr/local/nginx/sbin/nginx -g "daemon off;"

#Result
##origin nginx login with size 352x72
![image](http://nginx.org/nginx.png)

##crop to 64x64 with c1 (same crop logic with origin http_image_filter_module)
![image](https://github.com/ZisZ/ngx_http_image_filter_module_czs/blob/master/docker/pic/nginx_64x64-c1.png)

##crop to 64x64 with c2
![image](https://github.com/ZisZ/ngx_http_image_filter_module_czs/blob/master/docker/pic/nginx_64x64-c2.png)

##crop to 64x64 with c3
![image](https://github.com/ZisZ/ngx_http_image_filter_module_czs/blob/master/docker/pic/nginx_64x64-c3.png)

##crop to 64x64 with c4, result has size 72x72 and the same resolution with origin image
![image](https://github.com/ZisZ/ngx_http_image_filter_module_czs/blob/master/docker/pic/nginx_64x64-c3.png)

##zoom 100 to 128x128 with stretch
![image](https://github.com/ZisZ/ngx_http_image_filter_module_czs/blob/master/docker/pic/nginx_128x128-z100.png)

##zoom 90 to 128x128 with stretch
![image](https://github.com/ZisZ/ngx_http_image_filter_module_czs/blob/master/docker/pic/nginx_128x128-z90.png)

##zoom 80 to 128x128 with stretch
![image](https://github.com/ZisZ/ngx_http_image_filter_module_czs/blob/master/docker/pic/nginx_128x128-z80.png)

##zoom 70 to 128x128 with stretch
![image](https://github.com/ZisZ/ngx_http_image_filter_module_czs/blob/master/docker/pic/nginx_128x128-z70.png)
