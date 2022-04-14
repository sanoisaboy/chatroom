# chatroom
  
  
/*
create database which name chatroom 
*/

CREATE DATABASE IF NOT EXISTS chatroom;

/*
selcet database
*/

SET DATABASE = chatroom;

SHOW DATABASE;

/*create table which name users*/

CREATE TABLE IF NOT EXISTS users (
    id INT PRIMARY KEY,
    user_name varCHAR UNIQUE,
    user_password varCHAR 
);

/*create table which name message*/

CREATE TABLE IF NOT EXISTS messages (
    id INT PRIMARY KEY,
    body TEXT,
    create_at DATE,
    user_id INT
);

/*insert 4 user */
/*
  id | user_name | user_password
-----+-----------+----------------
   1 | Mopeter   | qwe123
   2 | BILL      | asd123
   3 | SAM       | zxc123
   4 | DOGGY     | qaz123
(4 rows)


*/


INSERT INTO users VALUES (1,'Mopeter','qwe123');
INSERT INTO users VALUES (2,'BILL','asd123');
INSERT INTO users VALUES (3,'SAM','zxc123');
INSERT INTO users VALUES (4,'DOGGY','qaz123');


/*insert 4 messages */
/*
  id |       body       | create_at  | user_id
-----+------------------+------------+----------
   1 | find another job | 2015-02-12 |       1
   2 | want to quit     | 2016-04-12 |       1
   3 | find a job       | 2035-12-12 |       2
   4 | Godzilla is God  | 2022-03-12 |       3
(4 rows)
*/

INSERT INTO messages VALUES (1,'find another job','2/12/2015',1 );
INSERT INTO messages VALUES (2,'want to quit','4/12/2016',1);
INSERT INTO messages VALUES (3,'find a job','12/12/2035',2);
INSERT INTO messages VALUES (4,'Godzilla is God','3/12/2022',3);

/*creat one to many relationship from user to messages */
/*
  id |       body       | create_at  | user_id | id | user_name | user_password
-----+------------------+------------+---------+----+-----------+----------------
   1 | find another job | 2015-02-12 |       1 |  1 | Mopeter   | qwe123
   2 | want to quit     | 2016-04-12 |       1 |  1 | Mopeter   | qwe123
   3 | find a job       | 2035-12-12 |       2 |  2 | BILL      | asd123
   4 | Godzilla is God  | 2022-03-12 |       3 |  3 | SAM       | zxc123
(4 rows)

*/

SELECT *
FROM messages
INNER JOIN users ON messages.user_id = users.id;

/* sort the messages by create_at*/
/*
  id |       body       | create_at  | user_id
-----+------------------+------------+----------
   1 | find another job | 2015-02-12 |       1
   2 | want to quit     | 2016-04-12 |       1
   4 | Godzilla is God  | 2022-03-12 |       3
   3 | find a job       | 2035-12-12 |       2
(4 rows)
*/
SELECT * 
FROM messages 
ORDER BY create_at;

/* delete id  which is  4*/

DELETE FROM messages WHERE id in (4);

/* delete table users */
DROP TABLE users;
