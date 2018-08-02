#### 一、初始化指令创建composer.json

运行
`
composer init
`
命令
- --name: 包的名称。
- --description: 包的描述。
- --author: 包的作者。
- --homepage: 包的主页。
- --require: 需要依赖的其它包，必须要有一个版本约束。并且应该遵循 foo/bar:1.0.0 这样的格式。
- --require-dev: 开发版的依赖包，内容格式与 --require 相同。
- --stability (-s): minimum-stability 字段的值。
> 当您运行该命令，它会以交互方式要求您填写一些信息，同时聪明的使用一些默认值。

执行完后，会在对应目录下创建composer.json文件

#### 二、手动创建composer.json文件，配置信息如下：
``
{
    "name": "acme/hello-world",
    "require": {
        "monolog/monolog": "1.0.*"
    }
}
``

不管composer.json的文件按以上哪种方式创建，composer.json文件创建后，执行安装

``
composer install
``  
最后会在应用程序目录下创建vendor目录，并在vendor下生产自动加载文件autoload.php
  

   
