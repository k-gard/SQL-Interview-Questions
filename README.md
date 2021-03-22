# SQL-Interview-Questions
answers to SQL interview questions

## Premium vs Freemium
### Microsoft 
![Premium vs Freemium](https://drive.google.com/uc?id=1U62og3lE5vsHPx5pCeXlIeNZDqq7auz3)

```
select A.date,non_paying ,paying
from   (Select date,sum(downloads) non_paying
        from (Select U.user_id,paying_customer
             from ms_user_dimension as U
             inner join 
             ms_acc_dimension as A
             on U.acc_id=A.acc_id
             where paying_customer = 'no') NPUSERS
        inner join 
             (Select user_id,date,downloads
                from ms_download_facts
             ) NPDNL
        on NPUSERS.user_id = NPDNL.user_id
        group by date
      )A
inner join
       (Select date,sum(downloads) paying
        from (Select U.user_id,paying_customer
              from ms_user_dimension U
              inner join 
              ms_acc_dimension A
              on U.acc_id=A.acc_id
              where paying_customer = 'yes') PUSERS
        inner join
             (Select user_id,date,downloads
                from ms_download_facts
              ) PDNL
        on PUSERS.user_id = PDNL.user_id
        group by date
        )B
on A.date = B.date
where non_paying > paying
order by date asc
```

