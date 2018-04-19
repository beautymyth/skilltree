
## 学名
工厂模式

## 标准定义
提供获取某个对象新实例的接口，同时在调用代码中避免出现确定实际实例化基类的步骤

## 自我理解
1.某个业务功能，需要根据不同的类型，使用不同类的实例化对象处理
<br>
2.此业务功能，可能会用于系统中的多个地方
<br>
3.可使用工厂类来完成实例化对象的处理，以避免在多处使用造成的代码冗余

## 生活中强行找例子
1.蛋糕店制作不同模型的饼干，需要使用不同的模具
<br>
2.有个机器，可以在选定模型后，自动吐出对应的模具

## UML图
![image](https://github.com/beautymyth/skilltree/blob/master/design%20pattern/images/%E5%B7%A5%E5%8E%82%E6%A8%A1%E5%BC%8F.png?raw=true)

## 代码示例
```php
/**
 * 小马模具
 */
class HorseCake {

    /**
     * 烘烤
     */
    public function bake() {
        echo '做小马饼干';
    }

}

/**
 * 飞机模具
 */
class PlainCake {

    /**
     * 烘烤
     */
    public function bake() {
        echo '做飞机饼干';
    }

}

/**
 * 饼干工厂
 */
class CakeFactory {

    /**
     * 根据饼干类型获取不同的模具
     */
    public static function getMould($strType) {
        $class = $strType . 'Cake';
        return new $class();
    }

}

//做小马饼干
CakeFactory::getMould('Horse')->bake();
//做飞机饼干
CakeFactory::getMould('Plain')->bake();
```

## 适用场景
1.业务需要根据不同类型，实例化不同的类来处理逻辑
