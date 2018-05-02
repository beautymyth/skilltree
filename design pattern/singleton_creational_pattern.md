
## 学名
单例模式(创建型)

## 标准定义
通过提供对自身共享实例的访问，单例设计模式用于限制特定对象只能被创建一次。

## 自我理解
1.业务中存在一个对象，出于对资源的有效利用或安全方面考虑
<br>
2.可使用单例模式来控制实例的个数

## 生活中强行找例子
1.超市的收银人员，会随着客流量的增大而增多
<br>
2.收银人员的上限会有一个限制

## UML图
![image](https://github.com/beautymyth/skilltree/blob/master/design%20pattern/images/%E5%8D%95%E4%BE%8B%E6%A8%A1%E5%BC%8F.png?raw=true)

## 代码示例
```php
/**
 * 收银操作
 */
class CashierSingleton {

    /**
     * 最多只有5个收银员
     */
    const intMax = 5;

    /**
     * 收银员
     */
    private static $arrInstance = array();

    /**
     * 收银窗口
     */
    private $intCashNo = 0;

    /**
     * 构造方法
     */
    private function __construct($intCashNo) {
        $this->intCashNo = $intCashNo;
    }

    /**
     * 私有化克隆方法
     */
    private function __clone() {
        
    }

    /**
     * 私有化重建方法
     */
    private function __wakeup() {
        
    }

    public static function getInstance() {
        //随机分配一个收银窗口
        $intCashNo = rand(1, self::intMax);
        //如果窗口还没有收银员，则分配一个
        if (!isset(self::$arrInstance[$intCashNo]) || !(self::$arrInstance[$intCashNo] instanceof self)) {
            self::$arrInstance[$intCashNo] = new self($intCashNo);
        }
        return self::$arrInstance[$intCashNo];
    }

    /**
     * 收银
     */
    public function cash() {
        echo $this->intCashNo . '号窗口收银<br>';
    }

}

//收银：会随机在1-5窗口之间
CashierSingleton::getInstance()->cash();
CashierSingleton::getInstance()->cash();
CashierSingleton::getInstance()->cash();
CashierSingleton::getInstance()->cash();
CashierSingleton::getInstance()->cash();
```

## 适用场景
1.业务对象只能存在限定个数的实例
