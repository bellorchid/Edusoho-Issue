CourseService单元测试
========

###assertFalse()

```php
assertFalse(bool $condition[, string $message = ''])
```

**当 $condition 为 TRUE 时报告错误,错误讯息由 $message 指定，assertNotFalse() 是与之相反的断言,接受相同的参数**


###assertArrayHasKey()

```php
assertArrayHasKey(mixed $key, array $array[, string $message = ''])
```

**当 $array 不包含 $key 时报告错误,错误讯息由 $message 指定,assertArrayNotHasKey() 是与之相反的断言,接受相同的参数。**


###assertClassHasAttribute()

```php
assertClassHasAttribute(string $attributeName, string $className[, string $message = ''])
```

**当 $className::attributeName 不存在时报告错误,错误讯息由 $message 指定,assertClassNotHasAttribute() 是与之相反的断言,接受相同的参数。**


###assertClassHasStaticAttribute()

```php 
assertClassHasStaticAttribute(string $attributeName, string $className[, string $message = ''])
```

**当 $className::attributeName 不存在时报告错误,错误讯息由 $message 指定,assertClassNotHasStaticAttribute() 是与之相反的断言,接受相同的参数**

###assertContains()

```php

```
