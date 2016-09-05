标签：Driphp
# PHP Daily Ask

---

##NO.1 如何解决浮点数计算不精确问题？

### 问题描述
在实际的项目中，往往会遇到浮点数计算的问题，但浮点数计算结果不精确，如何解决这个问题呢？如下面：

```php
<?php
var_dump(0.58*100*100==5800);//false
```
### 解决办法
NO.1 先把浮点数计算结果变为string类型，再转为int类型。
```php
<?php
var_dump(intval(strval(0.58*100*100))==5800);//true
```
NO.2使用BCMath高精度函数库。[建议用这个，更方便]
```php
bcadd($a,$b,$scale) 两个数相加,$scale为保留几位小数
bcsub($a,$b,$scale) 左操作数减去右操作数
bcmul($a,$b,$scale) 左数乘以右数
bcdiv($a,$b) 左数除以右数
```
示例如下
```php
bcadd(1,2,1);//3.0
bcsub(5,3);//2
bcmul(5,3);//15
bcdiv(100,2.2,2);//45.45
```
##NO.2 如何获取文件扩展(后缀)名？
### 问题描述
获取文件后缀名，是一个很实用，又有很多种解法的问题。
如：获取 /testweb/test.txt 的扩展名
### 解决办法
PHP中有一个函数：pathinfo()，可以获取文件的路径信息
```php
<?php
$file='/testweb/test.txt';
print_r(pathinfo($file));
```
上面的代码输出
```php
Array
(
    [dirname] => /testweb
    [basename] => test.txt
    [extension] => txt
    [filename] => test
)
```
其中，extension就是文件的扩展名。
获取文件的扩展名，需要下面代码：
```php
<?php
$file='/testweb/test.txt';
$path=pathinfo($file);
$extension=$path['extension'];//txt
```
或者，下面的代码
```php
<?php
$file='/testweb/test.txt';
$extension=pathinfo($file,PATHINFO_EXTENSION);//txt
```
##NO.3 如何将xml转换成数组
###问题描述
有时候，我们需要将xml转变成数组，以方便我们操作。比如接入微信支付的时候，微信返回给我们的就是xml数据，我们需要拿到xml，将xml转成数组。
###解决办法
```php
//禁止引用外部xml实体 
libxml_disable_entity_loader(true); 
//将xml载入对象中（转变成object）
$xmlstring = simplexml_load_string($xml, 'SimpleXMLElement', LIBXML_NOCDATA); 
//将object转变成json,再json_decode转变成数组
$arr = json_decode(json_encode($xmlstring),true); 
```



 
