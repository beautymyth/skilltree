
## 学名
装饰器模式(结构型)

## 标准定义
已有对象的部分内容或功能性发生改变，但不需要修改原始对象的结构，可使用装饰器模式

## 自我理解
1.已存在某个业务对象，此对象需要扩展功能来满足新需求
<br>
2.可使用装饰类来扩展功能，而不是继承的方式来实现
<br>
<font color='red'>3.为什么不使用继承重载，如果出现多次继承的情况就会使代码失去可理解性与维护性</font>
<br>

## 生活中强行找例子
1.家里一直煮白米粥
<br>
2.某天想吃白米+红豆粥，则在煮的时候额外加入红豆
<br>
3.某天想吃白米+小米粥，则在煮的时候额外加入小米

## UML图
![image](https://github.com/beautymyth/skilltree/blob/master/design%20pattern/images/%E8%A3%85%E9%A5%B0%E5%99%A8%E6%A8%A1%E5%BC%8F.png?raw=true)

## 代码示例
```php
/**
 * 煮白米粥
 */
class Cook {

    public function __construct() {
        
    }

    public function cook() {
        echo '白米粥';
    }

}

/**
 * 煮红豆白米粥
 */
class DecoratorCookA {

    private $objCook;

    public function __construct($objCook) {
        $this->objCook = $objCook;
    }

    /**
     * 装饰cook
     */
    public function cook() {
        echo '红豆';
        $this->objCook->cook();
    }

}

/**
 * 煮小米白米粥
 */
class DecoratorCookB {

    private $objCook;

    public function __construct($objCook) {
        $this->objCook = $objCook;
    }

    /**
     * 装饰cook
     */
    public function cook() {
        echo '小米';
        $this->objCook->cook();
    }

}

$objCook = new Cook();
$objDecoratorCookA = new DecoratorCookA(new Cook());
$objDecoratorCookB = new DecoratorCookB(new Cook());

//输出：白米粥
$objCook->cook();
echo '<br>';
//输出：红豆白米粥
$objDecoratorCookA->cook();
echo '<br>';
//输出：小米白米粥
$objDecoratorCookB->cook();
```

## 适用场景
1.对现有业务对象进行功能扩展，同时不修改原有对象的功能
