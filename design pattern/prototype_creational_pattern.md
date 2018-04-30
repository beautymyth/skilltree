
## 学名
原型模式(创建型)

## 标准定义
创建对象的方式是复制和克隆初始对象或原型，这种方式比创建新实例更有效。

## 自我理解
1.业务中存在一个对象，需要通过较复杂的逻辑，才能得到此对象的一个可用实例
<br>
2.在系统流程中需要使用多个此对象的实例，实例的初始信息基本一致
<br>
3.可通过克隆已经存在的实例，来避免每次都需要重新实例化对象

## 生活中强行找例子
1.生日蛋糕主要由奶油底座+底座上的摆设构成
<br>
2.一批定制蛋糕中，底座都是一样的，但是底座需要花很大的功夫去设计图案与样式
<br>
3.当设计好一个底座之后，之后的底座都通过这个底座去复制

## UML图
![image](https://github.com/beautymyth/skilltree/blob/master/design%20pattern/images/%E5%8E%9F%E5%9E%8B%E6%A8%A1%E5%BC%8F.png?raw=true)

## 代码示例
```php
/**
 * 蛋糕底座
 */
class DiZuo {

    /**
     * 加工好的底座
     */
    private $strDiZuo = '';

    /**
     * 设计与装饰
     */
    public function __construct() {
        //复杂逻辑
        $this->strDiZuo = '加工好的底座';
    }

    /**
     * 微调
     */
    public function modify($strModify) {
        $this->strDiZuo = $this->strDiZuo . $strModify;
    }

}

//模板底座
$objDiZuoModule = new DiZuo();
//复制第一个
$objDiZuoClone1 = clone $objDiZuoModule;
$objDiZuoClone1->modify('微调1');
//输出：object(DiZuo)#2 (1) { ["strDiZuo":"DiZuo":private]=> string(25) "加工好的底座微调1" } 
var_dump($objDiZuoClone1);
//复制第二个
$objDiZuoClone2 = clone $objDiZuoModule;
$objDiZuoClone2->modify('微调2');
//输出：object(DiZuo)#3 (1) { ["strDiZuo":"DiZuo":private]=> string(25) "加工好的底座微调2" }
var_dump($objDiZuoClone1);
```

## 适用场景
1.业务中需要多次使用某个对象的实例，实例的构建较复杂，且新实例的初始信息基本一致
