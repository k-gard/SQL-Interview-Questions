## Twitter
### Hard
![enter image description here](https://doc-0g-0s-docs.googleusercontent.com/docs/securesc/7aitodldkm0fuvap891ijbakis79h4q7/a9qhrongn3i6tjq8n9ja34itr79qa7ra/1616396625000/14652307635308192399/14652307635308192399/1RYN-0QdxNnVIhYg3kF3Koo9CIxkrGJJK?authuser=0&nonce=moe0bkqjjuhnu&user=14652307635308192399&hash=8mhmdglnq0jmgdq3d2f1bj671fe92iiu)

```sql
select E.department,first_name,salary
from Employee E
join 
(select department,max(salary) S from Employee E group by department ) A
on E.salary = A.S


