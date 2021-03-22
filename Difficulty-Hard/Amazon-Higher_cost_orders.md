## Amazon
### Hard

![Higher-cost-orders](https://drive.google.com/uc?id=1GOfOHSdImGXVdN-6eCfuPcXP8OubLU4Z)

```sql
With OrdersCost as  (Select cust_id,
			    order_date,
			    sum(totalOrderCost) totalCost
                     from (select cust_id,
		     		  order_date,
                                  order_quantity * order_cost as totalOrderCost
			   from Orders) A
                     where order_date >= '2019-02-01' and order_date <= '2019-05-01'
                     group by cust_id,order_date  
                     order by cust_id,order_date
		    )

select first_name,
       order_date,
       maxUserOrder 
from (select cust_id,
	     max(totalCost) maxUserOrder
      from OrdersCost
      group by cust_id) A
      inner join
      OrdersCost O
      on A.cust_id = O.cust_id and A.maxUserOrder= totalcost
      inner join
      customers C
      on O.cust_id = C.id
where totalcost = (select max(totalCost) from OrdersCost)

