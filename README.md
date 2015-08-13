# Database Schemas

## SUMMARY

A relational database is a collection of tables which are related to one another (surprise, surprise!).

Each table is a physical representation of an object and each column or field in that table represents an attribute of the model.  Each row within that table represents an instance of the model.

If we want to create a relationship between tables, we first need to identify the type of relationship.  The three relationships which we will discuss are one-to-many, one-to-one, and many-to-many. 

### ONE-TO-MANY

A one-to-many relationship is the easiest to understand and can be demonstrated using an example of the relationship between a person and the number of shoes that they own.  A user has many pairs of shoes, but a particular shoe-pair belongs to exactly one user.  Another example of a one-to-many relationship is between a street and a house.  A street can have many houses on it, but a house can only belong to one street.

When we create a table in a relational database, that table has a primary key.  This key is its unique identifier.  A table can also have a foreign key, which is created when we want to reference a relationship between one table and another.  The foreign key matches the primary key column of the related table.  

<pre>
+------------+        +-------------+
| users      |        | shoes       |
+------------+        +-------------+
| id         |&lt;---\   | id          |
| first_name |     \--| user_id     |
| last_name  |        | price       |
| email      |        | color       |
| created_at |        | created_at  |
| updated_at |        | updated_at  |
+------------+        +-------------+
</pre>

In the example of users and shoes, the foreign key is on the ‘many’ table, which stores the primary key of the ‘one’ table.  The convention is that the foreign key contains the singular version of the foreign table (e.g. the foreign key is user_id because it contains an integer that corresponds to one specific row in the users table).

### ONE-TO-ONE

A one-to-one relationship can best be represented by a person and their connection to their liver.  A person has only one driver’s license and that driver’s license belongs only to that person. 

Another, more practical, example would be a Facebook account.  A user has one Facebook account and that account belongs specifically to that user.  

<pre>
+---------------------+        +-------------------+
| users               |        | facebook_accounts |
+---------------------+        +-------------------+
| id                  |     /-&gt;| id                |
| first_name          |    /   | fb_username       |
| last_name           |   /    | created_at        |
| email               |  /     | updated_at        |
| facebook_account_id |-/      +-------------------+
| created_at          |
| updated_at          |
+---------------------+
</pre>

In the case of the Facebook example, a user’s facebook_account_id could be null if the user does not have a Facebook account.  Also, notice that a user can have, at most, one Facebook account, and the facebook_accounts table does not reference the user table. 

An important thing to remember with one-to-one relationships that if you have a logical grouping of fields which can be NULL (such as a facebook_account_id), then it is best to separate those fields into a separate table which represents a one-to-one relationship. 

### MANY-TO-MANY

A many-to-many relationship can best be represented through the example of patients and doctors.  One patient can see many doctors (a gynecologist, a cardiologist, an immunologist, a podiatrist) and a doctor has many patients.  

In order to show this relationship, we create a join table which holds the foreign keys for each of the tables which it is connecting.  

<pre>
+------------+       +------------------+       +--------------+
| doctors    |       | doctors_patients |       | patients     |
+------------+       +------------------+       +--------------+
| id         |&lt;--\   | id               |    /-&gt;| id           |
| first_name |    \--| doctor_id        |   /   | first_name   |
| last_name  |       | patient_id       |--/    | last_name    |
| expertise	 |       |                  |       | created_at   |
| created_at |       +------------------+       | updated_at   |
| updated_at |                                  +--------------+
+------------+                                  
</pre>

Here, the doctors_patients table serves as the join table and tells us which doctors have which patients or vice versa.  


## Releases

### Release 0 Design the schema for a one-to-many relationship

Use [SQL Designer](http://ondras.zarovi.cz/sql/demo/) to create your schema for the following one-to-many relationships.

<code>users</code> and <code>orders</code>

<code>houses</code> and <code>streets</code>

When you are done, take screenshots of your schema design and commit it. 

### Release 1 Design the schema for a one-to-one relationship

Use [SQL Designer](http://ondras.zarovi.cz/sql/demo/) to create your schema for the following one-to-one relationships.

<code>person</code> and <code>liver</code>

<code>person</code> and <code>passport</code>

When you are done, take a screenshots of your schema design and commit it. 

### Release 2 Design the schema for a many-to-many relationship

Use [SQL Designer](http://ondras.zarovi.cz/sql/demo/) to create your schema for the following many-to-many relationships.

<code>authors</code> and <code>books</code>

<code>students</code> and <code>classes</code>

<code>employees</code> and <code>skills</code>

When you are done, take screenshots of your schema design and commit it. 





