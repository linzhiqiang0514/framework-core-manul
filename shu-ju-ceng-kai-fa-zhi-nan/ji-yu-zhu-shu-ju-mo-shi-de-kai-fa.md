# 基于主数据模式的开发

## 主数据相关文档
[主数据相关文档.zip](../.gitbook/assets/主数据相关文档.zip)

## 包结构
与Dao相同

## Entity规范
### 不带动态属性的Entity
```
@Table(name = "PARTY")
public class Party extends AbstractBaseMetaEntityImpl<Long>
    implements IStatusCdOperator<String>, ICreateStaffOperator<Long> {

    //属性


    //方法


}

```
+ 说明：
    + 1、 继承AbstractBaseMetaEntityImpl<ID>

### 带有动态属性表的Entity
#### Cust.java
```
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
+ 说明：
    + 1、 继承AbstractBaseMetaEntityImpl<ID>
    + 2、 重写getAttrEntityClazz方法，返回动态属性表对应的对象
    
#### CustAttr.java
```
@Table(name = "CUST_ATTR")
public class CustAttr extends AbstractBaseMetaAttrEntityImpl<Long> {
    
    //属性
    //GetterAndSetter    
    //重写相应的虚方法
    
}
```
+ 说明：
    + 1、 继承AbstractBaseMetaAttrEntityImpl<ID>
    + 2、 重写相应的虚方法

## Mapper规范
与Dao模式相同
## Dao规范
与Dao模式相同
## Service规范
与Dao模式相同


