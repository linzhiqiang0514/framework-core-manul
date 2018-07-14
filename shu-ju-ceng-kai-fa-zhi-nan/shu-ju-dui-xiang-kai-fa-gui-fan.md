# 数据对象开发规范

## 注解规范
### 基本的注解
数据库映射对象（PO），需要对字段、类进行相应的注解标识。
主要是：
@Table
@Id
@Column
@Version

分片表，库内分表要特别标记
@PartitionTable
@SharedTable
@PartitionKey
@SharedKey

###范例

```
/**
 * .
 *
 * @author linzhiqiang
 * @version Revision 1.0.0
 * @版权： 版权所有 (c) 2011
 * @see:
 * @创建日期： 2018/7/6
 * @功能说明：
 */
@PartitionTable
@SharedTable
@Table(name = "PRIVILEGE")
public class Privilege extends BaseEntityImpl<Long>
    implements IStatusCdOperator<String>, IPartitionEntity<Date>, ISingleShardingEntity<Long>,
    IVersionEntity<Long> {
    
    public Privilege() {
    }
    
    public Privilege(boolean genId) {
        super(genId);
    }
    
    @Id
    @Column(name = "PRIVILEGE_ID")
    private Long   privilegeId;
    
    @Column(name = "PRIVILEGE_NAME")
    private String privilegeName;
    
    @Column(name = "PRIVILEGE_TYPE")
    private String privilegeType;
    
    @Column(name = "STATUS_CD")
    private String statusCd;
    
    @SharedKey
    @Column(name = "PRI_SHARDING_ID")
    private Long   priSharingId;
    
    @PartitionKey
    @Column(name = "PRI_INNER_SHARDING_ID")
    private Date   priInnerShadingId;
    
    @Version
    @Column(name = "D_VERSION")
    private Long   dVersion;
    
    public Long getPrivilegeId() {
        return privilegeId;
    }
    
    public void setPrivilegeId(Long privilegeId) {
        this.privilegeId = privilegeId;
    }
    
    public String getPrivilegeName() {
        return privilegeName;
    }
    
    public void setPrivilegeName(String privilegeName) {
        this.privilegeName = privilegeName;
    }
    
    public String getPrivilegeType() {
        return privilegeType;
    }
    
    public void setPrivilegeType(String privilegeType) {
        this.privilegeType = privilegeType;
    }
    
    public Date getPriInnerShadingId() {
        return priInnerShadingId;
    }
    
    public void setPriInnerShadingId(Date priInnerShadingId) {
        this.priInnerShadingId = priInnerShadingId;
    }
    
    public Long getPriSharingId() {
        return priSharingId;
    }
    
    public void setPriSharingId(Long priSharingId) {
        this.priSharingId = priSharingId;
    }
    
    public Long getdVersion() {
        return dVersion;
    }
    
    public void setdVersion(Long dVersion) {
        this.dVersion = dVersion;
    }
    
    @Override
    public Long getId() {
        return getPrivilegeId();
    }
    
    @Override
    public void setId(Long aLong) {
        setPrivilegeId(aLong);
    }
    
    @Override
    public String getStatusCd() {
        return statusCd;
    }
    
    @Override
    public void setStatusCd(String statusCd) {
        this.statusCd = statusCd;
    }

    @Override
    public Date getPartitionKey() {
        return getPriInnerShadingId();
    }

    @Override
    public void setPartitionKey(Date partitionKey) {
        setPriInnerShadingId(partitionKey);
    }

    @Override
    public Long getShardingKey() {
        return getPriSharingId();
    }

    @Override
    public void setShardingKey(Long shardingId) {
        setPriSharingId(shardingId);
    }

    @Override
    public Long getVersion() {
        return getdVersion();
    }

    @Override
    public void setVersion(Long version) {
        setdVersion(version);
    }
}
```


###说明
####一、普通表
1、增加@Table,@Id,@Column注解
2、表名、字段名，统一采用大写。
####二、版本控制（乐观锁）
当存在版本控制的乐观锁字段时，需要进行以下处理
1、增加@Version注解
2、实现接口 IVersionEntity<VType extends Serializable>，根据字段类型实现接口操作。
####三、分片表
当表属于分片表时，，需要进行以下处理
1、需要增加相应注解，标记分片表，分片字段
@SharedTable
@SharedKey
2、实现接口 ISingleShardingEntity<SType extends Serializable>（一维分片），ITwoDimensionsShardingEntity<MType extends Serializable, SType extends Serializable>（二维分片），根据字段类型实现接口操作。
####四、库内分表
当表属于库内分表时，，需要进行以下处理
1、需要增加相应注解，标记库内分表，库内分表字段
@PartitionTable
@PartitionKey
2、实现接口 IPartitionEntity<InType extends Serializable>，根据字段类型实现接口操作。





