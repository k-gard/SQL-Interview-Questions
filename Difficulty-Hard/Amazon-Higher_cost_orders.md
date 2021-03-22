## Amazon
### Hard

![Higher-cost-orders](https://doc-14-0s-docs.googleusercontent.com/docs/securesc/7aitodldkm0fuvap891ijbakis79h4q7/04f1ga8jg8lmsde9uuf8fig2anqvt3v7/1616396250000/14652307635308192399/14652307635308192399/1GOfOHSdImGXVdN-6eCfuPcXP8OubLU4Z?authuser=0&nonce=ra9i08dsadvcg&user=14652307635308192399&hash=u1uj14qrbe63kltgmonl0p1dbjaa9b5m)

```sql
With OrdersCost as  (
					 Select cust_id,
							order_date,
							sum(totalOrderCost) totalCost
                     from (select cust_id,
								  order_date,
                                  order_quantity * order_cost totalOrderCost
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

