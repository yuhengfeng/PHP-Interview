#### 常用的操作指令
<style>table th:first-of-type { width: 280px;}</style>

| 指令         |  说明    |
|:--------------|:--------------|
| `composer init`  | 根据提示初始化创建composer.json文件 |
| `composer install`  |如有 composer.lock 文件，直接安装，否则从 composer.json 安装最新扩展包和依赖并生成composer.lock；--profile：显示执行时间；--dev：安装到开发环境|
| `composer update`  | 从 composer.json 安装最新扩展包和依赖  composer update vendor/package 更新对应包的配置     |
| `composer require new/package`|添加安装 new/package, 可以指定版本，如： composer require new/package ~2.5.或者composer require "foo/bar:1.0.0"       |
| `composer remove vendor/package`  | 移除 vendor/package包      |
| `composer dump-auto`  |  更新composer的自动加载配置      |