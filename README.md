# SQL_QUERIES
LeetCode SQL Queries 

- Delete Duplicate Emails: Write a solution to delete all duplicate emails, keeping only one unique email with the smallest id.
- Solution:
- DELETE p1 FROM person p1, person p2
  WHERE p1.email = p2.email AND p1.id > p2.id;
