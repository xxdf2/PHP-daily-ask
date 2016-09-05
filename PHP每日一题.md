标签：Driphp
# PHP每日一题

---

##NO.1如何解决浮点数计算不精确问题？

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


 
