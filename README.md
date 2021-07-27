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

![image](https://user-images.githubusercontent.com/81119854/127005330-4c5539ce-2499-4e82-a883-ed7c320b8f02.png)

Let's call the UPDATE_SALEPRICE routine once again. We want to update the sale price of animal with ID 3 having WORSE health condition in the PETSALE table.

![image](https://user-images.githubusercontent.com/81119854/127005618-8ec3e4d8-8737-48b2-92a5-3f04cc0c10e5.png)

# Committing and rolling back a transaction using a stored procedure 

![image](https://user-images.githubusercontent.com/81119854/127025467-948408b4-fae4-436b-ad51-baeab3d73b81.png)
![image](https://user-images.githubusercontent.com/81119854/127025517-ba39a964-d8d6-47c8-8948-2e7bc455a0d9.png)
![image](https://user-images.githubusercontent.com/81119854/127025709-c7b0e4e2-a5d6-4189-b197-2db169a1de11.png)
![image](https://user-images.githubusercontent.com/81119854/127026176-a0b7d858-2796-499e-a41c-901263eb6f71.png)

![image](https://user-images.githubusercontent.com/81119854/127025591-c85439b3-5b16-4b2b-8df3-fb622728e6e0.png)
![image](https://user-images.githubusercontent.com/81119854/127025648-a87640e0-7eba-49be-90c6-51b3d37d9c69.png)
![image](https://user-images.githubusercontent.com/81119854/127025752-e01fd6ff-04b3-4971-972e-054746da828e.png)
![image](https://user-images.githubusercontent.com/81119854/127026131-7ffc0d29-2b21-48d5-93b8-5e8a487a9177.png)


Task A: example exercise

We will create a stored procedure routine named TRANSACTION_ROSE which will include TCL commands like COMMIT and ROLLBACK.

Now develop the routine based on the given scenario to execute a transaction.

Scenario: Let's buy Rose a pair of Boots from ShoeShop. So we have to update the Rose balance as well as the ShoeShop balance in the BankAccounts table. Then we also have to update Boots stock in the ShoeShop table. After Boots, let's also attempt to buy Rose a pair of Trainers.

![image](https://user-images.githubusercontent.com/81119854/127026667-aebc99f4-9a2d-458d-90a0-447145f8492b.png)
![image](https://user-images.githubusercontent.com/81119854/127026727-ea4cfbfb-59ef-48d2-b044-9306042073f1.png)
![image](https://user-images.githubusercontent.com/81119854/127026768-0c7fe8aa-7ef0-4f26-8003-1eac2de8ec3b.png)

![image](https://user-images.githubusercontent.com/81119854/127026834-eb6cc7be-64c1-4284-8554-2a4000d3fa25.png)

Let's now check if the transaction can successfully be committed or not.

![image](https://user-images.githubusercontent.com/81119854/127027050-b04e4bcb-0c66-487a-8219-f094cb25a6f6.png)

![image](https://user-images.githubusercontent.com/81119854/127027104-e64a8c01-ed7f-463a-bd87-a5db132e831a.png)
![image](https://user-images.githubusercontent.com/81119854/127027158-7e5ee090-75b5-4932-bce1-5feb7e867076.png)

We can observe that the transaction has been executed. But when we observe the tables, no changes have permanently been saved through COMMIT. All the possible changes happened might have been undone through ROLLBACK since the whole transaction fails due to the failure of a SQL statement or more. Let's go through the possible reason behind the failure of the transaction and how COMMIT - ROLLBACK works on a stored procedure:

1 - The first three UPDATEs should run successfully. Both the balance of Rose and ShoeShop should have been updated in the BankAccounts table. The current balance of Rose should stand at 300 - 200 (price of a pair of Boots) = 100. The current balance of ShoeShop should stand at 124200 + 200 = 124400. The stock of Boots should also be updated in the ShoeShop table after the successful purchase for Rose, 11 - 1 = 10.

2 - The last UPDATE statement tries to buy Rose a pair of Trainers, but her balance becomes insufficient (Current balance of Rose: 100 < Price of Trainers: 300) after buying a pair of Boots. So, the last UPDATE statement fails. Since the whole transaction fails if any of the SQL statements fail, the transaction won't be committed.

3 - The SQLCODE which is a stand-alone host variable contains success/failure/warning information of each SQL statement execution. Now since SQLCODE variable gets reset back as the next SQL statement runs, retcode is our local variable to catch the return value of this SQLCODE. SQLCODE returns negative value for each SQL statement if not executed successfully. So, on any error occurrence, all the changes are rolled back. Commit only takes place after the transaction gets executed successfully without any error.

Task B: practice exercise

Create a stored procedure TRANSACTION_JAMES to execute a transaction based on the following scenario: First buy James 4 pairs of Trainers from ShoeShop. Update his balance as well as the balance of ShoeShop. Also, update the stock of Trainers at ShoeShop. Then attempt to buy James a pair of Brogues from ShoeShop. 

If any of the UPDATE statements fail, the whole transaction fails. You will roll back the transaction. Commit the transaction only if the whole transaction is successful.

![image](https://user-images.githubusercontent.com/81119854/127029108-886ecc24-7c1a-49dd-9c28-159870e9d055.png)
![image](https://user-images.githubusercontent.com/81119854/127029175-3bb58054-ce90-4585-8ab9-2864e9abefbd.png)
![image](https://user-images.githubusercontent.com/81119854/127029216-b73803fe-6192-4254-9ce2-243d91d05601.png)

![image](https://user-images.githubusercontent.com/81119854/127029354-0f583fdc-5d52-41a9-9dd7-c40e0c504fbf.png)

![image](https://user-images.githubusercontent.com/81119854/127029752-e8018cc5-b57f-4ca6-be09-de8a9ffba62d.png)

![image](https://user-images.githubusercontent.com/81119854/127029819-2ebd2335-a914-4a59-85ba-d786016e09b7.png)

 The last UPDATE statement fails. So the whole transaction fails.

# Joins

![image](https://user-images.githubusercontent.com/81119854/127046165-90699318-4aca-4fc2-9f02-bbc2d1eeea16.png)
![image](https://user-images.githubusercontent.com/81119854/127046330-83e41a1a-a903-491a-90eb-40d1721a7d0c.png)

![image](https://user-images.githubusercontent.com/81119854/127046361-970d3176-c5ce-4010-a600-a8ebb1914e2c.png)
![image](https://user-images.githubusercontent.com/81119854/127046498-31018aec-8512-48ef-a088-52778e21a2ab.png)

![image](https://user-images.githubusercontent.com/81119854/127046522-c9f2d664-3282-42fa-bbe1-3cec2d71619d.png)
![image](https://user-images.githubusercontent.com/81119854/127046630-5b739ab7-b050-4536-b0bf-e7b92adc03b7.png)

![image](https://user-images.githubusercontent.com/81119854/127046661-5e211592-57aa-45fb-aaed-9ed5530ead0d.png)
![image](https://user-images.githubusercontent.com/81119854/127046797-abf972cf-8617-4d6d-bbe5-5d85f17b2a20.png)

![image](https://user-images.githubusercontent.com/81119854/127046829-9e16014c-dea1-42ec-9bea-aa6fdad608ef.png)
![image](https://user-images.githubusercontent.com/81119854/127046965-447d7e5a-ddfc-4958-bbbf-b0ce2cc47520.png)

![image](https://user-images.githubusercontent.com/81119854/127047001-0d250ee6-d7cb-43eb-95f6-59167b7b949b.png)
![image](https://user-images.githubusercontent.com/81119854/127047136-128ecc7e-0f89-479a-91f2-8bc1048fd46c.png)

![image](https://user-images.githubusercontent.com/81119854/127047209-16a0dd92-73d7-433b-8e96-956f801dcd0e.png)
![image](https://user-images.githubusercontent.com/81119854/127047403-2511f50b-f4a4-4e83-b231-9fd6b90a5c86.png)

# Join Problems

![image](https://user-images.githubusercontent.com/81119854/127069414-fd392ae4-a69b-486e-9116-0e9a48f70b2f.png)
![image](https://user-images.githubusercontent.com/81119854/127069440-963269d7-ef24-42ac-9bbf-25a78e30c8f2.png)
![image](https://user-images.githubusercontent.com/81119854/127069504-d5cc5365-e578-4c10-af4e-5d4c71f6f37e.png)

![image](https://user-images.githubusercontent.com/81119854/127156247-0dcb5448-6a2d-473f-9553-6da563e1bd28.png)
![image](https://user-images.githubusercontent.com/81119854/127156427-896a4b7b-d289-418a-a825-3ab76bbf8065.png)
![image](https://user-images.githubusercontent.com/81119854/127156294-fd48361a-98ea-4dae-ab77-1a314afc0112.png)

![image](https://user-images.githubusercontent.com/81119854/127156526-7958b68c-e384-49ef-a850-45e3a3eb3dd4.png)
![image](https://user-images.githubusercontent.com/81119854/127159694-d69edf22-eda7-4b7c-a982-e771e30502d7.png)
![image](https://user-images.githubusercontent.com/81119854/127159745-30e12d94-63cb-45fc-9c0a-197c9d0a097c.png)






