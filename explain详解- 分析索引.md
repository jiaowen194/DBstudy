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

[id]: https://github.com/jiaowen194/DBstudy/blob/master/20180604.png  "Optional title attribute"
