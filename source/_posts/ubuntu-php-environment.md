title: "在ubuntu14.04上搭建php、nginx环境"
date: 2015-09-15 17:57:23
tags: php,nginx,php环境,ubuntu
---
记录下在ubuntu14.04上搭建php、nginx环境

先装nginx

```sh
apt-get install nginx
```

接下来是php，不懂php，一大堆先都装上

```sh
sudo apt-get install php5 php5-common php5-mysql php5-curl php5-gd php5-intl php-pear php5-imagick php5-imap php5-mcrypt php5-memcache php5-ming php5-ps php5-pspell php5-recode php5-snmp php5-sqlite php5-tidy php5-xmlrpc php5-xsl php5-xcache php5-mcrypt
```

修改nginx配置

```sh
cd /etc/nginx/sites-available
vim example.com
```

添加下面内容保存
```sh
server {
        listen 80;
        #listen [::]:80 default_server ipv6only=on;

        root /mnt/example; #主机上的网站路径
        index index.php;

        # Make site accessible from http://localhost/
        server_name www.example.com example.com 121.43.159.99;

	if ($host = 'example.com' ) {
		rewrite ^/(.*)$ http://www.example.com/$1 permanent;
	}
	
	if (!-e $request_filename) {
                rewrite  ^(.*)$  /index.php?s=$1  last;
                break;
        }
	location ~* .php {
                fastcgi_split_path_info ^(.+\.php)(/.+)$;
                fastcgi_pass unix:/var/run/php5-fpm.sock;
                fastcgi_index index.php;
                include fastcgi_params;
        } 
}
```
启动php-fpm重启nginx就可以了