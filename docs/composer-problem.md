#### 1、关于 composer.lock 文件
> composer.lock 文件里保存着对每一个代码依赖的版本记录（见下图），提交到版本控制器中，并配合 composer install 使用，保证了团队所有协作者开发环境、线上生产环境中运行的代码版本的一致性。

[![composer-lock](https://lccdn.phphub.org/uploads/images/201603/23/1/sATOwsm5oQ.png)](#)

#### 2、关于扩展包的安装方法
> 那么，准备添加一个扩展包，install, update, require 三个命令都可以用来安装扩展包，选择哪一个才是正确的呢？
  
  答案是：使用 composer require 命令
  
另外，在手动修改 composer.json 添加扩展包后，composer update new/package 进行指定扩展包更新的方式，也可以正确的安装，不过不建议使用这种方法，因为，一旦你忘记敲定后面的扩展包名，就会进入万劫不复的状态，别给自己留坑呀。

#### 3、更新指定扩展到指定版本
> 有时候你之前使用过的扩展包，加入了新功能，你想更新单独这个扩展包到指定版本，也可以使用 require 来操作。
  
  如下面例子，需要更新 "sami/sami": "3.0." 到 "sami/sami": "3.2."
  [![](https://lccdn.phphub.org/uploads/images/201604/11/1/UTmjk2UAq4.png)](#)
  
  命令行运行：
  [![](https://lccdn.phphub.org/uploads/images/201604/11/1/jAN0gtPDxf.png)](#)
composer.json 已经被自动更新：
[![](https://lccdn.phphub.org/uploads/images/201604/11/1/LS2nVkGOLy.png)](#)

#### 4、composer require安装的常见问题
- composer require xxx或者 composer update xxx时出现类似于 `The requested package tymont-auth could not be found in any version, there may be a typo in the package name`

> 解决：在composer.json文件中去掉tymont-auth，再次执行composer 操作

#### 5、在上线之前需要优化composer的autoloader
`composer dump-autoload --optimize`
不加这一选项，你可能会发现20%到25%的性能损失