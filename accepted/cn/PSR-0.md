自动载入标准
====================

以下描述了必须遵守的强制公约。

强制
---------

* 一个完整的明明空间和类必须包含以下结构
  `\<发布者>\(<命名空间>)\*<类名>`
* 每一个类必须有一个发布名称（Vendor Name）
* 每个明明空间可以根据需要，有多个子明明空间
* 在从文件系统中载入时，每个命名空间的分隔符都可以被转换为`DIRECTORY_SEPARATOR`
* namespace.
* 类名中的每一个下划线“_”都可以被转换为`DIRECTORY_SEPARATOR`。命名空间中的下划线
  `_`不存在特殊意义。
* 完整的明明空间和类以`.php`结尾。
* 发布者、命名空间、类中的字母，可以是任意大小写的组合。


示例
--------

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

命名空间和类的介绍
-----------------------------------------

* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

我们指定的标准应该是最基本的autoloader协议。你可以通过使用可以载入PHP5.3的SPL类Loader，来进行测试。

示例实践
----------------------

接下来是一个完整的示例，表明php中的autoload如何写。

```php
<?php

function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

    require $fileName;
}
```

SPL类(SplClassLoader)实践
-----------------------------

下面的链接是一个SPL类的实践，如果你同意上面的标准，它可以载入你的类。下面的标准是目
前被推荐的方式。

* [http://gist.github.com/221634](http://gist.github.com/221634)

