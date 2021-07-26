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

