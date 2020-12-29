## What the databse all about?

It is a SQL Sample Database called HR that manages the HR data of the small businesses. The database consists of multiple related tables e.g., employees, departments, jobs, etc. This database are used by to store personal information relating to their employees. Below we will be showing the ERD Diagram as a presentation of the connection between entities, as well as the entity names and descriptions.


### Entity Relationship Diagram

ER Digram shows how our entities relate to each other within a system.

![image](https://github.com/biancacortez/HRdatabase/blob/main/img/ERD.PNG)

### Table Names and Description
1. The HR sample database has seven tables.
2.	The employees table stores the data of employees.
3.	The jobs table stores the job data including job title and salary range.
4.	The departments table stores department data.
5.	The dependents table stores the employee’s dependents.
6.	The locations table stores the location of the departments of the company.
7.	The countries table stores the data of countries where the company is doing business.
8.	The regions table stores the data of regions such as Asia, Europe, America, and the Middle East and Africa. The countries are grouped into regions.

### HR Database Dependency Diagram
The picture below defines the relationship between attributes.

![image](https://github.com/biancacortez/HRdatabase/blob/main/img/FDD.PNG)

### Source
The sample data can be download [here.](https://www.sqltutorial.org/what-is-sql/)

#### Here are some list of queries with their ouput.
   i. **`Query 1: `**
     INNER JOIN: An inner join will combine rows from different tables if the join condition is true.
   
       ```SQL
         DELIMITER //
         
         
         SELECT
            employees.employee_id,
            employees.first_name,
            employees.last_name,
            departments.department_id,
            departments.department_name
        FROM
            departments
        JOIN employees ON departments.department_id = employees.department_id //

         DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/5.PNG)
   Importance: It is important and useful when you want to retrieved data by combining column values of two table.
   
   ii. **`Query 2: `**
     RIGHT JOIN: The RIGHT JOIN keyword returns all records from the right table (table2), and the matched records from the left table (table1).
   
       ```SQL
         DELIMITER //
         
         SELECT
          locations.location_id,
          countries.country_id,
          countries.country_name
      FROM
          locations
      RIGHT JOIN countries ON countries.country_id = countries.country_id
      ORDER BY
          locations.location_id;

         DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/rightjoin.PNG)
   Importance: The use RIGHT OUTER JOIN is to try to make your SQL more self-documenting. 
   
   iii. **`Query 3: `**
     ORDER BY: This is used along with the select statement to sort the results either in ascending order or descending order. 
   
       ```SQL
         DELIMITER //
         
         
         SELECT * FROM jobs
         ORDER BY max_salary ASC, min_salary DESC;

         DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/1.PNG)
   Importance: Used to sort the result-set in ascending or descending order.
   
   iv. **`Query 4: `**
     NULL: A field with a NULL value is a field with no value, but a NULL values also indicate that you could have a value but don’t know what value should be yet.
   
       ```SQL
         DELIMITER //
                 
         SELECT first_name, last_name,phone_number
         FROM employees
         WHERE phone_number IS NULL;

         DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/2.PNG)
   Importance: This query can help you especially when every field in a table should have a value.
   
   v. **`Query 5: `**
     LIKE: This operator is used to compare between the two conditions and lists down all the rows of a table whose column name matches the pattern specified with the LIKE clause.
   
       ```SQL
         DELIMITER //
                 
      SELECT
          last_name,
          first_name
      FROM
          `employees`
      WHERE
          last_name LIKE 'C%';

         DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/4.PNG)
   Importance: Used in where cluase to search for a specified pattern in a column.
   
   vi. **`Query 6: `**
     DENSE_RANK(): It is an analytic query that computes the rank of a row in an arranged collection of rows.
   
       ```SQL
         DELIMITER //
                 
       SELECT
          job_title,
          max_salary,
          DENSE_RANK() OVER(
          PARTITION BY max_salary
       ORDER BY
          job_title
         ) AS ranking
       FROM
          jobs;

         DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/a5.PNG)
   Importance: It calculates the rank of a row in an ordered set of rows.
   
   vii. **`Query 7: `**
     CASE: The CASE statement goes through conditions and returns a value when the first condition is met (like an IF-THEN-ELSE statement).
   
       ```SQL
         DELIMITER //
                 
      SELECT
          region_id,
          region_name,
          CASE WHEN region_name = 'Europe' THEN 'Bonjour!'
               WHEN region_name = 'Americas' THEN 'Hey?' 
               WHEN region_name = 'Asia' THEN 'Hello!'
               ELSE 'MArhaba'
      END AS mylanguage
      FROM
          regions;

         DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/a6.PNG)
   Importance: The CASE statement is used to retrieve data based on a few conditions. 
   
   viii. **`Query 8: `**
     UNION: query is to combine the results of two queries together while removing duplicates.
   
       ```SQL
         DELIMITER //
                 
      SELECT country_id FROM countries
      UNION
      SELECT country_id FROM locations;

         DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/7.PNG)
   Importance: It removes duplicate rows between the various SELECT statements. 
          
   ix. **`Query 9: `**
     JOINS :combines columns from one or more tables in a relational database.
   
       ```SQL
         DELIMITER //
                 
      SELECT 
         employees.first_name , employees.last_name , 
         employees.department_id , departments.department_name 
      FROM employees  
      JOIN departments  
        ON employees.department_id = departments.department_id;

         DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/8.PNG)
   Importance: Can be use when we combine fields from different tables bu using common values.  
   
   x. **`Query 10: `**
     SUBQUERY: A subquery is a query that is nested inside a SELECT , INSERT , UPDATE , or DELETE statement, or inside another subquery. 
   
       ```SQL
         DELIMITER //
                 
      SELECT
          first_name
      FROM
          employees
      WHERE
          department_id IN(
          SELECT
              department_id
          FROM
              departments
          WHERE
              location_id IN(
              SELECT
                  location_id
              FROM
                  locations
              WHERE
                  country_id =(
                  SELECT
                      country_id
                  FROM
                      countries
                  WHERE
                      country_name = 'United Kingdom'
              )
          )
      );

         DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/9.PNG)
   Importance: A subquery is used to return data that will be used in the main query as a condition to further restrict the data to be retrieved.
   
xi. **`Query 11: `**
     CONCAT:The CONCAT() function adds two or more strings together. 
   
       ```SQL
         DELIMITER //
                 
      ALTER TABLE
         locations ADD COLUMN complete_address VARCHAR(50);
      UPDATE
          locations
      SET
          complete_address = CONCAT(
              street_address,
              ', ',
              city,
              ', ',
              state_province
          );

         DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/10.PNG)
   Importance: The CONCAT function implicitly coverts all arguments to string types and then concatenate the inputs.
   
xii. **`Query 12: `**
     Triggers: Help the database designer ensure certain actions, such as maintaining an audit file, are completed regardless of which program or user makes changes to the data. 
   
       ```SQL
         DELIMITER //
                 
      CREATE TRIGGER insert_trigger BEFORE INSERT ON
         locations FOR EACH ROW
      SET NEW
          .complete_address = CONCAT(
              NEW.street_address,
              ', ',
              NEW.city,
              ', ',
              NEW.state_province
          );
      CREATE TRIGGER update_trigger BEFORE UPDATE
      ON
          locations FOR EACH ROW
      SET NEW
          .complete_address = CONCAT(
              NEW.street_address,
              ', ',
              NEW.city,
              ', ',
              NEW.state_province
          );
          DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/11.PNG)
   Importance:  The trigger is mostly used for maintaining the integrity of the information on the database.
   
   xiii. **`Query 13: `**
     CONVERT: The CONVERT() function allows you to convert a value of one type to another. 
   
       ```SQL
         DELIMITER //
                 
      SELECT max_salary, CONVERT (max_salary, INTEGER) rounded_price FROM jobs;
          
          DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/12.PNG)
   Importance:  It is useful because the CONVERT() function converts a value (of any type) into a specified datatype.
   
   xiv. **`Query 14: `**
     RANK: The RANK() function is a window function that assigns a rank to each row within a partition of a result set. 
   
       ```SQL
         DELIMITER //
                 
      SELECT
       employee_id,
       last_name,
       first_name,
       hire_date,
       RANK() over(
      ORDER BY
          hire_date
      ) latest
      FROM
          employees;
          
          DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/13.PNG)
   Importance:  This function is useful in assigning a rank to each row within a partition of a result set.
   
   xv. **`Query 15: `**
     COUNT(): COUNT() returns the number of rows in a specified table, and it preserves duplicate rows.  
   
       ```SQL
         DELIMITER //
                 
      SELECT
          manager_id,   
          COUNT(*)
      FROM
          employees
      GROUP BY
          manager_id;
          
          DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/count.PNG)
   Importance:  It can use when counting datas within the column.
   
  xvi. **`Query 16: `**
     HAVING: A HAVING clause in SQL specifies that an SQL SELECT statement must only return rows where aggregate values meet the specified conditions.  
   
       ```SQL
         DELIMITER //
                 
      SELECT
          job_id,
          AVG(salary)
      FROM
          employees
      GROUP BY
          job_id
      HAVING
          AVG(salary) > 10000
          
          DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/having.PNG)
   Importance:  To view the present condition formed by the GROUP BY clause, the HAVING clause is used.

 xvii. **`Query 17: `**
     NTILE: The NTILE enables users to split a sequence set into a detailed number of relatively similar groups, or containers, rows sanctioning.  
   
       ```SQL
         DELIMITER //
                 
         SELECT
          employee_id,
          first_name,
          last_name,
          job_id,
          salary,
       NTILE(10) OVER(
         ORDER BY
          salary
         ) AS container_no
         FROM
             employees;
          
          DELIMITER ;
       ```
   ### Sample [output.](https://github.com/biancacortez/HRdatabase/blob/main/img/ouput/ntile.PNG)
   Importance:  NTILE() function can be use when assigning a number_expression for every row in a group, to which the row belongs.
