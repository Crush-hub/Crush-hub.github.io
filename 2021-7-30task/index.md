# 2021-7-30Task


# 工作记录

## 需求 &rarr; 涉及表 &rarr; 报文 &rarr; 接口 &rarr; bean &rarr; Sql

## 晨夕会

### 晨会-昨日业绩回顾

 {{< admonition  "补充">}}

1. 银行AUM代表的是银行资产管理规模，所以它是一个衡量银行业务的指标。

现实中，AUM(Asset Under Management)直译是指资产管理规模，所以银行可以用这个指标来衡量客户的价值。也就是说客户的AUM越高，那么他对该银行的贡献度越高。

2. DATE_FORMAT() 函数用于以不同的格式显示日期/时间数据。

```sql
DATE_FORMAT(date,format)
```

*date* 参数是合法的日期。*format* 规定日期/时间的输出格式。

 {{< /admonition >}}



- 接口：`meet/morning`

- 涉及表：PAGE_PERFORM_SUMMARY（晨夕会）
- 需求：

![](https://i.loli.net/2021/07/30/C7y2nbd8ch6vLYX.png " ")

- 报文

```xml
<?xml version="1.0" encoding="utf-8"?>
<trans name="in/meet/morning" desc="晨夕会-晨会">
	<snd>
		<field name="ORG_ID" desc="机构号" required="true" />
	</snd>
	<rcv>
		<field name="LOAN_BAL" desc="昨日个贷余额" />
		<field name="LOAN_COM_DAY" desc="个贷增加量" />
		<field name="LOAN_INFLOW" desc="昨日出账" />
		<field name="LOAN_OUTFLOW" desc="昨日还款" />
		<field name="AUM_BAL" desc="昨日AUM余额" />
		<field name="AUM_COM_DAY" desc="AUM增加量" />
		<field name="FUND_AMT" desc="昨日基金销售额" />
		<field name="INSURE_AMT" desc="昨日保险销售额" />
		<field name="PRECIOUS_METAL" desc="昨日贵金属销售额" />
		<field name="CUST_ADD" desc="昨日新增客户数" />
		<field name="PB_CUST_ADD" desc="昨日新增私银" />
		<field name="DIAMOND_CUST_ADD" desc="昨日新增钻石" />
		<field name="PLATINUM_CUST_ADD" desc="昨日新增白金" />
		<field name="GOLD_CUST_ADD" desc="昨日新增金卡" />
		<field name="NORMAL_CUST_ADD" desc="昨日新增普卡" />
	</rcv>
</trans>
```

- 流图

单条数据查询

- `sql`

```sql
<select id="get" parameterType="map" resultType="map">		 
		SELECT 			
			LOAN_BAL,
			LOAN_COM_DAY,
			LOAN_INFLOW,
			LOAN_OUTFLOW,
			AUM_BAL,
			AUM_COM_DAY,
			FUND_AMT,
			INSURE_AMT,
			PRECIOUS_METAL,
			CUST_ADD,
			PB_CUST_ADD,
			DIAMOND_CUST_ADD,
			PLATINUM_CUST_ADD,
			GOLD_CUST_ADD,
			NORMAL_CUST_ADD
		 FROM 
		 	`page_perform_summary` 
		 WHERE 
		 	ORG_ID=#{ORG_ID}
		 	AND
		 	DATE_FORMAT(PERFOR_TIME,'%Y-%m-%d')=CURDATE()
		 	AND PERFOR_TYPE=1 
	</select>
```





### 晨会-本日重点关注-今日理财到期客户名单

- **需求**：list表单；客户姓名；性别；产品名称；购买金额；

![](https://i.loli.net/2021/08/02/Rp7K5JiaZDjctsf.png  " ")

- **接口**：`meet/prodOve`
- **涉及表**：`PROD_FINA_INFO`（理财账户信息）；`CUST_BASE_INFO`（客户基本信息）
- **报文**:

```xml
<?xml version="1.0" encoding="utf-8"?>
<trans name="in/meet/prodOve" desc="晨夕会-理财到期">
	<snd>
	</snd>
	<rcv>
		<field name="LIST" type="E" desc="用户列表">
			<field name="CUST_NAME" desc="客户名称" />
			<field name="SEX" desc="客户性别" />
			<field name="PROD_NAME" desc="产品名称" />
			<field name="FINA_AMT" desc="理财金额" />	
		</field>
	</rcv>
</trans>
```

- **流图**：不分页查询
- **Sql**：

```sql
<select id="get" parameterType="map" resultType="map">
        SELECT 
        	A.CUST_NAME,
			B.SEX,
			A.PROD_NAME,
			A.FINA_AMT		
        FROM 
        	PROD_FINA_INFO A
        INNER JOIN
        	CUST_BASE_INFO B
        ON 
        	(A.CUST_NO=B.CUST_NO)
        WHERE      	
        	DATE_FORMAT(A.MATURE_DT,'%Y-%m-%d')=CURDATE()
    </select>
```

{{< admonition  "补充">}}

SQL INNER JOIN 关键字：在两表中存在至少一个匹配时，INNER JOIN 关键字返回行

语法：

```sql
SELECT column_name(s)
FROM table_name1
INNER JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
```

{{< /admonition  >}}

### 晨会-本日重点关注-今日生日客户名单

- **需求**：

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210802102832.png " ")

- **接口**：`meet/birth`
- **报文**：

```xml
<?xml version="1.0" encoding="utf-8"?>
<trans name="in/meet/birth" desc="晨夕会-生日客户">
	<snd>
	</snd>
	<rcv>		
		<field name="LIST" type="E" desc="用户列表">
			<field name="CUST_NAME" desc="客户名称" />
			<field name="SEX" desc="性别" />
			<field name="CUST_LEVEL" desc="客户等级" />
			<field name="AUM" desc="资产" />
		</field>
	</rcv>
</trans>
```





- **涉及表**：`CUST_MAN `（客户管户关系）`CUST_BASE_INFO`（客户基本信息）
- **Sql**：从身份证第7位起始，截取8位数字；利用cast函数转换为日期类型；利用DATE_FORMAT函数规定日期输出格式；选取生日等于当前时间的列

```sql
SELECT 
	A.CUST_NAME,
	B.SEX,
	A.CUST_LEVEL,
	A.AUM
FROM CUST_MAN A
INNER JOIN
	 CUST_BASE_INFO B
ON   (A.CUST_NO=B.CUST_NO)
WHERE DATE_FORMAT(CAST(SUBSTRING(A.CERT_NO,7,8) AS DATE), '%m-%d')
	  =DATE_FORMAT(NOW(),'%m-%d')
```

{{< admonition  "补充">}}

`substring`函数：==从特定位置开始，返回一个子字符串==

- substring(string,position) 从给定位置开始返回后面的子字符串
- substring(string,position,lenth) 从给定位置开始返回指定长度的子字符串

`position`：起始位置，如果 `position`是`0`，则返回一个空字符串

`lenth`:截取长度

例：SUBSTRING(A.CERT_NO,7,8)---20210802



`CAST`函数:==将某种数据类型的表达式显式转换为另一种数据类型==

语法：CAST (expression AS data_type)

- expression：任何有效的SQLServer表达式
- AS：分隔两个参数，在AS之前的是要处理的数据，在AS之后是要转换的数据类型
- data_type：目标系统所提供的数据类型，包括bigint和sql_variant，不能使用用户定义的数据类型。

|            数据类型            | data_type |
| :----------------------------: | :-------: |
| 二进制（同带binary前缀的效果） |  BINARY   |
|       字符型（可带参数）       |  CHAR()   |
|              日期              |   DATE    |
|              时间              |   TIME    |
|           日期时间型           | DATETIME  |
|              整数              |  SIGNED   |
|           无符号整数           | UNSIGNED  |

{{< /admonition  >}}



### 晨会-本日重点关注-今日还款客户名单

- **需求**：

![image-20210802152423223](https://gitee.com/cao-lianjie/pic-go/raw/master/img/image-20210802152423223.png " ")

- **接口**：meet/repay
- **涉及表**：`PROD_LOAN_REPAY`（贷款还款）；`CUST_BASE_INFO`（客户基本信息）
- **报文**：

```xml
<?xml version="1.0" encoding="utf-8"?>
<trans name="in/meet/repay" desc="晨夕会-今日还款">
	<snd>
	</snd>
	<rcv>
		<field name="LIST" type="E" desc="列表">		
			<field name="CUST_NAME" desc="客户姓名" />
			<field name="SEX" desc="性别" />
			<field name="PROD_TYPE" desc="产品类型" />
			<field name="REPAY_AMT" desc="还款金额" />
			<field name="MANAGER_ID" desc="客户经理职位" />
			<field name="ORG_ID" desc="所属机构" />		
		</field>
	</rcv>
</trans>
```

- **Sql**:

```sql
<select id="get" parameterType="map" resultType="map">
        SELECT 
        	A.CUST_NAME,
			B.SEX,
			A.PROD_TYPE,
			A.REPAY_AMT,
			A.MANAGER_ID,
			A.ORG_ID
        FROM 
        	PROD_LOAN_REPAY A
        INNER JOIN
        	CUST_BASE_INFO B
        ON 
        	(A.CUST_NO=B.CUST_NO)
        WHERE      	
        	DATE_FORMAT(A.REPAY_DT,'%Y-%m-%d')=CURDATE()
    </select>
```



### ==大额异动名单==

- **需求**：

![image-20210802153410336](https://gitee.com/cao-lianjie/pic-go/raw/master/img/image-20210802153410336.png " ")

- **接口**：meet/largeChance
- **涉及表**：`CUST_LARGE_AMT_CHANGE`（客户大额变动）；`CUST_BASE_INFO_ES`（ES客户宽表信息）
- **报文**：

```xml
<?xml version="1.0" encoding="utf-8"?>
<trans name="in/meet/largeChance" desc="晨夕会-客户大额异动">
	<snd>
	</snd>
	<rcv>
		<field name="LIST" type="E" desc="列表">
			<field name="CUST_NAME" desc="客户姓名" />
			<field name="SEX" desc="性别" />
			<field name="CHANCE_NUM" desc="变动笔数" />
			<field name="MANAGER_ID" desc="客户经理职位" />
			<field name="MANAGER_ORG" desc="管户机构" />			
		</field>
	</rcv>
</trans>
```



- **Sql**:

```sql
<select id="get" parameterType="map"resultType="map">				
		SELECT 
			B.CUST_NAME,
			B.SEX,	
			B.MANAGER_ID,
			B.MANAGER_ORG,
			A.E CHANCE_NUM
        FROM 	
        	CUST_BASE_INFO_ES B //CUST_LARGE_AMT_CHANGE
		JOIN
			(SELECT
				cust_no,
				count(*) e 
			FROM 
				CUST_TRAN_DETAIL  ？
			WHERE
				DATE_FORMAT(TRAN_TIME,'%Y-%m-%d')=
				DATE_SUB(CURDATE(),INTERVAL 1 DAY)
			GROUP BY
				cust_no) A    
		on
        	A.CUST_NO=B.CUST_NO
	</select>
```



### 贷款逾期名单

- **需求**：

![image-20210802171344777](https://gitee.com/cao-lianjie/pic-go/raw/master/img/image-20210802171344777.png " ")

- **接口**：meet/loanOve

- **涉及表**：`PROD_LOAN_INFO`（贷款产品信息） `CUST_BASE_INFO`（客户基本信息）

- **报文**：

```xml
<?xml version="1.0" encoding="utf-8"?>
<trans name="in/meet/loanOve" desc="晨夕会-贷款逾期">
	<snd>
	</snd>
	<rcv>
		<field name="LIST" type="E" desc="列表">
            
			<field name="CUST_NAME" desc="客户姓名" />
			<field name="SEX" desc="性别" />
			<field name="PROD_NAME" desc="产品类型" />
			<field name="OVERDUE_AMT" desc="逾期金额" />
			<field name="OVERDUE_DAYS" desc="逾期天数" />
			<field name="MANAGER_ID" desc="客户经理职位" />
			<field name="ORG_ID" desc="所属机构" />
		
		</field>
	</rcv>
</trans>
```



- **Sql**：

```sql
<select id="get" parameterType="map" resultType="map">
        SELECT 
        	A.CUST_NAME,
			B.SEX,
			A.PROD_NAME,
			A.OVERDUE_AMT,
			A.OVERDUE_DAYS,
			A.MANAGER_ID,
			A.ORG_ID
        FROM 
        	PROD_LOAN_INFO A
        INNER JOIN
        	CUST_BASE_INFO B
        ON 
        	(A.CUST_NO=B.CUST_NO)
        WHERE
        	(A.OVERDUE_DAYS > 0)
	</select>
```



## 客户360视图

### 查询客户基本信息

- **需求**：

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210803092553.png " ")



- **涉及表**：`CUST_BASE_INFO `（客户基本信息）；`CUST_BASE_INFO_ES`(ES客户宽表信息)
- **报文**：

```xml
<?xml version="1.0" encoding="utf-8"?>
<trans name="in/view/base" desc="视图-用户基本信息">
	<snd>
		<field name="CUST_NO" desc="客户号" required="true" />
	</snd>
	<rcv>
		<field name="Birthday" desc="客户出生日期" />
		<field name="AGE" desc="年龄" />
		<field name="MOBILE_PHONE" desc="手机号" />
		<field name="CUST_GROW_LEVEL" desc="用户成长等级" />
		<field name="CUST_SAFE_LEVEL" desc="用户安全认证等级" />
		<field name="CUST_SCOURCE" desc="客户来源" />
		<field name="ESTAB_CHANNEL" desc="建立渠道" />
		<field name="ESTAB_DT" desc="建立日期" />
		<field name="INTRO_YEAR" desc="引入年限" />
		<field name="IF_OURBNK_EMP" desc="是否本行员工" />
		<field name="FANMILY_ADDR1" desc="家庭地址1" />
		<field name="FANMILY_ADDR2" desc="家庭地址2" />
		<field name="COMPANY_NAME" desc="单位名称" />
		<field name="COMPANY_ADDR" desc="单位地址" />
		<field name="COMPANY_PHONE" desc="单位电话" />
		<field name="JOB_POST" desc="职务" />
		<field name="HIGHEST_EDU" desc="最高学历" />
		<field name="RECENT_CONTACT_TIME" desc="最近联系时间" />
		<field name="MANAGER_ID" desc="管户经理" />
		<field name="MANAGER_ORG" desc="管户机构" />
		<field name="CO_MANAGER_ID" desc="协办经理" />
		<field name="CO_MANAGER_ORG" desc="协办机构" />
	</rcv>
</trans>
```

- **接口**：`view/base`

- **Sql**

```sql
<select id="get" parameterType="map" resultType="map">		 
	SELECT 	
		DATE_FORMAT(CAST(SUBSTRING(A.CERT_NO,7,8) AS DATE), '%Y-%m-%d') Birthday,    
		A.AGE,
		A.MOBILE_PHONE,
		A.CUST_GROW_LEVEL,
		A.CUST_SAFE_LEVEL,
		A.CUST_SCOURCE,
		A.ESTAB_CHANNEL,
		A.ESTAB_DT,
		A.INTRO_YEAR,
		A.IF_OURBNK_EMP,
		A.FANMILY_ADDR1,
		A.FANMILY_ADDR2,
		A.COMPANY_NAME,
		A.COMPANY_ADDR,
		A.COMPANY_PHONE,
		A.JOB_POST,
		A.HIGHEST_EDU,	
		B.RECENT_CONTACT_TIME,
		B.MANAGER_ID,
		B.MANAGER_ORG,
		B.CO_MANAGER_ID,
		B.CO_MANAGER_ORG				
	FROM 
        CUST_BASE_INFO A
    JOIN
        CUST_BASE_INFO_ES B
    ON
        A.CUST_NO=B.CUST_NO
    WHERE
        A.CUST_NO=#{CUST_NO}
</select>
```



### ==客户画像==

- **需求**：

![image-20210803104240231](https://gitee.com/cao-lianjie/pic-go/raw/master/img/image-20210803104240231.png " ")

- **涉及表**：`CUST_LABEL_DETAIL`（客户标签，包括标签信息、客户画像、风险等级）
- **报文**：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<trans desc="视图-查看客户标签" name="in/view/tag">
  <snd>
    <field name="CUST_NO" desc="客户号" required="true"/>
    <field name="LABEL_TYPE" desc="标签类型" required="true" comment="L1客户标签/L2客户画像/L3风险等级"/>
  </snd>
  <rcv>
    <field name="LIST" desc="列表" type="E">
      <field name="LABEL_ID" desc="标签ID"/>
      <field name="LABEL_NAME" desc="标签名称"/>
      <field name="LABEL_VALUE" desc="标签值"/>
    </field>
  </rcv>
</trans>
```

- **接口**：`view/tag`
- **Sql**：

```sql
<select id="get" parameterType="map" resultType="map">		 
		SELECT 	
			LABEL_ID,
			LABEL_NAME,
			LABEL_VALUE
		FROM 
        	CUST_LABEL_DETAIL
        WHERE      	
        	CUST_NO=#{CUST_NO}
        AND
        	LABEL_TYPE=#{LABEL_TYPE}
         --	LABEL_TYPE=L2(L2客户画像)
	</select>
```

### 客户标签-自定义标签

- **需求**：

![image-20210803110226917](https://gitee.com/cao-lianjie/pic-go/raw/master/img/image-20210803110226917.png " ")

- **涉及表**：`CUST_DEF_LABEL`(客户自定义标签)
- **报文**：

```xml
<?xml version="1.0" encoding="utf-8"?>
<trans name="in/view/defTag" desc="视图-自定义标签">
	<snd>
		<field name="CUST_NO" desc="客户号" required="true" />
		<field name="CREATED_BY" desc="创建者" required="true" />
		<field name="LABEL_INFO" desc="标签信息" required="true" />
	</snd>
	<rcv>
	</rcv>
</trans>
```

- **接口**：`view/defTag`
- **Sql**：

```sql
<insert id="set">
	insert into CUST_DEF_LABEL 
	values (#{CUST_NO},CUST_NAME,#{LABEL_INFO},#{CREATED_BY},now())
</insert>
```

### 积分概览

- **需求**：

![image-20210803111423274](https://gitee.com/cao-lianjie/pic-go/raw/master/img/image-20210803111423274.png " ")

- **涉及表**：`CUST_POINT_DETAIL`(客户积分明细)
- **报文**：

```xml
<trans desc="视图-查看积分" name="in/view/point">
    
  <snd>
    <field name="CUST_NO" desc="客户号" required="true"/>
    <field name="POINT_STATUS" desc="积分状态" required="false" comment="不输入显示全部；1正常/2已用/3到期；其他为空"/>
  </snd>
    
  <rcv>
    <field name="ALL_POINT" desc="全部积分"/>
    <field name="OVE_POINT" desc="本月将过期积分"/>
    <field name="LIST" desc="列表" type="E">
      <field name="POINT_TYPE" desc="积分类型"/>
      <field name="BIZ_TIME" desc="有效日期"/>
      <field name="EVENT_DESC" desc="到期日期"/>
      <field name="EVENT_TYPE" desc="积分值"/>
    </field>
  </rcv>
    
</trans>
```

- **流图**：

![image-20210803112146844](https://gitee.com/cao-lianjie/pic-go/raw/master/img/image-20210803112146844.png " ")

- **接口**：`view/point`

- **Sql**:

```sql
<select id="geta" parameterType="map" resultType="map">		 
	SELECT sum(event_type) ALL_POINT 
	FROM cust_point_detail 
	WHERE POINT_STATUS=1 
	AND CUST_NO=#{CUST_NO} ;
</select>
	
<select id="getb" parameterType="map" resultType="map">		 	
	SELECT sum(event_type) OVE_POINT 
	FROM cust_point_detail 
	WHERE POINT_STATUS=1 
	AND CUST_NO=#{CUST_NO} 
	AND (DATE_FORMAT(EVENT_DESC,'%y-%m')=DATE_FORMAT(CURTIME(),'%y-%m'))
</select>
	
<select id="get" parameterType="map" resultType="map">		 
	SELECT 	
		POINT_TYPE,
		BIZ_TIME,
		EVENT_DESC,
		EVENT_TYPE
	FROM 
        CUST_POINT_DETAIL
    WHERE
        CUST_NO=#{CUST_NO}  
    AND       
        POINT_STATUS LIKE (IF (0&lt;#{POINT_STATUS}&lt;4,#{POINT_STATUS},'%%'))
</select>
```







```
IF ( 0< #{POINT_STATUS}< 4,   #{POINT_STATUS} , '%%' )
```






