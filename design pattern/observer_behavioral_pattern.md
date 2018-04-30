
## 学名
观察者模式

## 标准定义
便利的创建查看目标对象状态的对象，并提供与核心对象非耦合的指定功能性。

## 自我理解
1.业务中存在多个对象依赖于某个对象A，当A发生变化时，需要通知其它对象进行相应的处理
<br>
2.可以在对象A中，动态的增加或减少需要通知的对象

## 生活中强行找例子
1.从报社订阅报纸，当报社出版新报纸时
<br>
2.社会根据订阅的人，给他们邮寄新版报纸

## UML图
![image](https://github.com/beautymyth/skilltree/blob/master/design%20pattern/images/%E8%A7%82%E5%AF%9F%E8%80%85%E6%A8%A1%E5%BC%8F.png?raw=true)

## 代码示例
```php
/**
 * 出版社
 */
class Press {

    /**
     * 订阅者
     */
    private $arrObserver = [];

    /**
     * 增加订阅者
     */
    public function addObserver($objOb) {
        $this->arrObserver[] = $objOb;
    }

    /**
     * 给订阅者邮寄报纸
     */
    private function notifyOb($strMsg) {
        foreach ($this->arrObserver as $objOb) {
            $objOb->receive($strMsg);
        }
    }

    /**
     * 出版新报纸
     */
    public function pulish($strType) {
        $this->notifyOb($strType . '报纸');
    }

}

/**
 * 订阅者1
 */
class PeopleObserver1 {

    /**
     * 接受报纸
     */
    public function receive($strMsg) {
        echo __CLASS__ . ':' . $strMsg . '<br>';
    }

}

/**
 * 订阅者1
 */
class PeopleObserver2 {

    /**
     * 接受报纸
     */
    public function receive($strMsg) {
        echo __CLASS__ . ':' . $strMsg . '<br>';
    }

}

$objPress = new Press();
$objPeopleObserver1 = new PeopleObserver1();
$objPeopleObserver2 = new PeopleObserver2();
//增加订阅者
$objPress->addObserver($objPeopleObserver1);
$objPress->addObserver($objPeopleObserver2);
//出版体育报纸
$objPress->pulish('体育');
//出版财经报纸
$objPress->pulish('财经');
```

## 适用场景
1.业务中存在多个对象依赖于某个对象，当此对象发生变化时，需要告知依赖于它的对象
