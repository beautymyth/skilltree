
## 学名
数据访问对象模式

## 标准定义
提供透明访问任何数据源的对象

## 自我理解
1.项目中存在很多操作数据源的地方，没必要每个地方都进行数据源连接等通用操作
<br>
2.开发人员在开发不同的业务功能时，只需要关心业务相关联的sql语句就行，而不需要关心数据源是如何连接以及连接的到底是哪些数据源
<br>
3.至于使用orm还是纯sql的方式，看实际情况吧

## 生活中强行找例子
1.投币净水机，通过此机器获取到水，而不需要关心水到底是哪里来的

## UML图
![image](https://github.com/beautymyth/skilltree/blob/master/design%20pattern/images/%E6%95%B0%E6%8D%AE%E8%AE%BF%E9%97%AE%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%BC%8F.png?raw=true)

## 代码示例
```php
//配置文件
include getenv('BMRootPathPM') . 'Config/Config.config.php';
include ComModule_Path . 'Security/Des.Com.php';

/**
 * 数据访问对象类
 */
class DataBase {

    /**
     * 数据库连接对象
     */
    private $objConnect;

    /**
     * 数据库操作对象
     */
    private $objStmt;

    /**
     * 构造函数
     */
    public function __construct() {
        $dsn = sprintf('mysql:host=%s;dbname=%s;port=%s;charset=UTF8;', MYSQL_HOST, MYSQL_DB, MYSQL_PORT);
        $this->objConnect = new PDO($dsn, MYSQL_USER, DES::getInstance()->decrypt(MYSQL_PASS));
        $this->objConnect->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    }

    /**
     * 执行查询语句
     * @param string $strSql sql语句
     * @param array $arrParams 参数
     * @return array 返回结果
     */
    protected function ExecuteSelect($strSql, $arrParams) {
        try {
            //1.查询处理
            $this->objStmt = $this->objConnect->prepare($strSql);
            $this->ExecuteStatement($this->objStmt, $arrParams);
            $arrRes = $this->objStmt->fetchAll(PDO::FETCH_ASSOC);
            //2.返回结果
            return $arrRes;
        } catch (Exception $e) {
            return array();
        }
    }

    /**
     * 执行prepare的语句
     * @param PDOStatement $statement prepare的statement
     * @param array $params 参数
     * @throws Exception 执行失败抛出异常
     */
    private function ExecuteStatement(PDOStatement $statement, array $params) {
        if (!$statement->execute($params)) {
            throw new Exception('执行statement错误');
        }
    }

}

/**
 * 业务类BLLUse继承自DataBase
 */
class BLLUse extends DataBase {

    /**
     * 查询业务信息
     */
    public function select($intId) {
        $strSql = 'select cname from test where id=:id';
        $arrParams = [':id' => $intId];
        return $this->ExecuteSelect($strSql, $arrParams);
    }

}

//使用业务类
$objBLLUse = new BLLUse();
//输出array(1) { [0]=> array(1) { ["cname"]=> string(12) "轻松工作" } }
var_dump($objBLLUse->select(3));
```

## 适用场景
1.绝大多数对数据源（数据库，缓存等）的操作
