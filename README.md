Questionaire
===
 
##### Q1: Knowing what you know about GitHub, how would you design the high level infrastructure for github.com? What sequence of steps would happen when loading http://www.github.com in a browser? Don't worry about describing the specific libraries and services that handle each step.

A1:  
- High level infrastructure design:
  
  - Benefits of using Rackspace / Why is GitHub using Rackspace
  - How does GitHub's infrastruture currently operate?
  - Where is GitHub headed?
  - Capacity
  - How does GitHub's filesystem work?


- Sequence of steps what would happen:


##### Q2: Describe the common components of web application frameworks. What purpose does each component serve? What is the benefit of separating each component from the others?

A2:

##### Q3: Given the following table schema, indexes, and query plan, explain how the query is executed and what you would do to improve the performance.

    mysql> describe ci_statuses;
    +-----------------+--------------+------+-----+---------+----------------+
    | Field           | Type         | Null | Key | Default | Extra          |
    +-----------------+--------------+------+-----+---------+----------------+
    | id              | int(11)      | NO   | PRI | NULL    | auto_increment |
    | state           | varchar(255) | NO   |     | unknown |                |
    | sha             | varchar(255) | NO   | MUL | NULL    |                |
    | repository_id   | int(11)      | NO   | MUL | NULL    |                |
    | created_at      | datetime     | YES  |     | NULL    |                |
    | updated_at      | datetime     | YES  |     | NULL    |                |
    | pull_request_id | int(11)      | YES  | MUL | NULL    |                |
    | context         | varchar(255) | YES  |     | default |                |
    +-----------------+--------------+------+-----+---------+----------------+

    indexes:
    +----------------------------+------------------------------+--------+
    | Index_name                 | Columns                      | Unique |
    +----------------------------+------------------------------+--------+
    | PRIMARY                    | id                           |    1   |
    | sha                        | sha                          |    0   |
    | pull_request_id_created_at | pull_request_id, created_at  |    0   |
    | repository_id_created_at   | repository_id, created_at    |    0   |
    +----------------------------+------------------------------+--------+

    >explain SELECT r.id FROM repositories r JOIN ci_statuses s ON s.repository_id = r.id GROUP BY s.sha HAVING COUNT(s.context) > 1;
    +-------------+-------+--------+--------------------------+---------+---------+-----------------+-----------+--------------------------+
    | select_type | table | type   | possible_keys            | key     | key_len | ref             | rows      | Extra                    |
    +-------------+-------+--------+--------------------------+---------+---------+-----------------+-----------+--------------------------+
    | SIMPLE      | s     | index  | repository_id_created_at | sha     | 767     | NULL            | 122041204 |                          |
    | SIMPLE      | r     | eq_ref | PRIMARY                  | PRIMARY | 4       | s.repository_id |         1 | Using where; Using index |
    +-------------+-------+--------+--------------------------+---------+---------+-----------------+-----------+--------------------------+

    A3:


