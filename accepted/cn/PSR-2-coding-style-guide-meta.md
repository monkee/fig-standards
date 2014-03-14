PSR-2 Meta文档
===================

1. 摘要
----------


这篇指导的意图是减少不同作者阅读代码的认知不同造成的差异。它通过设定一系列规范代码的规则、期望来达成目的。

这里提到的样式的规则来自各种各样的成员项目。当各种各样的作者在多个项目中的协作，它帮助建立一个可以在各个项目中运行的规范。因此，这份指导的好处不是规则本身，而是这些规则的传播。


2. 投票
--------

- **接受投票:** [ML](https://groups.google.com/d/msg/php-fig/c-QVvnZdMQ0/TdDMdzKFpdIJ)


3. 勘误表
---------

### 3.1 - 跨行 (09/08/2013)

使用一个或多个多行参数（如数组或匿名函数）不会造成参数列表自身的分裂，因此4.6节不会自动强制。数组和匿名函数可以使用多行。

下面的例子是可行的。

```php
<?php
somefunction($foo, $bar, [
  // ...
], $baz);

$app->get('/hello/{name}', function ($name) use ($app) { 
    return 'Hello '.$app->escape($name); 
});
```

### 3.2 - 跨行 (10/17/2013)

When extending multiple interfaces, the list of `extends` should be treated the same as a list
of `implements`, as declared in Section 4.1.

当扩展多行接口时，`extends`的也应该被对待为`implements`，在4.1节中声明。

