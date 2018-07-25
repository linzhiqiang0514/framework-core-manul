# 服务定义规范

## 开发规范
### 范例
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
@Api("xxxx")
@RefreshableRestController
@RequestMapping("/xxxCenter/xxx/xxx")
public class CustController extends AbstractBaseController {
}
```
### 说明
+ 1、必须继承AbstractBaseController
+ 2、必须配置Swagger注解


