# API实现层开发

## Facade接口实现开发规范

```text
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
@Service("privilegeFacadeImpl")
public class PrivilegeFacadeImpl implements PrivilegeFacade {

    /**
     * 注入远程服务调用模板类。
     */
    @Autowired
    @Qualifier("externalRestTemplate")
    private PaasRestTemplate restTemplate;

    /**
     * 服务地址
     */
    @Value("${xxxxxxx}")
    String privelegeUrl;



    @Override
    public List<PrivilegeDTO> queryAllPrivilege() {
        ResponseEntity<PaasBaseResponse<PrivilegeDTO>> responseDto = restTemplate.exchange(
                serviceofferUrl + qryServiceOffer,
                HttpMethod.POST,
                new HttpEntity<>(new PaasBaseRequest<>()),
                new ParameterizedTypeReference<PaasBaseResponse<PrivilegeDTO>>() {
                });

        return responseDto.getBody().getBody();
    }
}
```

* 说明：
  * 1. 必须实现相应的接口


## RestTemplate的使用扩展
### 背景
目前的API模块可以供中心间，如业务层调用数据层，或者跨中心，如客户中心调用受理中心。
在这两种情况下，使用的PaasRestTemplate是不同的bean。

### 目的
为了解决两种不同的场景下，使用不同的template的问题，在AbstractFacadeImpl中增加了处理逻辑。

### 用法
+ 第一步：定义变量
```
@Value("${ord.data.api.isExternal:false}")	private boolean isExternal;
```
建议属性命名方式：
中心名.层名.服务名(可选).api.isExternal
如：
客户中心数据层：cus.data.api.isExternal
受理中心业务处理层：ord.biz.proc.api.isExternal

+ 第二步：重写isExternal方法
```
/**
	 * 是否中心间调用标志，默认为false,若服务需要被跨中心调用，则调用方需配置此参数为true
	 */
	@Value("${ord.biz.processing.api.isExternal:false}")
	private boolean isExternal;
	/**
	 * 重写超类方法
	 * @return
	 */
	 @Override
	protected boolean isExternal(){
		return isExternal;
	}
```

+ 完整案例：
```
/**
 * 业务服务实现--
 *
 * @author sunbin
 * @version Revision 1.0
 * @版权： 版权所有 (c) 2018
 * @创建日期：2018/08/15
 * @功能说明：
 */
@Service("orderProcessingFacade")
public class OrderProcessingFacadeImpl extends AbstractBaseFacadeImpl implements OrderProcessingFacade {
	/**
	 * 订单交互服务地址
	 */
	@Value("${processingRequestUrl}")
	private String processingRequestUrl;
	/**
	 * 是否中心间调用标志，默认为false,若服务需要被跨中心调用，则调用方需配置此参数为true
	 */
	@Value("${ord.biz.processing.api.isExternal:false}")
	private boolean isExternal;
	/**
	 * 重写超类方法
	 * @return
	 */
	 @Override
	protected boolean isExternal(){
		return isExternal;
	}
	@Override
	public PubBaseRes<String> createCustOrderNbr(InitCustomerOrderReq req) {
		ResponseEntity<PubBaseRes<String>> result = getPaasRestTemplate().exchange(
				processingRequestUrl + "createCustOrderNbr", HttpMethod.POST,
				new HttpEntity<>(new PaasBaseRequest<InitCustomerOrderReq>(req)),
				new ParameterizedTypeReference<PubBaseRes<String>>() {
				});
		return result.getBody();
	}
}
```


