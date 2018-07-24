Usage

        curl -O http://nginx.org/download/nginx-1.12.2.tar.gz
        curl <release url of ngx_http_image_filter_module_czs.tar.gz> -o czs.tar.gz
        docker build -t nginx_http_image_filter:czs .
        docker run -d -p:8080:80 nginx_http_image_filter:czs /usr/local/nginx/sbin/nginx -g "daemon off;"

Result

![image](http://nginx.org/nginx.png)
