
## 学名
解释器模式

## 标准定义
用于分析一个实体的关键元素，并且针对每个元素都提供自己的解释或相应的动作。

## 自我理解
1.业务中存在某些模板（消息，页面等），模板中有关键字元素
<br>
2.可以通过解释器类，对关键字元素进行翻译
<br>
3.对于复杂场景，还可以使用多种解释器类，翻译同一个关键字元素

## 生活中强行找例子
1.外卖便当，便当都有相同的米饭，通用配菜
<br>
2.不同风味便当，主要是主菜不同
<br>
3.在生产便当时，在米饭，通用配菜中加入主菜即可

## UML图
![image](https://github.com/beautymyth/skilltree/blob/master/design%20pattern/images/%E8%A7%A3%E9%87%8A%E5%99%A8%E6%A8%A1%E5%BC%8F.png?raw=true)

## 代码示例
```php
/**
 * 便当
 */
class BianDang {

    /**
     * 获取米饭与配菜
     */
    public function getBianDang() {
        return '米饭，配菜，{{ZhuCai.getZhuCai}}';
    }

}

/**
 * 猪肉便当
 */
class PorkBianDang {

    /**
     * 获取主菜
     */
    public function getZhuCai() {
        return '猪肉';
    }

}

/**
 * 鸡肉便当
 */
class ChickenBianDang {

    /**
     * 获取主菜
     */
    public function getZhuCai() {
        return '鸡肉';
    }

}

/**
 * 生产便当
 */
class BianDangInterpreter {

    /**
     * 便当配方
     */
    private $objBianDang;

    /**
     * 便当类型
     */
    private $strType;

    public function __construct($objBianDang, $strType) {
        $this->objBianDang = $objBianDang;
        $this->strType = $strType;
    }

    /**
     * 生产便当
     */
    public function createBianDang() {
        $strBianDang = $this->objBianDang->getBianDang();
        preg_match_all('/\{\{ZhuCai\.(.*)\}\}/', $strBianDang, $arrZhuCai, PREG_PATTERN_ORDER);
        if (!empty($arrZhuCai) && !empty($arrZhuCai[1])) {
            $arrReplacement = [];
            foreach ($arrZhuCai[1] as $strTmp) {
                $arrReplacement[] = $strTmp;
            }
            $arrReplacement = array_unique($arrReplacement);
            $objBianDangTmp = new $this->strType();
            foreach ($arrReplacement as $strTmp) {
                $strBianDang = str_replace("{{ZhuCai.{$strTmp}}}", call_user_func(array($objBianDangTmp, $strTmp)), $strBianDang);
            }
        }
        return $strBianDang;
    }

}

//鸡肉便当
$objBianDang = new BianDang();
$strType = 'ChickenBianDang';
$objBianDangInterpreter = new BianDangInterpreter($objBianDang, $strType);
//输出：米饭，配菜，鸡肉
echo $objBianDangInterpreter->createBianDang();

//猪肉便当
$objBianDang = new BianDang();
$strType = 'PorkBianDang';
$objBianDangInterpreter = new BianDangInterpreter($objBianDang, $strType);
//输出：米饭，配菜，猪肉
echo $objBianDangInterpreter->createBianDang();
```

## 适用场景
1.业务中存在模板翻译的需求，或者某些类似于模板翻译的需求
