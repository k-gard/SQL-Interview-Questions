## Airbnb
### Hard

![enter image description here](https://drive.google.com/uc?id=1dl0YH96f76nnv3fv4gWJKMWkG9HZ90I8)

```sql
with Hosts as (
select concat(price, room_type, host_since, zipcode, number_of_reviews) host_id
	   ,price,
        case when number_of_reviews = 0 then 'New'
             when number_of_reviews >= 1 and number_of_reviews <= 5 then 'Rising'
             when number_of_reviews >= 6 and number_of_reviews <=15 then 'Trending Up'
             when number_of_reviews >= 16 and number_of_reviews <= 40 then 'Popular'
             else 'Hot' end as Rating
from airbnb_host_searches
order by number_of_reviews desc)

 select rating,min(price),avg(price),max(price) 
 from (select Distinct Host_id,price,rating from Hosts) a
 group by rating


