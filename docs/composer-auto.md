#### [composer的自动加载机制](http://laravelacademy.org/post/7074.html)

##### 自动加载类型：

----

- **`classmap`**     这应该是最最简单的 autoload 模式了。大概的意思就是这样的：
```
{
"classmap": ["src/"]
}
```
然后 composer 在背后就会读取这个文件夹中所有的文件 然后再 `vendor/composer/autoload_classmap.php`中怒将所有的 class 的 namespace + classname 生成成一个 key => value 的 php 数组

- **`psr-0（标准）`**  现在这个标准已经过时了。当初制定这个标准的时候主要是在 php 从 5.2 刚刚跃迁到 5.3+ 有了命名空间的概念。所以这个时候 psr-0 的标准主要考虑到了 <5.2 的 php 中 类似 Acme_Util_ClassName 这样的写法:
```
{
"name": "acme/util",
"auto" : {
"psr-0": {
"Acme\\Util\\": "src/"
}
```

- **`psr-4`** 这个标准出来的时候一片喷声，大概的意思就是 FIG 都是傻逼么，刚刚出了 psr-0 然后紧跟着进推翻了自己。不过 FIG 也有自己的苦衷，帮没有 namespace 支持的 php5.2 擦了那么久的屁股，在2014年10月21日的早晨，终于丢失了睡眠，抛弃了 psr-0 的 composer 从此变得非常清爽。最简单来讲就是可以把 prs-4 的 namespace 直接想想成 file structure 
```
例如
"psr-4": {
"App\\": "app/",
"HenryYu\\": "app/HenryYu"
},
表示 
namespace App\HenryYu\Creators;
自动加载后 可以写成namespace HenryYu\Creators;
```
可以看到将 Acme\Util 指向了 src 之后 psr-4 就会默认所有的 src 下面的 class 都已经有了 Acme\Util 的 基本 namespace，而 psr-4 中不会将 _ 转义成 \ 所以就没有必要有 psr-0 那么深得文档结构了。

- **`file`** 然而这还是不够。因为可能会有一些全局的 helper function 的存在
```
{
"files": [
"path/to/file.php"
]}
```
运行 composer dump-auto就会更新composer的自动加载文件
