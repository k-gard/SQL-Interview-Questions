## Facebook
### Hard
![enter image description here](https://doc-0o-0s-docs.googleusercontent.com/docs/securesc/7aitodldkm0fuvap891ijbakis79h4q7/f22t8f2c6eonms3vhnmhuqnn8tgvpfbv/1616397375000/14652307635308192399/14652307635308192399/1LZW-P6oRNEV2rWTsOWYk4buURCLMPkyr?authuser=0&nonce=645srs0chhggi&user=14652307635308192399&hash=hdig32anni5j6kaqc9ifoopptkghk4jb)

```sql
SELECT USER1,
       CAST(totalfriends AS FLOAT)/
       CAST(totalUsers AS FLOAT)*100 AS popularity_percent
FROM
    (SELECT a.user1,
            totalUsers,
            CASE WHEN A.user1 in (SELECT user1 FROM facebook_friends)         
							   THEN (SELECT count(user2) 
						             FROM facebook_friends
						             WHERE A.user1 =facebook_friends.user1 )
		         ELSE (SELECT count(user1) 
					        FROM facebook_friends 
					        WHERE A.user1 = facebook_friends.user2 )
		    END AS totalfriends
    FROM (SELECT user1
          FROM (SELECT distinct user1 
                FROM facebook_friends) A
                UNION 
                (SELECT distinct user2
                 FROM facebook_friends
                 WHERE user2 NOT IN (SELECT distinct user1 
                                     FROM facebook_friends)
                )
                ORDER BY user1) A
         ,(SELECT count(distinct user2) totalUsers
           FROM facebook_friends)B
          )C

