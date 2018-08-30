# BO定义规范
## 继承规范
+ 1、所有的BO，与数据层的Entity继承相同。
+ 2、在这个基础上，多继承一个BO接口。分别是：
    + IBaseBoEntity：对应贫血模型对象与主数据对象
    + IDomBaseBoEntity：对应DDD的富血模型对象
    
## 范例
```
/**
 * .
 *
 * @author linzhiqiang
 * @version Revision 1.0.0
 * @版权： 版权所有 (c) 2011
 * @see:
 * @创建日期： 2018/7/14
 * @功能说明：
 */
public class OrderItemBo extends AbstractDomBaseEntityImpl<Long> implements IDomBaseBoEntity<Long> {
    //属性
    //方法
}
```

```
/**
 * .
 *
 * @author linzhiqiang
 * @version Revision 1.0.0
 * @版权： 版权所有 (c) 2011
 * @see:
 * @创建日期： 2018/7/14
 * @功能说明：
 */
public class CustomerBo extends BaseEntityImpl<Long> implements IBaseBoEntity<Long> {
    //属性
    //方法
}
```



