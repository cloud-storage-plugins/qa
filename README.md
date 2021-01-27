## 💾 云存储插件常见问题

## 关于

作者：沈唁

博客：[qq52o.me](https://qq52o.me)

GitHub：[sy-records](https://github.com/sy-records)

<img src="https://cdn.jsdelivr.net/gh/sy-records/staticfile/images/202012/wechat_white.png" width="400px">

欢迎加入沈唁的云存储全家桶交流QQ群：887595381 [![沈唁的云存储全家桶](https://img.shields.io/badge/QQ%E7%BE%A4-887595381-orange)](https://shang.qq.com/wpa/qunwpa?idkey=24d10d0c318118e5fe2f68a1a7e9f15a7cab40a879fc475849c3726f0d538894)

## Q&A

1. 怎么替换文章中之前的旧资源地址链接

插件中提供了替换数据库中之前的旧资源地址链接功能，只需要填好对应的链接即可。

建议携带`wp-content/uploads`，如：

```txt
https://qq52o.me/wp-content/uploads

https://new.qq52o.me/wp-content/uploads
```

2. 媒体库图片不可见

检查是否存在对应图片文件，是否可以正常访问，以及存储桶权限（公共读 私有写）

3. 保存配置时报错：`您的站点遇到了致命错误，请查看您的站点的管理电子邮箱来获得指引`

这个问题应该只出现在Windows的机器上，打开`WP_DEBUG`的话会报错：`Fatal error: Uncaught GuzzleHttp\Exception\RequestException: cURL error 60: SSL certificate problem: self signed certificate`，解决方法如下：

1）从 [https://curl.haxx.se/ca/cacert.pem](https://curl.haxx.se/ca/cacert.pem) 下载最新的cacert.pem  
2）将以下行添加到`php.ini`中，注意修改对应的路径

```ini
curl.cainfo=/path/to/cacert.pem
```

4. 上传时报错：上传时发生了错误，请稍后再试

在网站根目录的`wp-config.php`中打开`WP_DEBUG`，查看具体错误信息。

5. A TimThumb error has occured

> 此问题也会导致图片资源不可见

完整报错如下：

```txt
A TimThumb error has occured
The following error(s) occured:
You may not fetch images from that site. To enable this site in timthumb, you can either add it to $ALLOWED_SITES and set ALLOW_EXTERNAL=true. Or you can set ALLOW_ALL_EXTERNAL_SITES=true, depending on your security needs.
```

部分主体使用了TimThumb，所以访问的地址是`timthumb.php?src=xxx`，需要修改`timthumb.php`文件，在`$ALLOWED_SITES`加入对应的域名

6. 报错：Call to undefind function get_home_path()

修改插件文件，加入以下代码

```php
if (!function_exists('get_home_path')) {
    require_once(ABSPATH . 'wp-admin/includes/file.php');
}
```

## 赞赏

<img src="https://cdn.jsdelivr.net/gh/sy-records/staticfile/images/donate.png" width="400px">
