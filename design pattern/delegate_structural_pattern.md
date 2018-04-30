
## 学名
委托模式

## 标准定义
通过分配或委托至其他对象，委托设计模式能够去除核心对象中的判断和复杂的功能性

## 自我理解
1.存在<code>DealA</code>类，需要实现某个功能，但根据不同的输入有不同的处理方式
<br>
2.可以设计<code>DealA</code>的代理类，将不同的处理逻辑在代理类中实现，<code>DealA</code>只需要负责调度

## 生活中强行找例子
1.料理机工作时，榨汁与磨碎选用不同的功能组件

## UML图
![image](https://github.com/beautymyth/skilltree/blob/master/design%20pattern/images/%E5%A7%94%E6%89%98%E6%A8%A1%E5%BC%8F.png?raw=true)

## 代码示例
```php
/**
 * 料理机
 */
class LiaoLiJi {

    private $objDelegate;

    public function __construct($strType) {
        //根据传入参数，动态实例化不同的类
        $strClass = $strType . 'Delegate';
        $this->objDelegate = new $strClass();
    }

    /**
     * 工作
     */
    public function work() {
        $this->objDelegate->work();
    }

}

/**
 * 榨汁
 */
class ZhaZhiDelegate {

    public function work() {
        echo '榨汁';
    }

}

/**
 * 磨碎
 */
class MoSuiDelegate {

    public function work() {
        echo '磨碎';
    }

}

//榨汁
$objLiaoLiJi = new LiaoLiJi('ZhaZhi');
$objLiaoLiJi->work();
//磨碎
$objLiaoLiJi = new LiaoLiJi('MoSui');
$objLiaoLiJi->work();
```

## 适用场景
1.类中需要实现某个业务功能，但根据不同的输入，具体的处理方式不一样
