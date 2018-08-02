#### **`spl_autoload_register`**的使用实例
- 无命名空间同一个目录下，分别有三个文件`MyClass1.class.php`和`MyClass2.class.php`以及入口文件`index.php`

```
class MyClass1
{
    function __construct()
    {
        echo 'This is MyClass1 <br>';
    }
}
class MyClass2
{
    function __construct()
    {
        echo 'This is MyClass2 <br>';
    }
}

index.php文件下:

spl_autoload_register(function ($class_name) {
    require_once $class_name . '.class.php’;
});
$obj1  = new MyClass1();
$obj2  = new MyClass2();

```
运行结果：
```
This is MyClass1 
This is MyClass2
```
结论：其实可以在入口文件将两个类库文件都include进来，就能实例化他们，在类文件少的情况下还好，但是当我们的项目需求越来越多，类文件慢慢增加的情况下，第一中方案肯定是不行的，这样子，我们就可以利用spl_autoload_register函数来灵活的引入大量的类库，并使用他们了。

- 有命名空间，不在同一个目录中的类

目录结构如下：

[![](https://img-blog.csdn.net/20170507000506551)](#)

`Cat.class.php`文件内容:
```
<?php
namespace Animal;
class Cat
{
    function __construct()
    {
        echo 'This is a Cat Class!<br>';
    }
}
```
`Dog.class.php`文件内容:
```

<?php
namespace Animal;
class Dog
{
    function __construct()
    {
        echo 'This is a Dog Class!<br>';
    }
}
```
如果不使用自动加载，按照原有的`require_once`,那么`index.php`文件如下：
```

<?php
 
require_once "Animal/Dog.class.php";
 
$dog = new Dog();

```
使用自动加载:
```

<?php
//自动加载
spl_autoload_register(function ($class_name) {
    $class_name = str_replace('\\','/', $class_name); /*将 use语句中的’\’替换成’/‘，避免造成转移字符导致require_once时会报错*/
    require_once $class_name . '.class.php';        /*文件的后缀名是 .class.php*/
});
use Animal\Dog;
 
$dog = new Dog();
```
运行结果:`This is a Dog Class!`。

- 不同命名空间的类 不同路径的类文件

目录如下：

[![](https://img-blog.csdn.net/20170507000554554)](#)

`ActivityOne.class.php`文件内容:
```
<?php
namespace Logic\Activity;
class ActivityOne
{
    function __destruct()
    {
        echo 'This is a ActivityOne Class！\Logic\Activity\ActivityOne.class.php<br>';
    }
}
```
`index.php`文件内容:
```
<?php
//自动加载
spl_autoload_register(function ($class_name) {
    $class_name = str_replace('\\', '/', $class_name);
    $file_name  = $class_name . '.class.php';
    if (file_exists($file_name)) {
        require_once $file_name;
    }
});
use Animal\Dog;
use Logic\Activity\ActivityOne;
 
$dog = new Dog();
$A   = new ActivityOne();

```
运行结果:
```
This is a Dog Class!
This is a ActivityOne Class！\Logic\Activity\ActivityOne.class.php

```

> 1.命名空间与文件路劲的对应关系：如use Animal\Dog; Dog类的存放路径必须是在Animal文件夹中，否则引入文件是会报错找不到文件。

> 2.类文件的后缀名必须统一：如以’.class.php'结尾
  
  



