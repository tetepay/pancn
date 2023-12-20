# 极简云盘

#### 资源宝博客

+ 资源宝：https://www.httple.net

#### 介绍
“极简云盘”据说是Veno File Manager 的国内优化汉化版，大小不到1.5M，PHP运行环境，无需数据库支持。在apache环境下，确保.htaccess文件可用，才能启用伪静态规则，否则后台关闭伪静态才能实现文件下载

程序自带多套Material配色主题，带数据统计、用户系统、验证码、SMTP发件、创建文件夹/多文件/密码保护分享链接等功能，支持zip打包下载，音乐视频图片预览。

#### 特点
+ 整个程序包不到1m，极为简小，比一张图片都要小的多
+ 占用内存极小，高效简洁，性能十分出色，是款干净的轻博客程序
+ 无需数据库，不依赖MySQL、Oracle、SQLServer、SQLite等数据库，降低维护成本
+ 后台：/vfm-admin/
+ 账户：admin
+ 密码：123456

#### 环境要求
PHP版本：PHP5.6+ 推荐PHP7.4+

#### 伪静态设置
Nginx环境：
```nginx
location /RELATIVE_PATH {
    index index.php;
    rewrite /download/(.*)/h/(.*)/sh/(.*) /RELATIVE_PATH/vfm-admin/vfm-downloader.php?q=$1&sh=$2 last;
    rewrite /download/(.*)/h/(.*) /RELATIVE_PATH/vfm-admin/vfm-downloader.php?q=$1&h=$2 last;
    rewrite /download/zip/(.*)/n/(.*) /RELATIVE_PATH/vfm-admin/vfm-downloader.php?zip=$1&n=$2 last;
}
```

Apache环境：
```apache
# begin VFM rules
<IfModule mod_rewrite.c>
RewriteEngine on
RewriteCond %{REQUEST_URI}::$1 ^(.*?/)(.*)::\2$
RewriteRule ^(.*)$ - [E=BASE:%1]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule download/(.*)/h/(.*)/sh/(.*) %{ENV:BASE}/vfm-admin/vfm-downloader.php?q=$1&h=$2&sh=$3 [L]
RewriteRule download/(.*)/h/(.*) %{ENV:BASE}/vfm-admin/vfm-downloader.php?q=$1&h=$2 [L]
RewriteRule download/dl/(.*)/pw/(.*) %{ENV:BASE}/vfm-admin/vfm-downloader.php?dl=$1&pw=$2 [L]
RewriteRule download/dl/(.*) %{ENV:BASE}/vfm-admin/vfm-downloader.php?dl=$1 [L]
RewriteRule download/zip/(.*)/n/(.*) %{ENV:BASE}/vfm-admin/vfm-downloader.php?zip=$1&n=$2 [L]
</IfModule>
```
