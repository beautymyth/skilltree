
## 学名
适配器模式(结构型)

## 标准定义
将某个对象的接口适配为另一个对象所期望的接口

## 自我理解
1.已存在某个业务对象，它为其他对象提供接口
<br>
2.新业务也需要使用原对象的接口，但是可能需要进行一些调整
<br>
3.可以使用适配器类，将原有对象的接口适配给新业务使用

## 生活中强行找例子
1.家里有一台豆浆机，可以将大豆磨成豆浆，提供给豆皮机做豆皮
<br>
2.某天我想吃臭豆腐了，买了一个臭豆腐机，原料也是大豆，但是需要先有豆腐才行
<br>
3.因为豆浆机主要负责磨豆浆，不好改造为做豆腐，即使改造了，那么我豆皮机就没啥用了，所以买了一个豆腐机，将豆浆机磨好的豆浆加工为豆腐，再通过臭豆腐机做成臭豆腐

## UML图
![image](https://github.com/beautymyth/skilltree/raw/master/design%20pattern/images/%E9%80%82%E9%85%8D%E5%99%A8%E6%A8%A1%E5%BC%8F.png)

## 代码示例
#### 现有业务：我吃豆皮
```php
/**
 * 豆浆机
 * DealA:运行稳定且不算简单的类
 */
class DealA {

    private $strInput = '';

    public function __construct($strInput) {
        $this->strInput = $strInput;
    }

    /**
     * 磨豆腐
     */
    public function deal() {
        //此处省略1W行代码
        return $this->strInput . '_豆浆';
    }

}

/**
 * 豆皮机
 * UseA:使用DealA的处理的结果
 */
class UseA {

    private $objDealA;

    public function __construct($strInput) {
        $this->objDealA = new DealA($strInput);
    }

    /**
     * 做豆皮
     */
    public function deal() {
        return $this->objDealA->deal() . '_豆皮';
    }

}

$objUseA = new UseA('红豆');
//输出结果：红豆_豆浆_豆皮
echo $objUseA->deal();
```

#### 新需求：我要吃臭豆腐
```php
/**
 * 臭豆腐机
 * UseB:不能直接使用DealA的处理的结果
 */
class UseB {

    private $objAdapterDealA;

    public function __construct($strInput) {
        $this->objAdapterDealA = new AdapterDealA($strInput);
    }

    /**
     * 做臭豆腐
     */
    public function deal() {
        return $this->objAdapterDealA->deal() . '_臭豆腐';
    }

}

/**
 * 豆腐机
 * AdapterDealA(适配类):不对原来的DealA进行修改，通过此类来进一步加工DealA的输出，提供给UseB使用
 */
class AdapterDealA extends DealA {

    /**
     * 做豆腐
     */
    public function deal() {
        //对DealA结果进行加工
        return parent::deal() . '_豆腐';
    }

}

$objUseB = new UseB('红豆');
//输出：红豆_豆浆_豆腐_臭豆腐
echo $objUseB->deal();
```

## 适用场景
1. 将现有稳定的对象，适配给新业务使用
