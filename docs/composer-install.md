[![composer](https://www.phpcomposer.com/assets/img/phpcomposer.png)](https://www.phpcomposer.com/)

## Composer 是什么？
> 是 PHP 用来管理依赖（dependency）关系的工具。你可以在自己的项目中声明所依赖的外部工具库（libraries），Composer 会帮你安装这些依赖的库文件。

#### 一、win下的安装
> 在[下载地址](https://getcomposer.org/download/)中找到最新版的exe文件，下载下来，按照安装提示一步一步完成安装，默认会帮你指定你本地安装的php目录，安装完后将composer加入到系统环境变量中，就可以使用composer运行测试啦。

#### 二、linux下的安装
    //下载composer
    curl -sS https://getcomposer.org/installer | php
    //设置linux的环境变量
    mv composer.phar /usr/local/bin/composer
    //改为国内镜像
    composer config -g repo.packagist composer https://packagist.phpcomposer.com
    
#### 三、mac下的安装
> 确定已安装[Homebrew](https://brew.sh/)

    brew install composer
然后在终端输入composer测试,当出现composer图标，说明已安装成功，并加入环境变量