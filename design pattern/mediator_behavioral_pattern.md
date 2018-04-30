
## 学名
中介者模式

## 标准定义
创建一个对象，该对象能够在类似对象相互之间不直接交互的情况下传送或调解对这些对象的集合的修改。

## 自我理解
1.业务中存在多个对象但是非耦合的，当一个对象中产生某些事件时需要告知其它对象
<br>
2.如果在每个对象中都维护通知别的对象的逻辑，不便于维护
<br>
3.通过增加中介类，当某个对象产生事件，通知中介类，中介类再告知其它对象

## 生活中强行找例子
1.在马路边捡到失物了，不需要自己到处找失主
<br>
2.可以通知警察局，警察局将消息告知给很多人，看谁丢了东西

## UML图
![image](https://github.com/beautymyth/skilltree/blob/master/design%20pattern/images/%E4%B8%AD%E4%BB%8B%E8%80%85%E6%A8%A1%E5%BC%8F.png?raw=true)

## 代码示例
```php
/**
 * 路人1
 */
class People1 {

    /**
     * 警察局
     */
    private $objPoliceMediator;

    public function __construct($objPoliceMediator) {
        $this->objPoliceMediator = $objPoliceMediator;
    }

    /**
     * 生成消息
     */
    public function createMsg($strMsg) {
        $this->receiveMsg($strMsg);
        //通过警察局广播
        if (!is_null($this->objPoliceMediator)) {
            $this->objPoliceMediator->broadcast($this, $strMsg);
        }
    }

    /**
     * 接受消息
     */
    public function receiveMsg($strMsg) {
        echo __CLASS__ . ':' . $strMsg . '<br>';
    }

}

/**
 * 路人2
 */
class People2 {

    /**
     * 警察局
     */
    private $objPoliceMediator;

    public function __construct($objPoliceMediator) {
        $this->objPoliceMediator = $objPoliceMediator;
    }

    /**
     * 生成消息
     */
    public function createMsg($strMsg) {
        $this->receiveMsg($strMsg);
        //通过警察局广播
        if (!is_null($this->objPoliceMediator)) {
            $this->objPoliceMediator->broadcast($this, $strMsg);
        }
    }

    /**
     * 接受消息
     */
    public function receiveMsg($strMsg) {
        echo __CLASS__ . ':' . $strMsg . '<br>';
    }

}

/**
 * 警察局
 */
class PoliceMediator {

    private $arrPeople = [];

    public function __construct() {
        $this->arrPeople = ['People1', 'People2'];
    }

    /**
     * 通知除了捡到东西的人
     */
    public function broadcast($objFromPeople, $strMsg) {
        foreach ($this->arrPeople as $strPeople) {
            if (!($objFromPeople instanceof $strPeople)) {
                $objToPeople = new $strPeople();
                $objToPeople->receiveMsg($strMsg);
            }
        }
    }

}

$objPoliceMediator = new PoliceMediator();
//路人1捡到东西
$objPeople1 = new People1($objPoliceMediator);
//输出：
//People1:people1捡到一个东西
//People2:people1捡到一个东西
$objPeople1->createMsg('people1捡到一个东西');

//路人2捡到东西
$objPeople2 = new People2($objPoliceMediator);
//输出：
//People2:people2捡到一个东西
//People1:people2捡到一个东西
$objPeople2->createMsg('people2捡到一个东西');
```

## 适用场景
1.业务中存在多个类似的非耦合对象，当某个对象产生事件，需要同步告知其它对象
