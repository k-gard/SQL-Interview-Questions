## Facebook
### Hard
![enter image description here](https://drive.google.com/uc?id=1LZW-P6oRNEV2rWTsOWYk4buURCLMPkyr)
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

