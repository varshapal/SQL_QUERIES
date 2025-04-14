# SQL_QUERIES
LeetCode SQL Queries 

# 1 - Delete Duplicate Emails: 
- Write a solution to delete all duplicate emails, keeping only one unique email with the smallest id.
# Solution:
- DELETE p1 FROM person p1, person p2
  WHERE p1.email = p2.email AND p1.id > p2.id;
  

# 2 - Movie Rating:
- Find the name of the user who has rated the greatest number of movies. In case of a tie, return the lexicographically smaller user name.
- Find the movie name with the highest average rating in February 2020. In case of a tie, return the lexicographically smaller movie name.
  
# Solution:
- (SELECT u.name results FROM movierating mr
  JOIN users u
  ON u.user_id = mr.user_id
  GROUP BY mr.user_id
  ORDER BY COUNT(mr.user_id) DESC, u.name
  LIMIT 1)

  UNION ALL

  (SELECT m.title results FROM movierating mr
  JOIN movies m
  ON m.movie_id = mr.movie_id
  WHERE mr.created_at LIKE '2020-02-%'
  GROUP BY mr.movie_id
  ORDER BY AVG(mr.rating) DESC, m.title
  LIMIT 1);

# Explanation:
- First create a query for name of user who has rated the greatest number of movie, Select the name from users table and join the movierating table with user_id because user_id is common column name in both(users and movierating) table. Group by user_id, use order by with Count(mr.user_id) in decending order and name in ascending order, Limit 1 will display only 1 record.
- Create Second query for the movie name which have highest average rating in February 2020. Select the title from movie table join the movierating table with movie_id because movie_id is common column in both table. Use Where clause with LIKE for Feburary 2020, group by movie_id, order by average rating in descending order and title in ascending order, LIMIT 1 display only 1 record.
- USE union all with both query for getting both query result together.


# 3- Consecutive Numbers:   
  - Find all numbers that appear at least three times consecutively.

# Solution:
  - WITH cte AS (
    SELECT num,
    LEAD(num, 1) OVER(ORDER BY id) AS next_num,
    LEAD(num, 2) OVER(ORDER BY id) AS next2_num
    FROM logs
  )

    SELECT Distinct num consecutiveNums FROM cte
    WHERE num = next_num AND num = next2_num;

# Explanation:
  - First create Common Table Expression cte with window function lead,
  - First lead give the num 1 row ahead
  - Second lead give the num 2 row ahead.
  - Select query find distinct num from cte where nu is equal to next_num and next2_num.
