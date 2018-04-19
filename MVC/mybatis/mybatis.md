# Mybatis的批量插入功能
CustomerMapper接口中定义批量插入的方法
```java
void  batchInsertCustomer(List<Customer> customers);
```
CustomerMapper.xml中写上对应的sql语句
```
<insert id="batchInsertCustomer" parameterType="java.util.List">
        <selectKey resultType="int" keyProperty="id" order="AFTER">
            SELECT 
            LAST_INSERT_ID()
        </selectKey>
        insert into t_customer(name,age,gender,tel,email,qq,wechat,seller_id,inputUser_id,inputTime,state) values
        <foreach collection="list" item="item" index="index" separator=",">
        (#{item.name},#{item.age},#{item.gender},#{item.tel},#{item.email},#{item.qq},#{item.wechat},#{item.seller.id},#{item.inputUser.id},#{item.inputTime},#{item.state})
        </foreach>
    </insert>
```

这里需要注意几点：
1. insert的id必须和mapper接口中定义的方法一致，这样才能找到正确的sql语句
2. parameterType是接口中定义的参数的类型，刚好与List相匹配
3. selectKey的作用是为了拿到插入数据的主键id
4. 用foreach来遍历整个list，完成一个插入操作

简单的写一个测试类CustomerMapperTest测试一下：
```java
    @Autowired
    private CustomerMapper customerMapper;
    @Test
    public void testBatchInsertCustomer() {
        List<Customer> customers = customerMapper.loadAll();
        customerMapper.batchInsertCustomer(customers);
    }
```

最后就会发现，成功的将原来t_customer表中的数据翻番。

# Mybatis中的小技巧
1. 查询数据的时候where里面如果有"<"的时候，执行起来会出错，本质原因是*mapper.xml实质上还是xml，所以解析器会把该字符解释为新元素的开始
如何解决呢？
使用实体引用：

---|---:|:---:
&lt;  |<   |小于
&gt;    |>   |大于
&amp;   |&   |和号
&apos;  |'   |省略号
&quot;  |"   |引号

使用CDATA：
例如：```<![CDATA[<]]>```