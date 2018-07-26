# 基于主数据模式的开发

## 主数据相关文档

[主数据相关文档.zip](https://github.com/linzhiqiang0514/framework-core-manul/tree/1df45a1bb4a06a60b6ce0d46acfbf60aed11f254/.gitbook/assets/主数据相关文档.zip)

## 引入Jar包
引入framework-core-meta下对应的模块。
如:
data-service-->framework-core-meta-data-service
biz-service-->framework-core-meta-biz-service
## 包结构

与Dao相同

## Entity规范

### 不带动态属性的Entity

```text
@Table(name = "PARTY")
public class Party extends AbstractBaseMetaEntityImpl<Long>
    implements IStatusCdOperator<String>, ICreateStaffOperator<Long> {

    //属性


    //方法


}
```

* 说明：
  * 1、 继承AbstractBaseMetaEntityImpl

### 带有动态属性表的Entity

#### Cust.java

```text
@Table(name = "CUST")
public class Cust extends AbstractBaseMetaEntityImpl<Long>
    implements ICreateDateOperator<Date>, IUpdateDateOperator<Date> {
    //属性
    //方法

    @Override
    public Class<CustAttr> getAttrEntityClazz() {
        return CustAttr.class;
    }
}
```

* 说明：
  * 1、 继承AbstractBaseMetaEntityImpl
  * 2、 重写getAttrEntityClazz方法，返回动态属性表对应的对象

#### CustAttr.java

```text
@Table(name = "CUST_ATTR")
public class CustAttr extends AbstractBaseMetaAttrEntityImpl<Long> {

    //属性
    //GetterAndSetter    
    //重写相应的虚方法

}
```

* 说明：
  * 1、 继承AbstractBaseMetaAttrEntityImpl
  * 2、 重写相应的虚方法

## Mapper规范

与Dao模式相同

## Dao规范

与Dao模式相同

## Service规范

与Dao模式相同

## 操作动态属性

假设客户有个纵表属性，属性名称vipLevel。 配置了相应的主数据之后。

```text
Cust cust = new Cust();
cust.writeAttr("vipLevel",1);
```

