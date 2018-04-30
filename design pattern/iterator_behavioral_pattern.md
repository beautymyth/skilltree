
## 学名
迭代器模式

## 标准定义
构造特定对象，对象能够提供单一标准接口循环或迭代任何类型的可计数数据。

## 自我理解
1.业务中需要循环某个对象集合，一般情况下使用数组即可
<br>
2.随着业务的变化，对象集合生成的逻辑可能会发生变化，就需要调整所有涉及到使用的地方
<br>
3.可将对象集合的生成放到迭代器类中，在需要的地方迭代此类的实例即可，如果业务变化，只需调整此类中的生成逻辑

## 生活中强行找例子
1.糖葫芦机将水果块机加工好的水果块串起来
<br>
2.生产不同的糖葫芦只需要控制水果机加工不同的水果即可

## UML图
![image](https://github.com/beautymyth/skilltree/blob/master/design%20pattern/images/%E8%BF%AD%E4%BB%A3%E5%99%A8%E6%A8%A1%E5%BC%8F.png?raw=true)

## 代码示例
```php
/**
 * 水果块
 */
class Fruit {

    public $strFruitName = '';

    public function __construct($strFruitName) {
        $this->strFruitName = $strFruitName;
    }

}

/**
 * 水果块机
 */
class FruitIterator implements Iterator {

    /**
     * 加工好的水果块
     */
    private $arrFruits = [];

    /**
     * 当前迭代位置是否有效
     */
    private $blnValid = false;

    /**
     * 加工水果成水果块
     * @param int $intCount 需要块数
     */
    public function __construct($intCount = 10) {
        //隐藏很多加工逻辑
        $intIndex = 1;
        while ($intIndex <= $intCount) {
            $this->arrFruits[] = new Fruit('fruit' . $intIndex);
            $intIndex++;
        }
    }

    /**
     * 返回当前元素
     */
    public function current() {
        return current($this->arrFruits);
    }

    /**
     * 返回到迭代器的第一个元素
     */
    public function rewind() {
        $this->blnValid = (reset($this->arrFruits) === false) ? false : true;
    }

    /**
     * 向前移动到下一个元素
     */
    public function next() {
        $this->blnValid = (next($this->arrFruits) === false) ? false : true;
    }

    /**
     * 返回当前元素的键
     */
    public function key() {
        return key($this->arrFruits);
    }

    /**
     * 检查当前位置是否有效
     */
    public function valid() {
        return $this->blnValid;
    }

}

/**
 * 糖葫芦机
 */
class TangHuLuJi {

    private $objFruitIterator;

    public function __construct($objFruitIterator) {
        $this->objFruitIterator = $objFruitIterator;
    }

    /**
     * 串糖葫芦
     */
    public function create() {
        $strThl = '';
        foreach ($this->objFruitIterator as $objFruit) {
            $strThl.=$objFruit->strFruitName . '.';
        }
        return $strThl;
    }

}

//生成水果块
$objFruitIterator = new FruitIterator(6);
//串糖葫芦
$objTangHuLuJi = new TangHuLuJi($objFruitIterator);
//输出：fruit1.fruit2.fruit3.fruit4.fruit5.fruit6.
echo $objTangHuLuJi->create();
```

## 适用场景
1.业务中存在被迭代的对象集合，且对象集合的生成逻辑可能会发生变化
