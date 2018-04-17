
## 学名
外观模式

## 标准定义
通过在必须的逻辑和方法的集合前创建简单的外观接口，外观模式可以隐藏调用对象的复杂性。

## 自我理解
1.某个业务逻辑包含多个处理步骤，且不止一个地方进行使用
<br>
2.可以将多个处理步骤通过方法进行包装，这样每个地方的调用都会比较简单

## 生活中强行找例子
1.扫地机，轮子负责移动，相机负责规划路线，吸尘器负责吸取灰尘
<br>
2.将它们进行组装，就可以用来自动扫地了，只要点一个开关按钮就行

## UML图


## 代码示例
```php
/**
 * 轮子
 */
class LunZi {

    /**
     * 移动
     */
    public function move() {
        echo 'move-';
    }

}

/**
 * 相机
 */
class XiangJi {

    /**
     * 规划路线
     */
    public function route() {
        echo 'route-';
    }

}

/**
 * 吸尘器
 */
class XiChenQi {

    /**
     * 吸尘
     */
    public function clean() {
        echo 'clean-';
    }

}

/**
 * 扫地机
 */
class SaoDiJiFacade {

    private $objLunZi;
    private $objXiangJi;
    private $objXiChenQi;

    public function __construct() {
        $this->objLunZi = new LunZi();
        $this->objXiangJi = new XiangJi();
        $this->objXiChenQi = new XiChenQi();
    }

    /**
     * 扫地
     */
    public function saodi() {
        $this->objLunZi->move();
        $this->objXiangJi->route();
        $this->objXiChenQi->clean();
    }

}

//自动扫地
$objSaoDiJiFacade = new SaoDiJiFacade();
$objSaoDiJiFacade->saodi();
```

## 适用场景
1.需要将复杂逻辑进行包装，给外部使用提供简单的接口
