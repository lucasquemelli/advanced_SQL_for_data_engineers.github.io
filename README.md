# advanced_SQL_for_data_engineers.github.io
This project covers some advanced SQL techniques that are useful for Data Engineers.

# Views

In SQL, a view is an alternative way of representing data that exists in one or more tables. Just like a real table, it contains rows and columns. The fields in a view are fields from one or more real tables in the database. Though views can be queried like a table, views are dynamic; only the definition of the view is stored, not the data.

The syntax of a CREATE VIEW statement:

![image](https://user-images.githubusercontent.com/81119854/126873821-4f011ff2-9796-40ee-80e6-ef412124338f.png)

The syntax of a REPLACE VIEW statement:

![image](https://user-images.githubusercontent.com/81119854/126873846-325d1f25-16ee-4793-826a-6b335bca6c09.png)

The syntax of a DROP VIEW statement:

![image](https://user-images.githubusercontent.com/81119854/126873868-b4c0f8f5-eca2-4bef-8b2e-7c0755d05129.png)

Exercise 1: Create a View using IBM Db2 on Cloud

![image](https://user-images.githubusercontent.com/81119854/126873919-18577f8c-f751-4493-9ce2-3f5a78abb51c.png)

Using SELECT to query the EMPSALARY view and retrieving all the records:

![image](https://user-images.githubusercontent.com/81119854/126873965-1f0e0259-059f-4e57-8c37-664e85d8a495.png)

![image](https://user-images.githubusercontent.com/81119854/126873983-ce261261-54d8-4fa1-98e7-d6b8a631491b.png)

Exercise 2: Update a View

It now seems that the EMPSALARY view we created in exercise 1 doesn't contain enough salary information, such as max/min salary and the job title of the employees. Let's update the EMPSALARY view:

![image](https://user-images.githubusercontent.com/81119854/126991050-5b5b8cf7-9979-49a8-8059-f99d7eff1d36.png)

We are combining the data of two different tables, EMPLOYEES and JOBS by connecting their respective columns JOB_ID and JOB_IDENT since both the columns contain common unique data.

Using SELECT, we may query the updated EMPSALARY view to retrieve all the records:

![image](https://user-images.githubusercontent.com/81119854/126991473-bd5bab4a-125a-47c6-8ce4-437d418b724c.png)

![image](https://user-images.githubusercontent.com/81119854/126991516-4bba85f0-bcbd-47ad-bfed-f8bce19b69f7.png)

Exercise 3: Drop a View

![image](https://user-images.githubusercontent.com/81119854/126991777-7e66f5a0-8927-4409-9703-7cb9891fb967.png)

Using SELECT, we can verify whether the EMPSALARY view has been deleted or not. 

![image](https://user-images.githubusercontent.com/81119854/126991932-b9940003-a66d-45cf-8c37-dfd233e9ef18.png)

# Stored Procedures 

A stored procedure is a set of SQL statements that are stored and executed on the database server. So instead of sending multiple SQL statements from the client to the server, you encapsulate them in a stored procedure on the server and send one statement from the client to execute them.
 
Also, stored procedures can be useful if you have an SQL query that you write over and over again. You can save it as a stored procedure, and then just call it to execute it. In stored procedures, you can also pass parameters so that a stored procedure can act based on the passed parameter values.

For this lab, we will download the PETSALE-CREATE-v2.sql script, upload it to Db2 console and run it. 

![image](https://user-images.githubusercontent.com/81119854/126999745-89f06ed4-129b-49ea-afc3-ba476f90457b.png)

![image](https://user-images.githubusercontent.com/81119854/126999801-3c29c62c-bb3d-482d-becf-e67f88c1643f.png)

![image](https://user-images.githubusercontent.com/81119854/126999877-dfbdace2-0004-464d-a688-035220081da6.png)

![image](https://user-images.githubusercontent.com/81119854/127000469-12a44284-d0d1-4887-bc85-ff4127ef0769.png)
![image](https://user-images.githubusercontent.com/81119854/127000519-9fde61cb-10a6-40f6-85fb-a3f5c5ad52bc.png)

Exercise 1

In this exercise, we will create and execute a stored procedure to read data from a table on Db2 using SQL.

We will create a stored procedure routine named RETRIEVE_ALL.

This RETRIEVE_ALL routine will contain a SQL query to retrieve all the records from the PETSALE table, so you don't need to write the same query over and over again. You just call the stored procedure routine to execute the query everytime.

![image](https://user-images.githubusercontent.com/81119854/127001564-f322001a-0243-41b6-8609-ccc8fc8ccbc4.png)
![image](https://user-images.githubusercontent.com/81119854/127001632-846b61c1-b564-46d1-85f1-85c1a2a6d62b.png)

![image](https://user-images.githubusercontent.com/81119854/127001854-fe3c8c82-c654-4a79-a80f-cded34cdac99.png)

To call the RETRIEVE_ALL routine, we may do:

![image](https://user-images.githubusercontent.com/81119854/127002119-b08a8496-24e6-4adf-aab8-308a8f5d81d6.png)

![image](https://user-images.githubusercontent.com/81119854/127002167-f59cf5da-13b3-4ce7-b81a-6f73060b64bc.png)

We can view the created stored procedure routine RETRIEVE_ALL. Click on the 3-bar menu icon in the top left corner and click Data > APPLICATION OBJECTS > Procedures. Find the procedure routine RETRIEVE_ALL from Procedures by clicking Select All. Click on the procedure routine RETRIEVE_ALL.

![image](https://user-images.githubusercontent.com/81119854/127002779-a5e1d819-fcdd-41ce-8f2b-5630c21bb419.png)

![image](https://user-images.githubusercontent.com/81119854/127002937-44ecccd3-4150-4dfd-b457-c576fb098aa9.png)

If we wish to drop the stored procedure routine RETRIEVE_ALL, we may do:

![image](https://user-images.githubusercontent.com/81119854/127003136-c215f857-810d-4576-866a-9d8fe9aaae57.png)

Exercise 2

In this exercise, we will create and execute a stored procedure to write/modify data in a table on Db2 using SQL.

We will create a stored procedure routine named UPDATE_SALEPRICE with parameters Animal_ID and Animal_Health.

This UPDATE_SALEPRICE routine will contain SQL queries to update the sale price of the animals in the PETSALE table depending on their health conditions, BAD or WORSE.

This procedure routine will take animal ID and health conditon as parameters which will be used to update the sale price of animal in the PETSALE table by an amount depending on their health condition. 

Suppose:

For animal with ID XX having BAD health condition, the sale price will be reduced further by 25%.
For animal with ID YY having WORSE health condition, the sale price will be reduced further by 50%.
For animal with ID ZZ having other health condition, the sale price won't change.

The Stored Procedure:

![image](https://user-images.githubusercontent.com/81119854/127004219-b0f5c8ad-bb4b-4f0c-abdd-c67c2056bdcc.png)
![image](https://user-images.githubusercontent.com/81119854/127004298-be900c7d-933c-48cd-bce9-460d6bd98d1b.png)

![image](https://user-images.githubusercontent.com/81119854/127004341-849d73c4-0fff-40d5-8f14-2c6e5890ab82.png)

Let's call the UPDATE_SALEPRICE routine. We want to update the sale price of animal with ID 1 having BAD health condition in the PETSALE table.


