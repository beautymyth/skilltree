
## 学名
建造者模式(创建型)

## 标准定义
定义了处理其他对象的复杂构建过程的对象设计

## 自我理解
1.某业务对象存在多种应用场景，不同场景的实例应用在构造函数外还需要执行其他的辅助构造方法
<br>
2.随着业务的变化，执行的辅助构造方法可能也会变化
<br>
3.可使用建造者类来封装对象的实例化过程
<br>
<font color='red'>4.为什么不直接在构造函数中来解决，由于需求的变化，会导致构造方法被不断的修改，因为构造方法不仅用于某个场景，可能会影响其他场景</font>

## 生活中强行找例子
1.料理机，可用于榨汁，绞肉等
<br>
2.使用绞肉功能时，需要底座(__construct)，绞肉刀(init1)，绞肉容器(init2)，绞肉滤网(init3)
<br>
3.当把这些东西组装好后就可以绞肉了，此过程就是建造了一个绞肉机，之后想绞肉用这个组装好的就行了，不用每次都组装一遍

## UML图
![iamge](https://github.com/beautymyth/skilltree/raw/master/design%20pattern/images/%E5%BB%BA%E9%80%A0%E8%80%85%E6%A8%A1%E5%BC%8F.png)

## 代码示例
```php
/**
 * 料理机
 */
class LiaoLiJi {
    /*
     * 不同功能的零件
     */

    private $strLingJian;

    /**
     * 榨汁机，绞肉机都需要的部分
     */
    public function __construct() {
        $this->strLingJian = '底座';
    }

    /**
     * 绞肉刀
     */
    public function init1() {
        $this->strLingJian = $this->strLingJian . '_' . '绞肉刀';
    }

    /**
     * 绞肉容器
     */
    public function init2() {
        $this->strLingJian = $this->strLingJian . '_' . '绞肉容器';
    }

    /**
     * 绞肉滤网
     */
    public function init3() {
        $this->strLingJian = $this->strLingJian . '_' . '绞肉滤网';
    }

    /**
     * 榨汁刀
     */
    public function init4() {
        $this->strLingJian = $this->strLingJian . '_' . '榨汁刀';
    }

    /**
     * 榨汁容器
     */
    public function init5() {
        $this->strLingJian = $this->strLingJian . '_' . '榨汁容器';
    }

    /**
     * 榨汁滤网
     */
    public function init6() {
        $this->strLingJian = $this->strLingJian . '_' . '榨汁滤网';
    }

    /**
     * 料理机工作
     */
    public function run() {
        return $this->strLingJian;
    }

}

/**
 * 建造-绞肉机
 */
class BuilderLiaoLiJi1 {

    private $objLiaoLiJi;

    /**
     * 构建绞肉机
     */
    public function __construct() {
        $this->objLiaoLiJi = new LiaoLiJi();
    }

    /**
     * 组装:如果有零件变化只需要修改此方法
     */
    public function bulid() {
        $this->objLiaoLiJi->init1();
        $this->objLiaoLiJi->init2();
        $this->objLiaoLiJi->init3();
    }

    /**
     * 使用绞肉机
     */
    public function getLiaoLiJi() {
        return $this->objLiaoLiJi;
    }

}

/**
 * 建造-榨汁机
 */
class BuilderLiaoLiJi2 {

    private $objLiaoLiJi;

    /**
     * 构建绞肉机
     */
    public function __construct() {
        $this->objLiaoLiJi = new LiaoLiJi();
    }

    /**
     * 组装:如果有零件变化只需要修改此方法
     */
    public function bulid() {
        $this->objLiaoLiJi->init4();
        $this->objLiaoLiJi->init5();
        $this->objLiaoLiJi->init6();
    }

    /**
     * 使用绞肉机
     */
    public function getLiaoLiJi() {
        return $this->objLiaoLiJi;
    }

}

//使用绞肉机
$objJiaoRouJi = new BuilderLiaoLiJi1();
$objJiaoRouJi->bulid();
//输出：底座_绞肉刀_绞肉容器_绞肉滤网
echo $objJiaoRouJi->getLiaoLiJi()->run();
echo '<br>';
//使用榨汁机
$objZhaZhiJi = new BuilderLiaoLiJi2();
$objZhaZhiJi->bulid();
//输出：底座_绞肉刀_绞肉容器_绞肉滤网
echo $objZhaZhiJi->getLiaoLiJi()->run();
```

## 适用场景
1.获取业务对象的可用实例，除了构造函数外还需要执行其他辅助构造方法
