基本编码标准
=====================

标准的这一节包含了应该被考虑到的编码元素，这些元素保证分享的PHP代码达到高水平的技术协议。

关键字”必须“，”禁止“，”需要“，”建议”，“不建议”，“会”，“不会”，“建议”，“可以”和“可选”会
被用到。
（原文：The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119].）


[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md


1. 概览
-----------

- 文件必须使用`<?php` 和 `<?=` 作为PHP代码部分开头.

- 文件必须使用UTF-8编码，并且没有BOM。

- 文件应该要么申明类型（类、函数、常量等），要么引起副作用（输出、修改ini配置等），同一个文件中不应该同时出现这两种。

- 命名空间和类必须遵守“autoloading”规范：[[PSR-0], [PSR-4]].

- 类名必须是以大写字母开头的驼峰，如：`StudlyCaps`。

- 常亮必须为全部大写，并使用下划线分割。

- 方法（函数）名必须声明为小写字母开头的驼峰，如：`camelCase`。


2. 文件
--------

### 2.1. PHP 标签

PHP code MUST use the long `<?php ?>` tags or the short-echo `<?= ?>` tags; it
MUST NOT use the other tag variations.
PHP代码必须使用`<?php ?>`或 `<? ?>`；禁止使用其它标签。

### 2.2. 字符编码

PHP代码必须使用UTF-8编码，并且文件不含BOM。

### 2.3. 副作用

一个文件应该申明类型并且不产生副作用，或者仅产生副作用并且不包含逻辑代码，总之，两件事不能同时发生。

短语“副作用”表示，逻辑的执行不直接关系到类、函数、常量的声明。仅仅限制于载入的文件。

“副作用”包含但不限制于：输出，明确使用`require`或`include`，连接外部服务，修改ini配置，触发错误或异常，修改全局或者静态变量，读写文件等

接下来的示例，是一个文件既包含了声明又存在了副作用；这是一个反例。

```php
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
```

下面的例子只有一个声明，且不包含”副作用“，这是被提倡的。

```php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
```


3. 命名空间和类
----------------------------

命名空间和类必须遵守[PSR-0]。

这表示每一个类是一个单独的文件，并且至少在一个命名空间下（发行者）。

类名必须是以大写字母开头的驼峰，如：`StudlyCaps`。

PHP5.3以及以后的代码必须使用正式的命名空间。

例子

```php
<?php
// PHP 5.3 and later:
namespace Vendor\Model;

class Foo
{
}
```

Code written for 5.2.x and before SHOULD use the pseudo-namespacing convention
of `Vendor_` prefixes on class names.

```php
<?php
// PHP 5.2.x and earlier:
class Vendor_Model_Foo
{
}
```

4. 类常量，属性和方法
-------------------------------------------

这里指的”类（class）“指的是所有的类，接口（interface）和traits。

### 4.1. 常量

常量必须使用大写字母，并且使用下划线分割。

```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 4.2. 属性

这份指导刻意避免以下提到的属性的命名方法，如：`$StudlyCaps`, `$camelCase`, 或 `$under_score`。


Whatever naming convention is used SHOULD be applied consistently within a
reasonable scope. That scope may be vendor-level, package-level, class-level,
or method-level.
不论什么样的命名规范，都应该在一定的作用域下是一致的。这个作用域可以是：发布者级别，包级别，类的级别或者方法级别。

### 4.3. 方法

方法（函数）名必须声明为小写字母开头的驼峰，如：`camelCase()`。
