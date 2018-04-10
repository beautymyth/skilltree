
## 学名
适配器模式
## 标准定义
将某个对象的接口适配为另一个对象所期望的接口
## 自我理解
1.已存在一个运行稳定且不算简单的<code>DealA类</code>，通过类中的方法，将输入<code>inputA</code>转换为输出<code>outputA</code>，提供给<code>UseA类</code>使用
<br>
2.由于需求原因，新建了一个<code>UseB类</code>，同样需要用到<code>DealA类</code>的处理结果，不过输出<code>outputA</code>需要加工为<code>outputA1</code>
<br>
3.为了保持类的稳定性，不直接修改<code>DealA类</code>，通过新建<code>AdapterDealA类</code>继承自<code>DealA类</code>，在其中先调用<code>DealA类</code>的方法将输入<code>inputA</code>转换为输出<code>outputA</code>，在通过自身的方法将<code>outputA</code>加工为<code>outputA1</code>，最后提供给<code>UseB类</code>使用
## 生活中强行找例子
1.家里有一台<code>豆浆机</code>，可以将大豆磨成豆浆，提供给<code>豆皮机</code>做豆皮
<br>
2.某天我想吃臭豆腐了，买了一个<code>臭豆腐机</code>，原料也是大豆，但是需要现有豆腐才行
<br>
3.因为<code>豆浆机</code>主要负责磨豆浆，不好改造为做豆腐，即使改造了，那么我<code>豆皮机</code>就没啥用了，所以买了一个<code>豆腐机</code>，将<code>豆浆机</code>磨好的豆浆加工为豆腐，再通过<code>臭豆腐机</code>做成臭豆腐
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
1. 对现有稳定的类，进行业务的扩展，出于稳定性，不能直接修改原来的类，新业务还需要调用类中原有的方法。
