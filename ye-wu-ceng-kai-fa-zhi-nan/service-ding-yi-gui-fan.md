# Service定义规范
## 非DDD模式的Service
### 接口
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
public interface ICustBoService extends IGenericBoService<CustBO,Long> {
}
```
+ 说明：
    + 1、 接口继承IGenericBoService

### 实现
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
public class CustBoServiceImpl extends AbstractGenericBoServiceImpl<CustBO, Long>
    implements ICustBoService {
}
```
+ 说明：
    + 1、 类继承于AbstractGenericBoServiceImpl

##DDD的Manager
### 接口
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
public interface IOrderItemBoManager extends IDomGenericBoManager<OrderItemBo,Long> {
}
```
+ 说明：
    + 1、 接口继承IDomGenericBoManager

### 实现
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
public class OrderItemBoManagerImpl extends AbstractDomGenericBoManagerImpl<OrderItemBo, Long>
    implements IOrderItemBoManager {
}
```
+ 说明：
    + 1、 类继承于AbstractDomGenericBoManagerImpl



