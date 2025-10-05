

<!-- Database create query -->

CREATE DATABASE task_manager;



<!-- USER TABLE CREATE QUERY  -->

CREATE TABLE users(
id INT PRIMARY KEY AUTO_INCREMENT,
name VARCHAR(68) NOT NULL,
email VARCHAR(128) NOT NULL UNIQUE,
created_at DATE

);



<!-- CREATE TASKS TABLE QUERY  -->

CREATE TABLE tasks(
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    title VARCHAR(128),
    description VARCHAR(268),
    status BOOLEAN DEFAULT FALSE,     <!-- KEEP STATUS TO DEFAULT FALSE(0) SO THAT WE CAN UPDATE STATUS LATTER-->
    created_at DATE,
    FOREIGN KEY (user_id) REFERENCES users(id);   <!-- DECLARING FOREIGN KEY FOR MAINTAINING RELATIONSHIP BETWEEN USER AND TASK TABLE.TASK TABLE USER ID IS MAINTAINING  
                                                  RELATIONSHIP TO USER TABLE ID .Each user can have multiple task (one to many Relationship) -->
)



<!-- INSERT MULTIPLE USER IN USER TABLE -->


INSERT INTO users(`name`,`email`,`created_at`)VALUES
('Sohan','sohan@mail.com','29-09-20025'),
('Fahim','fahim@mail.com','30-09-20025'),
('Saeem','saeem@mail.com','01-10-20025');





<!-- INSERT MULTIPLE TASKS AGAINST ONE USER  -->

INSERT INTO tasks(`user_id`,`title`,`description`,`created_at`)VALUES
(1,'Gaming','Paticipate in a gaming event','07-10-2025'),
(1,'Football','Football match','08-10-2025'),
(1,'Travelling','Start travelling','09-10-2025'),
(2,'Study','Group study','10-10-2025'),
(2,'Debate','Particapte in a debating event','11-10-2025'),
(2,'Exam','Proggamming test exam','12-10-2025'),
 (3,'Music','Music competition','13-10-2025'),
 (3,'Movie','Watching movie in theatre','14-10-2025'),
 (3,'Adventure','Serching for mysterious thing in a jungle','15-10-2025');






<!-- INSERT SOME ADDITIONAL USERS SO THAT CAN UNDERSTAND JOINING BETWEEN  USERS AND TASKS TABLE -->


INSERT INTO users(`name`,`email`,`created_at`)VALUES
('Wahid','wahid@mail.com','25-09-2025'),
('Nahid','nahid@mail.com','24-09-2025'),
('Sahid','sahid@mail.com','22-09-2025');





<!-- Joining users and tasks table from task_manager database (INNER JOIN,LEFT JOIN, RIGHT JOIN ) -->


<!-- INNER JOIN (Show only common data from users and tasks table ) -->

SELECT users.name,users.email,tasks.user_id,tasks.title,tasks.description,tasks.status,tasks.created_at FROM users INNER JOIN tasks ON users.id= tasks.user_id;





<!-- LEFT JOIN (In LEFT JOIN  Its depends on which table on left side in query.I put user table in left side in query thats why it will show all data from user table where user table have extra data but no data in task table against user tables extra data .It will show tasks table data as null against user tables extra data . In LEFT JOIN ,it will show all data from left table and from right table it will show only data which data is connected to left table.If there is no data it will show null.) -->


SELECT users.name,users.email,tasks.user_id,tasks.title,tasks.description,tasks.status,tasks.created_at FROM users LEFT JOIN tasks ON users.id= tasks.user_id;





<!-- What will happend if i put user table in right side and tasks table in left side  in LEFT JOIN ?-->

<!-- it will  show all data from task table and show only data from user table which is connected to task table.It will not showing all data from user table if i put user table in right side in LEFT JOIN.Extra data from users table will not showing this time   -->


SELECT users.name,users.email,tasks.user_id,tasks.title,tasks.description,tasks.status,tasks.created_at FROM tasks LEFT JOIN users ON users.id= tasks.user_id;






<!-- RIGHT JOIN (In RIGHT JOIN  Its depends on which table on right  side in query.I put users table in right side in query thats why it will show all data from users table where users table have extra data but no data in task table against user tables extra data .It will show tasks table data as null against user tables extra data . In RIGHT JOIN ,it will show all data from RIGHT table and from LEFT table it will show only data which data is connected to left table.If there is no data it will show null.) -->


SELECT users.name,users.email,tasks.user_id,tasks.title,tasks.description,tasks.status,tasks.created_at FROM tasks RIGHT JOIN users ON users.id= tasks.user_id;





<!-- What will happend if i put user table in left side and tasks table in right side  in RIGHT JOIN ?-->

<!-- it will  show all data from task table and show only data from user table which is connected to task table.It will not showing all data from user table if i put user table in left side in RIGHT JOIN.Extra data from users table will not showing this time  -->


SELECT users.name,users.email,tasks.user_id,tasks.title,tasks.description,tasks.status,tasks.created_at FROM users RIGHT JOIN tasks ON users.id= tasks.user_id;




<!-- SELECT ALL TASKS QUERY -->

SELECT * FROM `tasks`;


<!-- Update all tasks status to 1 -->

UPDATE `tasks` SET status=1; 



<!-- UPDATE TASK STATUS USING id -->
UPDATE `tasks` SET status=0 WHERE id=2;



<!-- UPDATE TASK STATUS USING user_id -->

UPDATE `tasks` SET status=0 WHERE user_id=3;



<!-- SORTING TASK IN DESCENDING ORDER BY ID -->

SELECT * FROM `tasks` ORDER BY id DESC;



<!-- SORTING TASK IN DESCENDING ORDER BY user_id -->

SELECT * FROM `tasks` ORDER BY user_id DESC;



<!-- Sorting tasks in ascending order by status -->

SELECT * FROM `tasks` ORDER BY status ASC LIMIT 4;


<!-- Sorting tasks in descending order by status and using limit to  how many task i want to show  -->

SELECT * FROM `tasks` ORDER BY status DESC LIMIT 5;





<!-- Pagination  -->]

<!-- in first page 4 task will be showed and  in second page skip 4 task   -->

<!-- Descending order -->
SELECT * FROM `tasks` ORDER BY id DESC LIMIT 4;  <!-- First page-->

SELECT * FROM `tasks` ORDER BY id DESC LIMIT 4 OFFSET 4;  <!-- Second page-->




<!-- Ascending oder  -->

SELECT * FROM `tasks` ORDER BY id LIMIT 4 ;  <!-- First page-->

SELECT * FROM `tasks` ORDER BY id LIMIT 4 OFFSET 4; <!-- Second page-->
 



 <!-- Query to check How many tasks each user has  -->

 SELECT COUNT(id) FROM tasks GROUP BY user_id;



<!-- Using aggregator function to find maximum id  -->

SELECT MAX(id) FROM tasks;



<!-- Using aggregator function to find minimum id  -->

SELECT MIN(id) FROM `tasks`;



<!-- AVERAGE -->

SELECT AVG(id) FROM `tasks` WHERE id>3;

SELECT AVG(user_id) FROM `tasks`;




<!-- SUM -->

SELECT SUM(id) FROM `tasks`;

SELECT SUM(user_id) FROM `tasks` WHERE id>5;



<!-- DELETE a tasks  -->

DELETE FROM `tasks` WHERE id=9;
