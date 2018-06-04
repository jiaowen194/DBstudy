# mysql之explain详解（分析索引的最佳使用）

## 查询语句

```sql
explain 
		select pi.id invoice_id,pw.id id ,pw.order_id,ac.car_number,pw.actual_freight,pw.owner_type,
		(case WHEN mm.company_auth_status = 1 
			then (select company_name from a_company where member_id=pw.owner_id LIMIT 1) 
			when mm.personal_auth_status =1 
			then (select name from a_person where member_id=pw.owner_id LIMIT 1) 
			ELSE ' ' end) real_name

		from p_waybill pw
		left JOIN p_invoice pi on pi.id = pw.invoice_id
		left JOIN m_member mm on mm.id = pw.owner_id
		left join a_car ac on ac.id = pw.car_no
```
 
## 结果

![image](https://github.com/jiaowen194/DBstudy/blob/master/20180604.png)


## 详解

### type详细的介绍

* all     全表扫描
* index   按索引次序扫描，先读索引，再读实际的行，结果还是全表扫描，主要优点是避免了排序。因为索引是排好的。
* range   以范围的形式扫描
* ref     非唯一索引访问(只有普通索引)
* eq_ref  使用唯一索引查找(主键或唯一索引)
* const   常量查询
* system  系统查询 
* null    优化过程中就已经得到结果，不在访问表或索引

### possible_keys：可能用到的索引

### key:实际用到的索引

### key_line:索引字段最大可能使用长度

### ref ：
指出对 key 列所选择的索引的查找方式，常见的值有 const, func, NULL, 具体字段名。当 key 列为 NULL ，即不使用索引时，此值也相应的为 NULL 。

### rows :估计需要扫描的行数

### Extra　:显示以上信息之外的其他信息
* Using index 此查询使用了覆盖索引(Covering Index)，即通过索引就能返回结果，无需访问表。
* Using where 表示 MySQL 服务器从存储引擎收到行后再进行“后过滤”（Post-filter）。所谓“后过滤”，就是先读取整行数据，再检查此行是否符合 where 句的条件，符合就留下，不符合便丢弃。因为检查是在读取行后才进行的，所以称为“后过滤”。
* Using temporary 使用到临时表


