# API实现层开发

## Facade接口实现开发规范

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
  

