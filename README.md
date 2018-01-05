# ngx_http_image_filter_module_czs
ngx_http_image_filter_module with crop strategy, zoom operation and stretch operation.

Here are three patches:
1. ngx_http_image_filter_crop_strategy.patch; add crop strategy support. There are 4 strategies:
  * center: default, also the standard ngx_http_image_filter_module crop strategy;
  * top: show the top center part of image;
  * smart: center at top quarter position, where most possible eyes located in a standard head picture.
  * smartraw: same strategy with smart but keep the same PPI with raw image (without resize).
2. ngx_http_image_filter_zoom.patch; add zoom operation support. Only zoom in is supported.
3. ngx_http_image_filter_stretch.patch; add stretch operation support.
NOTICE: patch them with numbered order.

I make these patches from nginx 1.2.9, but they can also be patched into nginx 1.12.2 because ngx_http_image_filter_module have only minor changes between these versions;

standard ngx_http_image_filter_module usage should be found at http://nginx.org/en/docs/http/ngx_http_image_filter_module.html.

the additional usage:


Example Configuration

        location ^~ /image {
          set $width $arg_w;
          set_if_empty $width 10000;
          set $height $arg_h;
          set_if_empty $height 10000;
          set $crop $arg_c;
          set_if_empty $crop 1;
          set $zoom $arg_z;
          set_if_empty $zoom 0;

          image_filter zoom $zoom;
          #image_filter crop $width $height $crop;
          image_filter stretch $width $height;
        }


Syntax:
       image_filter zoom percent;
       image_filter crop width height strategy;
       image_filter stretch width height;

* percent: Acceptable values are in the range from 0 to 100, where 0 means zoom disable, and 100 means zero zoom.
* zoom happens before other operations (resize, rotate, streatch, crop).
* in case of wrong width and height of stretch (too big value will generate a monster image), there are internal limits value 200.


###############

这里提供了三份patch，让ngx_http_image_filter_module可以支持不同的裁剪策略并支持变焦和拉伸操作：
1. ngx_http_image_filter_crop_strategy.patch；支持裁剪策略，提供4种不同的策略：
  * center：默认策略，同时也是标准的ngx_http_image_filter_module的裁剪策略；
  * top：展示图片的上部中部位置；
  * smart：中央定位于上部1/4处，对于一张标准头像，这里大概是眼睛的位置；
  * smartraw：裁剪策略与smart相同，但图片最后保持与原图相同的分辨率（不进行缩放）；
2. ngx_http_image_filter_zoom.patch；增加变焦功能，仅支持变焦拉近（放大）；
3. ngx_http_image_filter_stretch.patch；增加拉伸功能；
注意：打补丁时按编号给的顺序打；

这几个patch是从nginx 1.2.9中生成出来的，但因为ngx_http_image_filter_module在版本变化过程中仅有少量修改，所以它们也可以成功打到1.12.2上；

标准的ngx_http_image_filter_module用法可以从http://nginx.org/en/docs/http/ngx_http_image_filter_module.html找到；

补充的用法如下：


配置示例

        location ^~ /image {
          set $width $arg_w;
          set_if_empty $width 10000;
          set $height $arg_h;
          set_if_empty $height 10000;
          set $crop $arg_c;
          set_if_empty $crop 1;
          set $zoom $arg_z;
          set_if_empty $zoom 0;

          image_filter zoom $zoom;
          #image_filter crop $width $height $crop;
          image_filter stretch $width $height;
        }


语法:
       image_filter zoom percent;
       image_filter crop width height strategy;
       image_filter stretch width height;

* percent： 这个参数接受0~100的值，0表示不进行变焦操作，而100表示0变焦（但还是会进行一次图片拷贝）；
* 变焦操作发生在所有其它操作之前（其它操作依次是缩放、旋转、拉伸和裁剪）；
* 为防止拉伸操作时宽高参数出现问题（过大的参数会拉伸出过大的图片），内置了一个200的限制；
