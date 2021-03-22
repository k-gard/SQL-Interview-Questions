## Twitter
### Hard
![enter image description here](https://drive.google.com/uc?id=1RYN-0QdxNnVIhYg3kF3Koo9CIxkrGJJK)

```sql
select E.department,first_name,salary
from Employee E
join 
(select department,max(salary) S from Employee E group by department ) A
on E.salary = A.S


