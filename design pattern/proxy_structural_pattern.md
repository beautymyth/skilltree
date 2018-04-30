
## 学名
代理模式(结构型)

## 标准定义
创建了透明置于两个不同对象之间的对象，从而能够截取或代理这两个对象间的通信和访问。

## 自我理解
1.业务中存在一个对象，在某些应用情况下需要进行一些额外控制或修改
<br>
2.可通过代理类，来重载原对象的方法，在新方法里增加控制逻辑或修改原逻辑

## 生活中强行找例子
1.土豆削皮机，对所有放进去的土豆都削皮
<br>
2.由于客户对土豆大小有限制，所以只对超过某个尺寸的土豆进行削皮
<br>
3.可复制原机器功能，在投入土豆的地方，增加一个过滤功能，按需对土豆尺寸进行过滤

## UML图
![image](https://github.com/beautymyth/skilltree/blob/master/design%20pattern/images/%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F.png?raw=true)

## 代码示例
```php
/**
 * 削皮机
 */
class PeerMachine {

    /**
     * 削皮
     */
    public function peer($arrPotato) {
        foreach ($arrPotato as $intPotato) {
            echo '土豆尺寸：' . $intPotato . '<br>';
        }
    }

}

/**
 * 削皮机-代理类
 */
class PeerMachineProxy extends PeerMachine {

    /**
     * 重新代理削皮逻辑
     * 只处理尺寸>=5的土豆
     */
    public function peer($arrPotato) {
        foreach ($arrPotato as $intPotato) {
            if ($intPotato < 5) {
                continue;
            }
            echo '土豆尺寸：' . $intPotato . '<br>';
        }
    }

}

//土豆
$arrPotato = range(1, 10, 2);

//旧需求
$objPeerMachine = new PeerMachine();
//输出：1，3，5，7，9
$objPeerMachine->peer($arrPotato);

//新需求
$objPeerMachineProxy = new PeerMachineProxy();
//输出：5，7，9
$objPeerMachineProxy->peer($arrPotato);
```

## 适用场景
1.业务中某个对象，在使用时需要增加额外的处理
