#### 为什么要用类的[自动加载](http://www.php.net/manual/zh/language.oop5.autoload.php)
> 在编写面向对象（OOP） 程序时，很多开发者为每个类新建一个 PHP 文件。 这会带来一个烦恼：每个脚本的开头，都需要包含（include）一个长长的列表（每个类都有个文件）。

在php5及以上版本中可以通过`__autoload()`魔术方法来优化加载方法,还有一些指向它的加载函数，例如`spl_autoload_register()`,但是大多数开发者倾向于`spl_autoload_register`函数，两者区别在于：
- `__autoload()`，只能被定义一次，不能作用与多个，没有spl_autoload_register灵活,并且在以后的版本中它可能被弃用
- `spl_autoload_register`提供了一种更加灵活的方式来实现类的自动加载（同一个应用中，可以支持任意数量的加载器，比如第三方库中的）,可以加载自己写的函数来覆盖__autoload()函数
- 两者都不能用户交互模式(俗称命令行模式)

