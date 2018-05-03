
## 学名
策略模式(行为型)

## 标准定义
帮助构建的对象不必自身包含逻辑，而是能够根据需要利用其它对象中的算法。

## 自我理解
1.业务对象需要对相同的输入，执行不同的处理逻辑
<br>
2.可使用策略模式，在运行时对相同输入采用不同的算法处理

## 生活中强行找例子
1.可以对鱼进行蒸，煮，炸的烹饪方式

## UML图
![image](https://github.com/beautymyth/skilltree/blob/master/design%20pattern/images/%E7%AD%96%E7%95%A5%E6%A8%A1%E5%BC%8F.png?raw=true)

## 代码示例
```php
/**
 * 烹饪鱼
 */
class FishCookStrategy {

    /**
     * 烹饪方式
     */
    private $objCookType;

    public function __construct() {
        
    }

    /**
     * 设置烹饪方式
     */
    public function setCookType($objCookType) {
        $this->objCookType = $objCookType;
    }

    /**
     * 烹饪
     */
    public function cook($strFish) {
        $this->objCookType->cook($strFish);
    }

}

/**
 * 蒸
 */
class CookZheng {

    public function cook($strFish) {
        echo '蒸：' . $strFish . '<br>';
    }

}

/**
 * 煮
 */
class ZhuZheng {

    public function cook($strFish) {
        echo '煮：' . $strFish . '<br>';
    }

}

$objFishCookStrategy = new FishCookStrategy();

//蒸
$objCookZheng = new CookZheng();
$objFishCookStrategy->setCookType($objCookZheng);
$objFishCookStrategy->cook('鲫鱼');
//煮
$objZhuZheng = new ZhuZheng();
$objFishCookStrategy->setCookType($objZhuZheng);
$objFishCookStrategy->cook('鲫鱼');
```

## 适用场景
1.对于相同的输入参数，在运行时可使用不同的算法进行处理
