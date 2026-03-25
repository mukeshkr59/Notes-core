# Lecture 1: Introduction to DBMS and SQL

## Agenda

- What is a Database
- What, What Not, Why, How of Scaler SQL Curriculum
- Types of Databases
- Intro to Relational Databases
- Intro to Keys

## What is a Database

Okay, tell me, In your day to day life whenever you have a need to save some information, where do you save it? Especially when you may need to refer to it later, maybe something like your expenses for the month, or your todo or shopping list?

Correct! Many of us use softwares like Excel, Google Sheets, Notion, Notes app etc to keep a track of things that are important for us and we may need to refer to it in future. Everyone, be it humans or organizations, have need to store a lot of data that me useful for them later. Example, let's think about Scaler. At Scaler, we would want to keep track of all of your's attendance, assignments solved, codes written, coins, mentor session etc! We would also need to store details about instructors, mentors, TAs, batches, etc. And not to forget all of your's email, phone number, password. Now, where will we do this?

For now, forget that you know anything about databases. Imagine yourself to be a new programmer who just knows how to write code in a programming language. Where will you store data so that you are able to retrieve it later and process that?

Correct! You will store it in files. You will write code to read data from files, and write data to files. And you will write code to process that data. For example you may create separate CSV (comma separated values, you will understand as we proceed) files to store information about let's say students, instructors, batches. Eg:

```
students.csv
name, batch, psp, attendance, coins, rank
Naman, 1, 94, 100, 0, 1
Amit, 2, 81, 70, 400, 1
Aditya, 1, 31, 100, 100, 2
```

```instructors.csv
name, subjects, average_rating
Rachit, C++, 4.5
Rishabh, Java, 4.8
Aayush, C++, 4.9
```

```batches.csv
id, name, start_date, end_date
1, AUG 22 Intermediate, 2022-08-01, 2023-08-01
2, AUG 22 Beginner, 2022-08-01, 2023-08-01
```

Now, let's say you want to find out the average attendance of students in each batch. How will you do that? You will have to write code to read data from students.csv, and batches.csv, and then process it to find out the average attendance of students in each batch. Right? Do you think this will be very cumbersome?

### Issues with Files as a Database

1. Inefficient

While the above set of data is very small in size, let's think of actual Scaler scale. We have 2M+ users in our system. Imagine going through a file with 2M lines, reading each line, processing it to find your relevant information. Even a very simple task like finding the psp of a student named Naman will require you to open the file, read each line, check if the name is Naman, and then return the psp. Time complexity wise, this is O(N) and very slow.

2. Integrity

Is there anyone stopping you from putting a new line in `students.csv` as ```Naman, 1, Hello, 100, 0, 1``` . If you see that `Hello` that is unexpected. The psp can't be a string. But there is no one to validate and this can lead to very bad situations. This is known as data integrity issue, where the data is not as expected.

3. Concurrency

Later in the course, you will learn about multi-threading and multi-processing. It is possible for more than 1 people to query about the same data at the same time. Similarly, 2 people may update the same data at the same time. On save, whose version should you save? Imagine you give same Google Doc to 2 people and both make changes on the same line and send to you. Whose version will you consider to be correct? This is known as concurrency issue.

4. Security

Earlier we talked about storing password of users. Imagine them being stored on files. Anyone who has access to the file can see the password of all users. Also anyone who has access to the file can update it as well. THere is no authorization at user level. Eg: a particular person may be only allowed to read, not write. '

### What's a Database

Now let's get back to our main topic. What is a database? A database is nothing but a collection of related data. Example, Scaler will have a Database that stores information about our students, users, batches, classes, instructors, and everything else. Similarly, Facebook will have a database that stores information about all of it's users, their posts, comments, likes, etc. The above way of storing data into files was also nothing but a database, though not the easiest one to use and with a lot of issues.

### What's a Database Management System (DBMS)

A DBMS as the name suggests is a software system that allows to efficiently manage a database. A DBMS allows us to create, retrieve, update, and delete data (often also called CRUD operations). It also  allows to define rules to ensure data integrity, security, and concurrency. It also provides ways to query the data in the database efficiently. Eg: find all students with psp > 50, find all students in batch 1, find all students with rank 1 in their batch, etc. There are many database management systems, each with their tradeoffs. We will talk about the types of databases later today.

Now let me talk about how the curriculum is structured. We will be having 11 live classes, followed by a contest. In the live classes we are going to cover everything that is important for you for interviews as well as day to day job. Having said that, as I mentioned that Databases are  avery vast field, attached with every live class you will be able to see a set of recorded videos curated for you for extra learning you can gain. Those videos will mostly be around theoretical concepts behind databases that are not much asked in interviews much nor used at day to day job, but good to know. Sometimes these videos will be on solving extra problems for a particular SQL Topic. You can go through those videos if you want to gain deeper understanding but aren't mandatory to solve assignments or clear contest.

| S.No | Lecture Title |
| --- | --- |
| 1 | Introduction to Databases and SQL |
| 2 | CRUD |
| 3 | CRUD-2 and Joins |
| 4 | Joins - 2 |
| 5 | Aggregate and Subqueries |
| 6 | Indexes |
| 7 | Transactions |
| 8 | Schema Design - 1 |
| 9 | Schema Design - 2 |
| 10 | Views and Window Functions |
| CONTEST | - |

I hope this excites you for your learning journey in this module and I wish you are able to make the most out of it. 

## Types of Databases

Welcome back after the break. Hope you had a good rest and had some water, etc. Now let's start with the next topic for the day and discuss different types of databases that exist. Okay, tell me one thing, when you have to store some data, eg let's say you are an instructor at Scaler and want to keep a track of attendance and psp of every student of you, in what form will you store that?


Correct! Often one of the easiest and most intuitive way to store data can be in forms of tables. Example for the mentioned use case, I may create a table with 3 columns: name, attendance, psp and fill values for each of my students there. This is very intuitive and simple and is also how relational databases work.

### Relational Databases

Relational Databases allow you to represent a database as a collection of multiple related tables. Each table has a set of columns and rows. Each row represents a record and each column represents a field. Example, in the above case, I may have a table with 3 columns: name, attendance, psp and fill values for each of my students there. Let's learn some properties of relational databases.

1. Relational Databases represent a database as a collection of tables with each table storing information about something. This something can be an entity or a relationship between entities. Example: I may have a table called students to store information about students of my batch (an entity). Similarly I may have a table called student_batches to store information about which student is in which batch (a relationship betwen entities).
2. Every row is unique. This means that in a table, no 2 rows can have same values for all columns. Example: In the students table, no 2 students can have same name, attendance and psp. There will be something different for example we might also want to store their roll number to distingusih 2 students having the same name.
3. All of the values present in a column hold the same data type. Example: In the students table, the name column will have string values, attendance column will have integer values and psp column will have float values. It cannot happen that for some students psp is a String.
4. Values are atomic. What does atomic mean? What does the word `atom` mean to you?

Correct. Similarly, atomic means indivisible. So, in a relational database, every value in a column is indivisible. Example: If we have to store multiple phone numbers for a student, we cannot store them in a single column as a list. How to store those, we will learn in the end of the course when we do Schema Design. Having said that, there are some SQL databases that allow you to store list of values in a column. But that is not a part of SQL standard and is not supported by all databases. Even those that support, aren't most optimal with queries on such columns.

5. The columns sequence is not guaranteed. This is very important. SQL standard doesn't guarantee that the columns will be stored in the same sequence as you define them. So, if you have a table with 3 columns: name, attendance, psp, it is not guaranteed that the data will be stored in the same sequence. So it is recommended to not rely on the sequence of columns and always use column names while writing queries. While MySQL guaranteees that the order of columns shall be same as defined at time of creating table, it is not a part of SQL standard and hence not guaranteed by all databases and relying on order can cause issues if in future a new column is added in between.

6. The rows sequence is not guaranteed. Similar to columns, SQL doesn't guarantee the order in which rows shall be returned after any query. So, if you want to get rows in a particular order, you should always use `ORDER BY` clause in your query which we will learn about in the next class. So when you write an SQL query, don't assume that the first row will always be the same. The order of rows may change across multiple runs of same query. Having said that, MySQL does return rows in order of their primary key (we will learn about this later today), but again, don't rely on that as not guaranteed by SQL standard.
  
7. The name of every column is unique. This means that in a table, no 2 columns can have same name. Example: In the students table, I cannot have 2 columns with name `name`. This is because if I have to write a query to get the name of a student, I will have to write `SELECT name FROM students`. Now if there are 2 columns with name `name`, how will the database know which one to return? Hence, the name of every column is unique.


### Non-Relational Databases

Now that we have learnt about relational databases, let's talk about non-relational databases. Non-relational databases are those databases that don't follow the relational model. They don't store data in form of tables. Instead, they store data in form of documents, key-value pairs, graphs, etc. In the DBMS module, we will not be talking about them. We will talk about them in the HLD Module. 

In the DBMS module, our goal is to cover the working of relational databases and how to work with them, that is via SQL queries. 

## Keys in Relational Databases

Now we are moving to probably the most important foundational concept of Relational Databases: Keys. let's say you are working at Scaler and are maintaining a table of every students' details. Someone tells you to update the psp of Naman to 100. How will you do that? What can go wrong?

What if there are 2 Namans?
 
Correct. If there are 2 Namans, how will you know which one to update? This is where keys come into picture. Keys are used to uniquely identify a row in a table. There are 2 important types of keys: Primary Key and Foreign Key. There are also other types of keys like Super Key, Candidate Key etc. Let's learn about them one by one.

### Super Keys

To understand this, let's take an example of a students table at scaler with following columns.

| name | psp | email | batch | phone number |
| - | - |- | - | - |
|Naman | 1 | 94 | 100 | 0 | 1 |
|Amit |  2 | 81 |  70 | 400 | 1 |
|Aditya| 1| 31| 100| 100| 2 |

Which are the columns that can be used to uniquely identify a row in this table?

Let's start with name. How many of you think name can be used to uniquely identify a row in this table? 

Correct. Name is not a good idea to recognize a row. Why? Because there can be multiple students with same name. So, if we have to update the psp of a student, we cannot use name to uniquely identify the student. Email, phone number on the other hand are a great idea, assuming no 2 students have same email, or same phone number. 

Do you think the value of combination of columns (name, email) can uniquely identify a student? Do you think there will be only 1 student with a particular combination of name and email. Eg: will there be only 1 student like (Naman, naman@scaler.com)?

Correct, similarly do you think (name, phone number) can uniquely identify a student? What about (name, email, phone number)? What about (name, email, psp)? What about (email, psp)?

The answer to each of the above is Yes. Each of these can be considered a `Super Key`. A super key is a combination of columns whose values can uniquely identify a row in a table. What do you think are other such super keys in the students table?

In the above keys, did you ever feel something like "but this column was useless to uniquely identify a row.." ? Let's take example of (name, email, psp). Do you think psp is required to uniquely identify a row? Similarly, do you think name is required as you anyways have email right? 

Now let's remove the columns that weren't necessary. 

Also, let's say we were an offline school, and students don't have email or phone number. In that case what do you think schools use to uniquely identify a student? Eg: If we remove redundant columns from (name, email, psp), we will be left with (email). Similarly, if we remove redundant columns from (name, email, phone number), we will be left with (phone number) or (email). These are known as `candidate keys`. A candidate key is a super key from which no column can be removed and still have the property of uniquely identifying a row. If any more column is removed from a candidate key, it will no longer be able to uniquely identify a row. Let's take another example. Consider a table Scaler has for storing students's attendance for every class

| student_id | class_id | attendance |

What do you think are the candidate keys for this table? Do you think (student_id) is a candidate key? Will there be only 1 row with a particular student_id?

Is (class_id) a candidate key? Will there be only 1 row with a particular class_id?

Is (student_id, class_id) a candidate key? Will there be only 1 row with a particular combination of student_id and class_id?

Yes! (student_id, class_id) is a candidate key. If we remove any of the columns of this, the remanining part is not a candidate key. Eg: If we remove student_id, we will be left with (class_id). But there can be multiple rows with same class_id. Similarly, if we remove class_id, we will be left with (student_id). But there can be multiple rows with same student_id. Hence, (student_id, class_id) is a candidate key.

Is (student_id, class_id, attendance) a candidate key? Will there be only 1 row with a particular combination of student_id, class_id and attendance?

But can we remove any column from this and still have a candidate key? Eg: If we remove attendance, we will be left with (student_id, class_id). This is a candidate key. Hence, (student_id, class_id, attendance) is not a candidate key.

### Primary Key

We just learnt about super keys and candidate keys. Can 1 table have mulitiple candidate keys? Yes. The table earlier had both (email), (phone number) as candidate keys. A key in MySQL plays a very important role. Example, MySQL orders the data in disk by the key. Similarly, by default, it returns answers to queries ordered by key. Thus, it is important that there is only 1 key. And that is called `primary key`. A primary key is a candidate key that is chosen to be the key for the table. In the students table, we can choose (email) or (phone number) as the primary key. Let's choose (email) as the primary key.

Sometimes, we may have to or want to create a new column to be the primary key. Eg: If we have a students table with columns (name, email, phone number), we may have to create a new column called roll number or studentId to be the primary key. This may be because let's say a user can change their email or phone number. Something that is used to uniquely identify a row should ideally never change. Hence, we create a new column called roll number or studentId to be the primary key.

We will see later today on how MySQL allows to create primary keys etc. Before we go to foreign keys and composite keys, let's actually get our hands dirt with SQL. 

### Foreign Keys

Now let's get to the last topic of the day. Which is foreign keys. Let's say we have a table called batches which stores information about batchesat Scaler. It has columns (id, name, startDate, endDate). We would want to know for every student, which batch do they belong to. How can we do that?

Correct, We can add batchId column in students table. But how do we know which batch a student belongs to? How do we ensure that the batchId we are storing in the students table is a valid batchId? What if someone puts the value in batchID column as 4 but there is no batch with id 4 in batches table. We can set such kind of constraints using foreign keys. A foreign key is a column in a table that references a column in another table. It has nothing to do with primary, candidate, super keys. It can be any column in 1 table that refers to any column in other table. In our case, batchId is a foreign key in the students table that references the id column in the batches table. This ensures that the batchId we are storing in the students table is a valid batchId. If we try to insert any value in the batchID column of students table that isn't present in id column of batches table, it will fail. ANother example:

Let's say we have `years` table as:
`| id | year | number_of_days |`

and we have a table students as:
`| id | name | year |`

Is `year` column in students table a foreign key? 

The correct answer is yes. It is a foreign key that references the id column in years table. Again, foreign key has nothing to do with primary key, candidate key etc. It is just any column on one side that references another column on other side. Though often it doesn't make sense to have that and you just keep primary key of the other table as the foreign key. If not a primary key, it should be a column with unique constraint. Else, there will be ambiguities.

Okay, now let's think of what can go wrong with foreign keys?

Correct, let's say we have students and batches tables as follows:

| batch_id | batch_name |
|----------|------------|
| 1        | Batch A    |
| 2        | Batch B    |
| 3        | Batch C    |


| student_id | first_name | last_name | batch_id |
|------------|------------|-----------|----------|
| 1          | John       | Doe       | 1        |
| 2          | Jane       | Doe       | 1        |
| 3          | Jim        | Brown     | 2        |
| 4          | Jenny      | Smith     | 3        |
| 5          | Jack       | Johnson   | 2        |

Now let's say we delete the row with batch_id 2 from batches table. What will happen? Yes, the students Jim and Jack will be orphaned. They will be in the students table but there will be no batch with id 2. This is called orphaning. This is one of the problems with foreign keys. Another problem is that if we update the batch_id of a batch in batches table, it will not be updated in students table. Eg: If we update the batch_id of Batch A from 1 to 4, the students John and Jane will still have batch_id as 1. This is called inconsistency.

To fix for these, MySQL allows you to set ON DELETE constraints so that cascading deletes happen when such a delete happens.



# Lecture 2: CRUD

## What is CRUD?

Hello Everyone  
Today we are going to start the journey of learning MySQL queries by learning about CRUD Operations. Okay tell me one thing. Let's say there is a table in which we are storing information about students. What all can we do in that table or its entries?

Correct. Primarily, on any entity stored in a table, there are 4 operations possible:

1. Create (or inserting a new entry)
2. Read (fetching some entries)
3. Update (updating information about an entry already stored)
4. Delete (deleting an entry)

Today we are going to discuss about these operations in detail. Understand that read queries can get a lot more complex, involving aggregate functions, subqueries etc, which we shall talk about in detail in later classes. So don't worry about that. Take today's class as an introduction to the world of MySQL queries.

We will be starting with learning about Create, then go to Read, then Update and finally Delete. So let's get started. For today's class as well as most of the classes ahead, we will be using Sakila database, which is an official sample database provided by MySQL. I hope you have downloaded and set that up on your machine already, following instructions shared in the earlier classes.

## Sakila Database Walkthrough

Let me give you all a brief idea about what Sakila database represents so that it is easy to relate to the conversations that we shall have around this over the coming weeks. Sakila database represents a digital video rental store, assume an old movie rental store before Netflix etc came. It's designed with functionality that would allow for all the operations of such a business, including transactions like renting films, managing inventory, and storing customer and staff information. Example: it has tables regarding films, actors, customers, staff, stores, payments etc. You shall get more familiar with this in the coming classes, don't worry!

## Create

### CREATE Query

First of all, what is SQL? SQL stands for Structured Query Language. It is a language used to interact with relational databases. It allows you to create tables, fetch data from them, update data, manage user permissions etc. Today we will just focus on creation of data. Remaining things will be covered over the coming classes. Why "Structured Query" bceause it allows to query over data arranged in a structured way. Eg: In Relational databases, data is structured into tables. 

A simple query to create a table in MySQL has:
  - column names
  - data type of column (integer, varchar, boolean, date, timestamp)
  - properties of column (unique, not null, default)

Similarily, the table could also have properties (primary key, key)

```sql
CREATE TABLE students (
    id INT AUTO_INCREMENT,
    firstName VARCHAR(50) NOT NULL,
    lastName VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    dateOfBirth DATE NOT NULL,
    enrollmentDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    psp DECIMAL(3, 2) CHECK (psp BETWEEN 0.00 AND 100.00),
    batchId INT,
    isActive BOOLEAN DEFAULT TRUE,
    PRIMARY KEY (id),
);
```

Here we are creating a table called students. Inside brackets, we mention the different columns that this table has. Alongwith each columns, we mention the data type of that column. Eg: firstName is of type VARCHAR(50). Please do watch the video on SQL Data Types attached to today's class to understand what VARCHAR, TIMESTAMP etc means. For our today's discussion, it suffices to know that these are different data types supported by MySQL. After the data type, we mention any constraints on that column. Eg: NOT NULL means that this column cannot be null. In tomorrow's class when we will learn how to insert data, if we try to not put a value of this column, we will get an error. UNIQUE means that this column cannot have duplicate values. If we insert a new row in a table, or update an existing row that leads to 2 rows having same value of this column, the query will fail and we will get an error. DEFAULT specifies that if no value is provided for this column, it will take the given value. Example, for enrollmentDate, it will take the value of current_timestamp, which the time when you are inserting the row. CHECK (psp BETWEEN 0.00 AND 100.00) means that the value of this column should be between 0.00 and 100.00. If some other value is put, the query will fail.


### INSERT Query

Now let's start with the first set of operation for the day: The Create Operation. As the name suggests, this operation is used to create new entries in a table. Let's say we want to add a new film to the database. How do we do that?

`INSERT` statement in MySQL is used to insert new entries in a table. Let's see how we can use it to insert a new film in the `film` table of Sakila database.

```sql
INSERT INTO film (title, description, release_year, language_id, rental_duration, rental_rate, length, replacement_cost, rating, special_features) 
VALUES ('The Dark Knight', 'Batman fights the Joker', 2008, 1, 3, 4.99, 152, 19.99, 'PG-13', 'Trailers'),
       ('The Dark Knight Rises', 'Batman fights Bane', 2012, 1, 3, 4.99, 165, 19.99, 'PG-13', 'Trailers'),
       ('The Dark Knight Returns', 'Batman fights Superman', 2016, 1, 3, 4.99, 152, 19.99, 'PG-13', 'Trailers');
```

Let's dive through the syntax of the query. First we have the `INSERT INTO` clause, which is used to specify the table in which we want to insert the new entry. Then we have the column names in the brackets, which are the columns in which we want to insert the values. Then we have the `VALUES` clause, which is used to specify the values that we want to insert in the columns. The values are specified in the same order as the columns are specified in the `INSERT INTO` clause. So the first value in the `VALUES` clause will be inserted in the first column specified in the `INSERT INTO` clause, and so on.

A few things to note here:

1. The column names is optional. If you don't specify the column names, then the values will be inserted in the columns in the order in which they were defined at the time of creating the table. Example: in the above query, if we don't specify the column names, then the values will be inserted in the order `film_id`, `title`, `description`, `release_year`, `language_id`, `original_language_id`, `rental_duration`, `rental_rate`, `length`, `replacement_cost`, `rating`, `special_features`, `last_update`. So the value `The Dark Knight` will be inserted in the `film_id` column, `Batman fights the Joker` will be inserted in the `title` column and so on.  
   - This is not a good practice, as it makes the query prone to errors. So always specify the column names. 
   - This makes writing queries tedious as while writing query you have to keep a track of what column was where. And even a small miss can lead to a big error. 
   - Also, if you don't specify the column names, then you have to specify values for all the columns. If you don't want to specify values for all the columns, then you have to specify the column names. Example: if you don't specify column names, then you have to specify values for all the columns, including `film_id`, `original_language_id` and `last_update`, which we may want to keep `NULL`.

Anyways, an example of a query without column names is as follows:

```sql
INSERT INTO film
VALUES (default, 'The Dark Knight', 'Batman fights the Joker', 2008, 1, NULL, 3, 4.99, 152, 19.99, 'PG-13', 'Trailers', default);
```

NULL is used to specify that the value of that column should be `NULL`, and `default` is used to specify that the value of that column should be the default value specified for that column. Example: `film_id` is an auto-increment column, so we don't need to specify its value. So we can specify `default` for that column, which will insert the next auto-increment value in that column.

So that's pretty much all that's there about Create operations. There is 1 more thing about insert, which is how to insert data from one table to another, but we will talk about that after talking about read. Any doubts till now? Via thumbs up/ down can you all let me know how many of you are 100% clear till here?

So seems like all doubts are clear. Before I start with read operations, let me have 2 small Quiz questions for you.

## Read

Now let's get to the most interest, and also maybe most important part of today's session: Read operations. . `SELECT` statement is used to read data from a table. Let's see how we can use it to read data via different queries on the `film` table of Sakila database. A basic select query is as follows:

```sql
SELECT * FROM film;
```

Here we are selecting all the columns from the `film` table. The `*` is used to select all the columns. This query will give you the value of each column in each row of the film table. If we want to select only specific columns, then we can specify the column names instead of `*`. Example:

```sql
SELECT title, description, release_year FROM film;
```

Here we are selecting only the `title`, `description` and `release_year` columns from the `film` table. Note that the column names are separated by commas. Also, the column names are case-insensitive, so `title` and `TITLE` are the same. Example following query would have also given the same result:

```sql
SELECT TITLE, DESCRIPTION, RELEASE_YEAR FROM film;
```

Now, let's learn some nuances around the `SELECT` statement.

### Selecting Distinct Values

Let's say we want to select all the distinct values of the `rating` column from the `film` table. How do we do that? We can use the `DISTINCT` keyword to select distinct values. Example:

```sql
SELECT DISTINCT rating FROM film;
```

This query will give you all the distinct values of the `rating` column from the `film` table. Note that the `DISTINCT` keyword, as all other keywords in MySQL, is case-insensitive, so `DISTINCT` and `distinct` are the same.

We can also use the `DISTINCT` keyword with multiple columns. Example:

```sql
SELECT DISTINCT rating, release_year FROM film;
```

This query will give you all the distinct values of the `rating` and `release_year` columns from the `film` table. Let's talk about how this works. A lot of SQL queries can be easily understood by relating them to basic for loops etc. Over this class, and the coming classes, I will relate every complex query with a corresponding pseudo code has you tried to do the same in a programming language. As all of you have already solved many DSA problems, this shall be much more easy and fun for you to learn. BTW: At the end, I will also share a final diagram that relates an SQL query to a corresponding pseudo code, with select, aggregate, group by, having, order by, limit, join, subquery, etc.

So, let's try to understand the above query with a pseudo code. The pseudo code for the above query would be as follows:

```python
answer = []

for each row in film:
    answer.append(row)

filtered_answer = []

for each row in answer:
    filtered_answer.append(row['rating'], row['release_year'])

unique_answer = set(filtered_answer)

return unique_answer
```

So what you see is that DISTINCT keyword on multiple column gives you for all of the rows in the table, the distinct value of pair of these columns.

### Select statement to print a constant value

Let's say we want to print a constant value in the output. Eg: The first program that almost every programmer writes: "Hello World". How do we do that? We can use the `SELECT` statement to print a constant value. Example:

```sql
SELECT 'Hello World';
```

That's it. No from, nothing. Just the value. You can also combine it with other columns. Example:

```sql
SELECT title, 'Hello World' FROM film;
```

### Operations on Columns

Let's say we want to select the `title` and `length` columns from the `film` table. If you see, the value of length is currently in minutes, but we want to select the length in hours instead of minutes. How do we do that? We can use the `SELECT` statement to perform operations on columns. Example:

```sql
SELECT title, length/60 FROM film;
```

Later in the course we will learn about Built In functions in SQL as well. You can use those functions as well to perform operations on columns. Example:

```sql
SELECT title, ROUND(length/60) FROM film;
```

ROUND function is used to round off a number to the nearest integer. So the above query will give you the title of the film, and the length of the film in hours, rounded off to the nearest integer.

### Inserting Data from Another Table

BTW, select can also be used to insert data in a table. Let's say we want to insert all the films from the `film` table into the `film_copy` table. We can combine the `SELECT` and `INSERT INTO` statements to do that. Example:

```sql
INSERT INTO film_copy (title, description, release_year, language_id, rental_duration, rental_rate, length, replacement_cost, rating, special_features)
SELECT title, description, release_year, language_id, rental_duration, rental_rate, length, replacement_cost, rating, special_features
FROM film;
```

Here we are using the `SELECT` statement to select all the columns from the `film` table, and then using the `INSERT INTO` statement to insert the selected data into the `film_copy` table. Note that the column names in the `INSERT INTO` clause and the `SELECT` clause are the same, and the values are inserted in the same order as the columns are specified in the `INSERT INTO` clause. So the first value in the `SELECT` clause will be inserted in the first column specified in the `INSERT INTO` clause, and so on.

Okay, let's take a pause to answer any doubts anyone may be having till now. For those who are absolutely clear can you please do a thumbs up in the chat. If any doubt, can you please do a thumbs down and post the doubt in chat.

Okay, let me also verify how well you have learnt till now with a few quiz questions.

Till now, we have been doing basic read operations. SELECT query with only FROM clause is rarely sufficient. Rarely do we want to return all rows. Often we need to have some kind of filtering logic etc. for the rows that should be returned. Let's learn how to do that.

### WHERE Clause

Let's say we want to select all the films from the `film` table which have a rating of `PG-13`. How do we do that? We can use the `WHERE` clause to filter rows based on a condition. Example:

```sql
SELECT * FROM film WHERE rating = 'PG-13';
```

Here we are using the `WHERE` clause to filter rows based on the condition that the value of the `rating` column should be `PG-13`. Note that the `WHERE` clause is always used after the `FROM` clause. In terms of pseudocode, you can think of where clause to work as follows:

```python
answer = []

for each row in film:
    if row.matches(conditions in where clause) # new line from above
        answer.append(row)

filtered_answer = []

for each row in answer:
    filtered_answer.append(row['rating'], row['release_year'])

unique_answer = set(filtered_answer) # assuming we also had DISTINCT

return unique_answer
```

If you seem where clause can be considered analgous to `if` in a programming language. With if as well there are many other operators that are used, right. Can you name which operators do we often use in programming languages with `if`?

> NOTE: Wait for students to give answer. Give hints to get AND, OR, NOT from them.

### AND, OR, NOT

Correct. We use things like `and` , `or`, `!` in programming languages to combine multiple conditions. Similarly, we can use `AND`, `OR`, `NOT` operators in SQL as well. Example: We want to get all the films from the `film` table which have a rating of `PG-13` and a release year of `2006`. We can use the `AND` operator to combine multiple conditions.

```sql
SELECT * FROM film WHERE rating = 'PG-13' AND release_year = 2006;
```

Similarly, we can use the `OR` operator to combine multiple conditions. Example: We want to get all the films from the `film` table which have a rating of `PG-13` or a release year of `2006`. We can use the `OR` operator to combine multiple conditions.

```sql
SELECT * FROM film WHERE rating = 'PG-13' OR release_year = 2006;
```

Similarly, we can use the `NOT` operator to negate a condition. Example: We want to get all the films from the `film` table which do not have a rating of `PG-13`. We can use the `NOT` operator to negate the condition.

```sql
SELECT * FROM film WHERE NOT rating = 'PG-13';
```

An advice on using these operators. If you are using multiple operators, it is always a good idea to use parentheses to make your query more readable. Else, it can be difficult to understand the order in which the operators will be evaluated. Example:

```sql
SELECT * FROM film WHERE rating = 'PG-13' OR release_year = 2006 AND rental_rate = 0.99;
```

Here, it is not clear whether the `AND` operator will be evaluated first or the `OR` operator. To make it clear, we can use parentheses. Example:

```sql
SELECT * FROM film WHERE rating = 'PG-13' OR (release_year = 2006 AND rental_rate = 0.99);
```

Till now, we have used only `=` for doing comparisons. Like traditional programming languages, MySQL also supports other comparison operators like `>`, `<`, `>=`, `<=`, `!=` etc. Just one special case, `!=` can also be written as `<>` in MySQL. Example:

```sql
SELECT * FROM film WHERE rating <> 'PG-13';
```

### IN Operator

With comparison operators, we can only compare a column with a single value. What if we want to compare a column with multiple values? For example, we want to get all the films from the `film` table which have a rating of `PG-13` or `R`. One way to do that can be to combine multiple consitions using `OR`.  A better way will be to use the `IN` operator to compare a column with multiple values. Example:

```sql
SELECT * FROM film WHERE rating IN ('PG-13', 'R');
```

Okay, now let's say we want to get those films that have ratings anything oter than the above 2. Any guesses how we may do that?

Correct! We had earlier discussed about `NOT`. You can also use `NOT` before `IN` to negate the condition. Example:

```sql
SELECT * FROM film WHERE rating NOT IN ('PG-13', 'R');
```

Think of IN to be like any other operator. Just that it allows comparison with multiple values.

Hope you had a good break. Let's continue with the session. In this second part of the session, we are going to start the discussion by discussing about another important keyword in SQL, `BETWEEN`.

### IS NULL Operator

Now we are almost at the end of the discussion about different operators. Do you all remember how we store emptiess, that is, no value for a particular column for a particular row? We store it as `NULL`. Interestingly working with NULLs is a bit tricky. We cannot use the `=` operator to compare a column with `NULL`. Example:

```sql
SELECT * FROM film WHERE description = NULL;
```

The above query will not return any rows. Why? Because `NULL` is not equal to `NULL`. Infact, `NULL` is not equal to anything. Nor is it not equal to anything. It is just `NULL`. 

Example:

```sql
SELECT NULL = NULL;
```

The above query will return `NULL`. Similarly, `3 = NULL` , `3 <> NULL` , `NULL <> NULL` will also return `NULL`. So, how do we compare a column with `NULL`? We use the `IS NULL` operator. Example:

```sql
SELECT * FROM film WHERE description IS NULL;
```

Similarly, we can use the `IS NOT NULL` operator to find all the rows where a particular column is not `NULL`. Example:

```sql
SELECT * FROM film WHERE description IS NOT NULL;
```

In many assignments, you will find that you will have to use the `IS NULL` and `IS NOT NULL` operators. Without them you will miss out on rows that had NULL values in them and get the wrong answer. Example:
find customers with id other than 2. If you use `=` operator, you will miss out on the customer with id `NULL`. Example:

```sql
SELECT * FROM customers WHERE id != 2;
```

The above query will not return the customer with id `NULL`. So, you will get the wrong answer. Instead, you should use the `IS NOT NULL` operator. Example:

```sql
SELECT * FROM customers WHERE id IS NOT NULL AND id != 2;
```

## Update

Now let's move to learn U of CRUD. Update and Delete are thankfully much simple, so don't worry, we will be able to breeze through it over the coming 20 mins. As the name suggests, this is used to update rows in a table. The general syntax is as follows:

```sql
UPDATE table_name SET column_name = value WHERE conditions;
```

Example:

```sql
UPDATE film SET release_year = 2006 WHERE id = 1;
```

The above query will update the `release_year` column of the row with `id` 1 in the `film` table to 2006. You can also update multiple columns at once. Example:

```sql
UPDATE film SET release_year = 2006, rating = 'PG' WHERE id = 1;
```

Let's talk about how update works. It works as follows:

```python
for each row in film:
    if row.matches(conditions in where clause)
        row['release_year'] = 2006
        row['rating'] = 'PG'
```

So basically update query iterates through all the rows in the table and updates the rows that match the conditions in the where clause. So, if you have a table with 1000 rows and you run an update query without a where clause, then all the 1000 rows will be updated. So, be careful while running update queries. Example:

```sql
UPDATE film SET release_year = 2006;
```

## Delete

Finally, we are at the end of CRUD. Let's talk about Delete operations. The general syntax is as follows:

```sql
DELETE FROM table_name WHERE conditions;
```

Example:

```sql
DELETE FROM film WHERE id = 1;
```

The above query will delete the row with `id` 1 from the `film` table. If you don't specify a where clause, then all the rows from the table will be deleted. Example:

```sql
DELETE FROM film;
```

Let's talk about how delete works as well in terms of code.

```python
for each row in film:
    if row.matches(conditions in where clause)
        delete row
```


### Agenda
 - Delete
 - Delete vs truncate vs drop
 - Limit
 - Count
 - Order By
 - Join 


### Delete

```sql
DELETE FROM table_name WHERE conditions;
```

Example:

```sql
DELETE FROM film WHERE id = 1;
```

The above query will delete the row with `id` 1 from the `film` table. 

Beware, If you don't specify a where clause, then all the rows from the table will be deleted. Example:

```sql
DELETE FROM film;
```

Let's talk about how delete works as well in terms of code.

```python
for each row in film:
    if row.matches(conditions in where clause)
        delete row
```

There is a minor advance thing about DELETE which we shall talk about along with Joins in the next class. So, don't worry about it for now.

### Delete vs Truncate vs Drop

There are two more commands which are used to delete rows from a table. They are `TRUNCATE` and `DROP`. Let's discuss them one by one.

#### Truncate

The command looks as follows:

```sql
TRUNCATE film;
```

The above query will delete all the rows from the `film` table. TRUNCATE command internally works by removing the complete table and then recreating it. So, it is much faster than DELETE. But it has a disadvantage. It cannot be rolled back. We will learn more about rollbacks in the class on Transactions (In short, rollbacks can only happen for incomplete transactions - not committed yet - to be discussed in future classes). But at a high level, this is because as the complete table is deleted as an intermediate step, no log is maintained as to what all rows were deleted, and thus is not easy to revert. So, if you run a TRUNCATE query, then you cannot undo it. 

>Note: It also resets the primary key ID. For example, if the highest ID in the table before truncating was 10, then the next row inserted after truncating will have an ID of 1.

#### Drop

The command looks as follows:

Example:

```sql
DROP TABLE film;
```

The above query will delete the `film` table. The difference between `DELETE` and `DROP` is that `DELETE` is used to delete rows from a table and `DROP` is used to delete the entire table. So, if you run a `DROP` query, then the entire table will be deleted. All the rows and the table structure will be deleted. So, be careful while running a `DROP` query. Nothing will be left of the table after running a `DROP` query. You will have to recreate the table from scratch.

Note that,
DELETE:
1. Removes specified rows one-by-one from table (may delete all rows if no condition is present in query but keeps table structure intact). 
2. It is slower than TRUNCATE.
3. Doesn't reset the key. 
4. It can be rolled back.

TRUNCATE:
1. Removes the complete table and then recreats it.
2. Faster than DELETE.
3. Resets the key.
4. It can not be rolled back because the complete table is deleted as an intermediate step.

DROP:
1. Removes complete table and the table structre as well.
2. It can not be rolled back.

Rollback to be discussed in transactions class. Note that there is no undo in SQL queries once the query is completely committed. 


### LIKE Operator

LIKE operator is one of the most important and frequently used operator in SQL. Whenever there is a column storing strings, there comes a requirement to do some kind of pattern matching. Example, assume Scaler's database where we have a `batches` table with a column called `name`. Let's say we want to get the list of `Academy` batches and the rule is that an Academy batch shall have `Academy` somewhere within the name. How do we find those? We can use the `LIKE` operator for this purpose. Example:

```sql
SELECT * FROM batches WHERE name LIKE '%Academy%';
```

Similarly, let's say in our Sakila database, we want to get all the films which have `LOVE` in their title. We can use the `LIKE` operator. Example:

```sql
SELECT * FROM film WHERE title LIKE '%LOVE%';
```

Let's talk about how the `LIKE` operator works. The `LIKE` operator works with the help of 2 wildcards in our queries, `%` and `_`. The `%` wildcard matches any number of characters (>= 0 occurrences of any set of characters). The `_` wildcard matches exactly one character (any character). Example:

1. LIKE 'cat%' will match "cat", "caterpillar", "category", etc. but not "wildcat" or "dog".
2. LIKE '%cat' will match "cat", "wildcat", "domesticcat", etc. but not "cattle" or "dog".
3. LIKE '%cat%' will match "cat", "wildcat", "cattle", "domesticcat", "caterpillar", "category", etc. but not "dog" or "bat".
4. LIKE '_at' will match "cat", "bat", "hat", etc. but not "wildcat" or "domesticcat".
5. LIKE 'c_t' will match "cat", "cot", "cut", etc. but not "chat" or "domesticcat".
6. LIKE 'c%t' will match "cat", "chart", "connect", "cult", etc. but not "wildcat", "domesticcat", "caterpillar", "category".


### COUNT

Count function takes the values from a particular column and returns the number of values in that set. Umm, but don't you think it will be exactly same as the number of rows in the table? Nope. Not true. Aggregate functions only take not null values into account. So, if there are any null values in the column, they will not be counted.

Example: Let's take a students table with data like follows:

| id | name | age | batch_id |
|----|------|-----|----------|
| 1  | A    | 20  | 1        |
| 2  | B    | 21  | 1        |
| 3  | C    | 22  | null     |
| 4  | D    | 23  | 2        |

If you will try to run COUNT and give it the values in batch_id column, it will return 3. Because there are 3 not null values in the column. This is different from number of rows in the students table.

Let's see how do you use this operation in SQL.

```sql
SELECT COUNT(batch_id) FROM students;
```

To understand how aggregate functions work via a pseudocode, let's see how SQL query optimizer may execute them.

```python
table = []

count = 0

for row in table:
    if row[batch_id] is not null:
        count += 1

print(count)
```

Few things to note here:
While printing, do we have access to the values of row? Nope. We only have access to the count variable. So, we can only print the count. Extrapolating this point, when you use aggregate functions, you can only print the result of the aggregate function. You cannot print the values of the rows.

Eg:
    
```sql
SELECT COUNT(batch_id), batch_id FROM students;
```

This will be an invalid query. Because, you are trying to print the values of `batch_id` column as well as the count of `batch_id` column. But, you can only print the count of `batch_id` column.

### LIMIT Clause

And now let's discuss the last clause for the day. LIMIT clause allows us to limit the number of rows returned by a query. Example:

```sql
SELECT * FROM film LIMIT 10;
```

The above query will return only 10 rows from the `film` table. If you want to return 10 rows starting from the 11th row, you can use the `OFFSET` keyword. Example:

```sql
SELECT * FROM film LIMIT 10 OFFSET 10;
```

The above query will return 10 rows starting from the 11th row from the `film` table. 
Note that in MySQL, you cannot use the `OFFSET` keyword without the `LIMIT` keyword. Example:

```sql
SELECT * FROM film OFFSET 10;
```

throws an error. 

LIMIT clause is applied at the end. Just before printing the results. Taking the example of pseudocode, it works as follows:

```python
answer = []

for each row in film:
    if row.matches(conditions in where clause) # new line from above
        answer.append(row)

answer.sort(column_names in order by clause)

filtered_answer = []

for each row in answer:
    filtered_answer.append(row['rating'], row['release_year'])

return filtered_answer[start_of_limit: end_of_limit]
```

Thus, if your query contains ORDER BY clause, then LIMIT clause will be applied after the ORDER BY clause. Example:

```sql
SELECT * FROM film ORDER BY title LIMIT 10;
```

The above query will return 10 rows from the `film` table in ascending order of the `title` column.


### ORDER BY Clause

Now let's discuss another important clause. ORDER BY clause allows to return values in a sorted order. Example:

```sql
SELECT * FROM film ORDER BY title;
```

The above query will return all the rows from the `film` table in ascending order of the `title` column. If you want to return the rows in descending order, you can use the `DESC` keyword. Example:

```sql
SELECT * FROM film ORDER BY title DESC;
```

You can also sort by multiple columns. Example:

```sql
SELECT * FROM film ORDER BY title, release_year;
```

The above query will return all the rows from the `film` table in ascending order of the `title` column and then in ascending order of the `release_year` column. Consider the second column as tie breaker. If 2 rows have same value of title, release year will be used to break tie between them. Example:

```sql
SELECT * FROM film ORDER BY title DESC, release_year DESC;
```

Above query will return all the rows from the `film` table in descending order of the `title` column and if tie on `title`, in descending order of the `release_year` column.

By the way, you can ORDER BY on a column which is not present in the SELECT clause. Example:

```sql
SELECT title FROM film ORDER BY release_year;
```

Let's also build the analogy of this with a pseudocode.

```python
answer = []

for each row in film:
    if row.matches(conditions in where clause) # new line from above
        answer.append(row)

answer.sort(column_names in order by clause)

filtered_answer = []

for each row in answer:
    filtered_answer.append(row['rating'], row['release_year'])

return filtered_answer
```

If you see, the `ORDER BY` clause is applied after the `WHERE` clause. So, first the rows are filtered based on the `WHERE` clause and then they are sorted based on the `ORDER BY` clause. And only after that are the columns that have to be printed taken out. And that's why you can sort based on columns not even in the `SELECT` clause.

#### ORDER BY Clause with DISTINCT keyword

If you also have DISTINCT in the SELECT clause, then you can only sort by columns that are present in the SELECT clause. Example:

```sql
SELECT DISTINCT title FROM film ORDER BY release_year;
```

The above query will give an error. You can only sort by `title` column. Example:

```sql
SELECT DISTINCT title FROM film ORDER BY title;
```

Why this? Because without this the results can be ambiguous. Example:

```sql
SELECT DISTINCT title FROM film ORDER BY release_year;
```

The above query will return all the distinct titles from the `film` table. But which `release_year` should be used to sort them? There can be multiple `release_year` for a particular `title`. So, the results will be ambiguous.

### Joins

Every SQL query we had written till now was only finding data from 1 table. Most of the queries we had written in the previous classes were on the `film` table where we applied multiple filters etc. But do you think being able to query data from a single table is enough? Let's take a scenario of Scaler. Let's say we have 2 tables as follows in the Scaler's database:

`batches`

| batch_id | batch_name |
|----------|------------|
| 1        | Batch A    |
| 2        | Batch B    |
| 3        | Batch C    |

`students`

| student_id | first_name | last_name | batch_id |
|------------|------------|-----------|----------|
| 1          | John       | Doe       | 1        |
| 2          | Jane       | Doe       | 1        |
| 3          | Jim        | Brown     | 2        |
| 4          | Jenny      | Smith     | 3        |
| 5          | Jack       | Johnson   | 2        |

Suppose, someone asks you to print the name of every student, along with the name of their batch. The output should be something like:

| student_name | batch_name |
|--------------|------------|
| John     | Batch A    |
| Jane     | Batch A    |
| Jim    | Batch B    |
| Jenny  | Batch C    |
| Jack | Batch B    |

Will you be able to get all of this data by querying over a single table? No. The `student_name` is there in the students table, while the `batch_name` is in the batches table! We somehow need a way to combine the data from both the tables. This is where joins come in. What does the word `join` mean to you? 

Joins, as the name suggests, are a way to combine data from multiple tables. For example, if I want to combine the data from the `students` and `batches` table, I can use joins for that. Think of joins as a way to stitch rows of 2 tables together, based on the condition you specify. Example: In our case, we would want to stitch a row of students table with a row of batches table based on what? Imagine that every row of `students` I try to match with every row of `batches`. Based on what condition to be true between those will I stitch them?

We would want to stitch a row of students table with a row of batches table based on the `batch_id` column. This is what we call a `join condition`. A join condition is a condition that must be true between the rows of 2 tables for them to be stitched together. Let's see how we can write a join query for our example. 

```sql
SELECT students.first_name, batches.batch_name
FROM students
JOIN batches
ON students.batch_id = batches.batch_id;
```

Let's break down this query. The first line is the same as what we have been writing till now. We are selecting the `first_name` column from the `students` table and the `batch_name` column from the `batches` table. The next line is where the magic happens. We are using the `JOIN` keyword to tell SQL that we want to join the `students` table with the `batches` table. The next line is the join condition. We are saying that we want to join the rows of `students` table with the rows of `batches` table where the `batch_id` column of `students` table is equal to the `batch_id` column of `batches` table. This is how we write a join query. 

Let's take an example of this on the Sakila database. Let's say for every film, we want to print its name and the language. How can we do that?

```sql
SELECT film.title, language.name
FROM film
JOIN language
ON film.language_id = language.language_id;
```

Now, sometimes typing name of tables in the query can become difficult. For example, in the above query, we have to type `film` and `language` multiple times. To make this easier, we can give aliases to the tables. For example, we can give the alias `f` to the `film` table and `l` to the `language` table. We can then use these aliases in our query. Let's see how we can do that:

```sql
SELECT f.title, l.name
FROM film AS f
JOIN language AS l
ON f.language_id = l.language_id;
```



## Agenda

 - Self Join
 - More problems on Joins
 - Inner vs Outer joins
 - WHERE vs ON
 - Union and Union All 


## Self Join

Let's say at Scaler, for every student we assign a Buddy. For this we have a `students` table, which looks as follows:

`id | name | buddy_id`

This `buddy_id` will be an id of what?

Correct. Now, let's say we have to print for every student, their name and their buddy's name. How will we do that? Here 2 rows of which tables would we want to stitch together to get this data?

Correct, an SQL query for the same shall look like:

```sql
SELECT s1.name, s2.name
FROM students s1
JOIN students s2
ON s1.buddy_id = s2.id;
```

This is an example of SELF join. A self join is a join where we are joining a table with itself. In the above query, we are joining the `students` table with itself. In a self joining, aliasing tables is very important. If we don't alias the tables, then SQL will not know which row of the table to match with which row of the same table (because both of them have same names as they are the same table only).

### SQL query as pseudocode

As we have been doing since the CRUD class, let's also see how Joins can be represented in terms of pseudocode.

Let's take this query:

```sql
SELECT s1.name, s2.name
FROM students s1
JOIN students s2
ON s1.buddy_id = s2.id;
```

In pseudocode, it shall look like:

```python3
ans = []

for row1 in students:
    for row2 in students:
        if row1.buddy_id == row2.id:
            ans.add(row1 + row2)

for row in ans:
    print(row.name, row.name)
```

## More problems on JOIN

### Joining multiple tables

Till now, we had only joined 2 tables. But what if we want to join more than 2 tables? Let's say we want to print the name of every film, along with the name of the language and the name of the original language. How can we do that? If you have to add 3 numbers, how do you do that?

To get the name of the language, we would first want to combine film and language table over the `language_id` column. Then, we would want to combine the result of that with the language table again over the `original_language_id` column. This is how we can do that:

```sql
SELECT f.title, l1.name, l2.name
FROM film f
JOIN language l1
ON f.language_id = l1.language_id
JOIN language l2
ON f.original_language_id = l2.language_id;
```

Let's see how this might work in terms of pseudocode:

```python3
ans = []

for row1 in film:
    for row2 in language:
        if row1.language_id == row2.id:
            ans.add(row1 + row2)

for row in ans:
    for row3 in language:
        if row.language_id == row3.language_id:
            ans.add(row + row3)

for row in ans:
    print(row.name, row.language_name, row.original_language_name)
```

### Joins with multiple conditions in ON clause

Till now, whenever we did a join, we joined based on only 1 condition. Like in where clause we can combine multiple conditions, in Joins as well, we can have multiple conditions.

Let's see an example. For every film, name all the films that were released in the range of 2 years before or after that film and there rental rate was more than the rate of the movie.

```sql
SELECT f1.name, f2.name
FROM film f1
JOIN film f2
ON (f2.year BETWEEN f1.year - 2 AND f1.year + 2) AND f2.rental > f1.rental;
```

> Note:
> 1. Join does not need to happen on equality of columns always.
> 2. Join can also have multiple conditions.

A Compound Join is one where Join has multiple conditions on different columns.


## Inner vs Outer Joins

While we have pretty much discussed everything that is mostly important to know about joins, there are a few nitty gritties that we should know about.

Let's take the join query we had written a bit earlier:

```sql
SELECT s1.name, s2.name
FROM students s1
JOIN students s2
ON s1.buddy_id = s2.id;
```

Let's say there is a student that does not have a buddy, i.e., their `buddy_id` is null. What will happen in this case? Will the student be printed?

If you remember what we discussed about CRUD , is NULL equal to anything? Nope. Thus, the row will never match with anything and not get printed. The join that we discussed earlier is also called inner join. You could have also written that as:

```sql
SELECT s1.name, s2.name
FROM students s1
INNER JOIN students s2
ON s1.buddy_id = s2.id
```

The keyword INNER is optional. By default a join is INNER join.

As you see, an INNER JOIN doesn't include a row that didn't match the condition for any combination.

Opposite of INNER JOIN is OUTER JOIN. Outer Join will include all rows, even if they don't match the condition. There are 3 types of outer joins:
- Left Join
- Right Join
- Full Join

As the names convey, left join will include all rows from the left table, right join will include all rows from the right table and full join will include all rows from both the tables.

Let's take an example to understand these well:

Assume we have 2 tables: students and batches with following data:


`batches`

| batch_id | batch_name |
|----------|------------|
| 1        | Batch A    |
| 2        | Batch B    |
| 3        | Batch C    |

`students`

| student_id | name       | batch_id |
|------------|------------|----------|
| 1          | John       | 1        |
| 2          | Jane       | 1        |
| 3          | Jim        | null     |
| 4          | Ram        | null     |
| 5          | Sita       | 2        |

Now let's write queries to do each of these joins:

```sql
SELECT s.name, b.batch_name
FROM students s
LEFT JOIN batches b
ON s.batch_id = b.batch_id;
```

```sql
SELECT s.name, b.batch_name
FROM students s
RIGHT JOIN batches b
ON s.batch_id = b.batch_id;
```

```sql
SELECT s.name, b.batch_name
FROM students s
FULL OUTER JOIN batches b
ON s.batch_id = b.batch_id;
```


Now let's use different types of joins and tell me which row do you think will not be a part of the join.

Output of LEFT JOIN (Go row by row in left table - which is students and then look for match/matches):

```
John batchA
Jane batchA
Jim NULL
Ram NULL
Sita batchB
```

Output of RIGHT JOIN (Go row by row in right table - which is batches table and then look for match/matches):
batchA has 2 matches - John and Jane
batchB has 1 match - Sita
batchC has 0 match - NULL

```
John batchA
Jane batchA
Sita batchB
NULL batchC
```

Output of FULL JOIN (Do the left join. Then look at every row of right table which is `batches` and figure out rows which were not printed yet - print them with null match)

```
John batchA
Jane batchA
Jim NULL
Ram NULL
Sita batchB
NULL batchC
```

## Join with WHERE v/s ON

Let's take an example to discuss this. If we consider a simple query:
```sql
SELECT *
FROM A
JOIN B
ON A.id = B.id;
```
In pseudocode, it will look like:

```python3
ans = []

for row1 in A:
    for row2 in B:
        if (ON condition matches):
            ans.add(row1 + row2)

for row in ans:
    print(row.id, row.id)
```
Here, the size of intermediary table (`ans`) will be less than `n*m` because some rows are filtered.

We can also write the above query in this way:

```sql
SELECT *
FROM A, B
WHERE A.id = B.id;
```
The above query is nothing but a CROSS JOIN behind the scenes which can be written as:

```sql
SELECT *
FROM A
CROSS JOIN B
WHERE A.id = B.id;
```
Here, the intermediary table `A CROSS JOIN B` is formed before going to WHERE condition.

In pseudocode, it will look like:

```python3
ans = []

for row1 in A:
    for row2 in B:
        ans.add(row1 + row2)

for row in ans:
    if (WHERE condition matches):
        print(row.id, row.id)
```

The size of `ans` is always `n*m` because table has cross join of A and B. The filtering (WHERE condition) happens after the table is formed.

From this example, we can see that:
1. The size of the intermediary table (`ans`) is always greater or equal when using WHERE compared to using the ON condition. Therefore, joining with ON uses less internal space.
2. The number of iterations on `ans` is higher when using WHERE compared to using ON. Therefore, joining with ON is more time efficient.

In conclusion,
1. The ON condition is applied during the creation of the intermediary table, resulting in lower memory usage and better performance.
2. The WHERE condition is applied during the final printing stage, requiring additional memory and resulting in slower performance.
3. Unless you want to create all possible pairs, avoid using CROSS JOINS.

## UNION and UNION ALL

Sometimes, we want to print the combination of results of multiple queries. Let's take an example of the following tables:

`students`
| id | name |
|----|------|

`employees`
| id | name |
|----|------|

`investors`
| id | name |
|----|------|


You are asked to print the names of everyone associated with Scaler. So, in the result we will have one column with all the names.

We can't have 3 SELECT name queries because it will not produce this singular column. We basically need SUM of such 3 queries. Join is used to stitch or combine rows, here we need to add the rows of one query after the other to create final result.

UNION allows you to combine the output of multiple queries one after the other.

```sql
SELECT name FROM students
UNION
SELECT name FROM employees
UNION
SELECT name FROM investors;
```
Now, as the output is added one after the other, there is a constraint: Each of these individual queries should output the same number of columns.

Note that, you can't use ORDER BY for the combined result because each of these queries are executed independently.

UNION outputs distinct values of the combined result. **It stores the output of individual queries in a set and then outputs those values in final result. Hence, we get distinct values. But if we want to keep all the values, we can use UNION ALL. It stores the output of individual queries in a list and gives the output, so we get all the duplicate values.**

If you want to perform any operation on the combined result, you put them in braces and give it an alias. 
For example, 

```sql
SELECT
  first_name, last_name
FROM
(SELECT first_name, last_name
FROM customer

UNION

SELECT first_name, last_name
FROM actor) AS some_alias


ORDER BY first_name, last_name
LIMIT 10
```


## Agenda

 - Group By
 - Group by on multiple columns
 - Having clause
 - Sub-queries 

## GROUP BY Clause

Till now we combined multiple values into a single values by doing some operation on all of them. What if, we want to get the final values in multiple sets? That is, we want to get the set of values as our result in which each value is derived from a group of values from the column. 

The way Group By clause works is it allows us to break the table into multiple groups so as to be used by the aggregate function. 

For example: `GROUP BY batch_id` will bring all rows with same `batch_id` together in one group

> Note: Also, GROUP BY always works before aggregate functions. Group By is used to apply aggregate function within groups (collection of rows). The result comes out to be a set of values where each value is derived from its corresponding group.

Let's take an example.


| id | name | age | batch_id |
|----|------|-----|----------|
| 1  | A    | 20  | 1        |
| 2  | B    | 21  | 3        |
| 3  | C    | 22  | 1        |
| 4  | D    | 23  | 2        |
| 5  | E    | 23  | 1        |
| 6  | F    | 25  | 2        |
| 7  | G    | 22  | 3        |
| 8  | H    | 21  | 2        |
| 9  | I    | 20  | 1        |

```sql
SELECT COUNT(*), batch_id FROM students GROUP BY batch_id;
```

The result of above query will be:
| COUNT(\*) | batch_id |
|-----------|----------|
| 4         | 1        |
| 3         | 2        |
| 2         | 3        |

Explanation: The query breaks the table into 3 groups each having rows with `batch_id` as 1, 2, 3 respectively. There are 4 rows with `batch_id = 1`, 3 rows with `batch_id = 2` and 2 rows with `batch_id = 3`.

Note that, we can only use the columns in SELECT which are present in Group By because only those columns will have same value across all rows in a group.

**Ordering of Operations:**

```
1. Select the tables. 
  1.2. Do the joins if required
2. Apply the filters (where clause) 
3. Group by 
   3.2: Filtering happens with having clause 
4. Select what to print including aggregates
5. Order by, limit, offset. 
```

### Examples

***Q1: Print the name of every actor (first_name, last_name) and with that print the number of films they have acted in.***

```sql
SELECT
    a.first_name, a.last_name, count(1) AS count_movies

  FROM actor a
    JOIN film_actor b
       ON a.actor_id = b.actor_id
  
       
GROUP BY a.actor_id
```

***Q2: If you have a table `user_classes` with columns as (userID, classID, attended (0 / 1)), then find user-wise attendance.***

```sql
SELECT userid, AVG(attended) FROM user_classes GROUP BY userid
```

### Group by on multiple columns

**Table: companies_users**

| user_id | company_id | round_date | interview_result |
| --- | --- | --- | --- |
| 1 | 1 | 2023-07-01 | 1 |
| 1 | 1 | 2023-07-03 | 1 |
| 1 | 1 | 2023-07-07 | 0 |
| 1 | 2 | 2023-07-02 | 0 |
| 2 | 2 | 2023-07-03 | 1 |
| 2 | 2 | 2023-07-04 | 1 |

***Q:Find the number of rounds given by every user in every company they interviewed for.***

```sql
SELECT user_id, company_id, count(1)
FROM companies_users 
GROUP BY user_id, company_id
```

## HAVING Clause

HAVING clause is used to filter groups. Let's take a question to understand the need of HAVING clause:

There are 2 tables: Students(id, name, age, batch_id) and Batches(id, name). Print the batch names that have more than 100 students along with count of the students in each batch.

```sql
SELECT COUNT(S.id), B.name
FROM Students S
JOIN Batches B ON S.batch_id = B.id
GROUP BY B.name;
HAVING COUNT(S.id) > 100;
```

Here, `GROUP BY B.name` groups the results by the `B.name` column (batch name). It ensures that the count is calculated for each distinct batch name. 
`HAVING COUNT(S.id) > 100` condition filters the grouped results based on the count of `S.id` (number of students). It retains only the groups where the count is greater than 100.

The sequence in which query executes is: 
- Firstly, join of the two tables is done. 
- Then is is divided into groups based on `B.name`. 
- In the third step, result is filtered using the condition in HAVING clause. 
- Lastly, it is printed through SELECT.

FROM -> WHERE -> GROUP BY -> HAVING -> SELECT 

WHERE is not build to be able to handle aggregates. We can not use WHERE after GROUP BY because WHERE clause works on rows and as soon as GROUP BY forms a result, the rows are convereted into groups. So, no individual conditions or actions can be performed on rows after GROUP BY. 

## SUBQUERIES

Imagine you are given an employee table which has all employee ID, names and their salary.
If I asked you to report employees who earn more than company average, how would you do it? 

Note that the following query does not work:

```sql
SELECT * FROM employees WHERE salary > AVG(salary)
```

**Why?:** Because where clause filters row by row. Aggregation only happens at the time of printing (unless for group_by and having clause). WHERE clause does not know about AVG(salary). 

Manually, I will first find out the company average and then put it in a query. But what if I did not want to put it manually. Subqueries come to our rescue here. 

If I break the above down, what are the steps:

 - Step 1: Find the average salary amongst all employees. 

```sql
SELECT AVG(salary) FROM employees
```

 - Step 2: Find all employees who make more than the above number. 

```sql
SELECT * FROM employees WHERE salary > (SELECT AVG(salary) FROM employees)
```

As you can see, in SQL, it's possible to place a SQL query inside another query. This inner query is known as a subquery.
In a subquery, the outer query's result depends on the result set of the inner subquery. That's why subqueries are also called nested queries.

### More examples

***Q: Find all employees who make more salary than their department average.***

What's step 1 here? I need to find out department wise average salaries. 
Ok, let's do that. 

```sql
SELECT dept, AVG(salary) FROM employees GROUP BY dept
```

If the above was a table, would it be possible to get result quickly by doing a JOIN. Oh yes, absolutely. Let's do that then. 

```sql
SELECT
  e.id, e.name
FROM employees AS e
  JOIN (SELECT dept, AVG(salary) AS dept_salary FROM employees GROUP BY dept) AS tmp_table
  ON (e.dept = tmp_table.dept AND e.salary > tmp_table.dept_salary)
```

this helps build intuition about group by, having and sub-queries. 



## Agenda

- Introduction to Indexing
- How Indexes Work
- Indexes and Range Queries
    - Data structures used for indexing
- Cons of Indexes
- Indexes on Multiple Columns
- Indexing on Strings
- How to create index


## Introduction to Indexing

Hello Everyone

Till now, in the course, we had been discussing majorly about how to write SQL queries to fetch data we want to fetch. While discussing those queries, I also often wrote pseudocode talking about how at a higher level that query might work behind the scenes. 

Let us go back to that pseudocode. What do you think are some of the problems you see a user of DB will face if the DB really worked exactly how the pseudocode mentioned it worked?

Correct! In the pseudocode we had, for loops iterated over each row of the database to retrieve the desired rows. This resulted in a minimum time complexity of O(N) for every query. When joins or other operations are involved, the complexity further increases.

Adding to this, in which hardware medium is the data stored in a database?

Yes. A database stores its data in disk. Now, one of the biggest problems with disk is that accessing data from disk is very slow. Much slower than accessing data from RAM. For reference, read https://gist.github.com/jboner/2841832 Reading data from disk is 20x slower than reading from RAM! Let's talk about how data is fetched from the disk. We all know that on disk DB stores data of each row one after other. When data is fetched from disk, OS fetches data in forms of blocks. That means, it reads not just the location that you wnat to read, but also locations nearby.

First OS fetches data from disk to memory, then CPU reads from memory. Now imagine a table with 100 M rows and you have to first get the data for each row from disk into RAM, then read it. It will be very slow. Imagine you have a query like:

```sql
select * from students where id = 100;
```

To execute above, you will have to go through literally each row on the disk, and access even the blocks where this row doesn't exist. Don't you think this is a massive issue and can lead to performance problems?

To understand this better, let's take an example of a book. Imagine a big book covering a lot of topics. Now, if you want to find a particular topic in the book, what will you do? Will you start reading the book from the first page? No, right? You will go to the index of the book, find the page number of the topic you want to read, and then go to that page. This is exactly what indexing is. As index of a book helps go to the correct page of the book fast, the index of a database helps go to the correct block of the disk fast.

Now this is a very important line. Many people say that an index sorts a table. Nope. It has nothing to do with sorting. We will go over this a bit later in today's class. The major problem statement that indexes solve is to reduce the number of disk block accesses to be done. By preventing wastefull disk block accesses, indexes are able to increase performance of queries.

## How Indexes Work

While we have talked about the problem statement that indexes help solve, let's talk about how indexes work behind the scenes to optimize the queries. Let's try to build indexes ourselves. Let's imagine a huge table with 100s of millions of rows in table spread across 100s of disk blocks. We have a query like:

```sql
select * from students where id = 100;
```

We want to somehow avoid going to any of the disk block that is definitely not going to have the student with id 100. I need something that can help me directly know that hey, the row with id 100 is present in this block. Are you familiar with a data structure that can be stored in memory and can quickly provide the block information for each ID?

Correct. A map or a hashtable, whatever you call it can help us. If we maintain a hashmap where key is the id of the student and value is the disk block where the row containing that ID is present, is it going to solve our problem? Yes! That will help. Now, we can directly go to the block where the row is present and fetch the row. This is exactly how indexes work. They use some other data structure, which we will come to later.

Here we had queries on id. An important thing about `id` is that id is?

Yes. ID is unique. Will the same approach work if the column on which we are querying may have duplicates? Like multiple rows with same value of that column? Let's see. Let's imagine we have an SQL query as follows:

```sql
select * from students where name = 'Naman';
```

How will you modify your map to be able to accomodate multiple rows with name 'Naman'? 

Yes. What if we modify our map a bit. Now our keys will be String (name) and values will be a list of blocks that contain that name. Now, for a query, we will first go to the list of blocks for that name, and then go to each block and fetch the rows. This way as well, have we avoided fetching the blocks from the disk that were useless? Yes! Again, this will ensure our performance speeds up.

## Indexes and Range Queries

So, is this all that is there about indexes? Are they that simple? Well, no. Are the SQL queries you write always like `x = y`? What other kind of queries you often have to do in DB?

If a HashMap is how an index works, do you think it will be able to take care of range queries? Let's say we have a query like:

```sql
select * from students where psp between 40.1 and 90.1;
```

Will you be able to use hashmap to get the blocks that contain these students? Nope. A hashmap allows you to get a value in O(1) but if you have to check all the values in the range, you will have to check them 1 by 1 and potentially it will take O(N) time.

Hmm. So how will we solve it. Is there any other type of Map you know? Something that allow you to iterate over the values in a sorted way?

Correct. There is another type of Map called TreeMap. 

Let's in brief talk about the working of a TreeMap. For more detailed discussion, revise your DSA classes. A TreeMap uses a Balanced Binary Search Tree (often AVL Tree or Red Black Tree) to store data. Here, each node contains data and the pointers to left and right node.

Now, how will a TreeMap help us in our case? A TreeMap allows us to get the node we are trying to query in O(log N). From there, we can move to the next biggest value in O(log N). Thus, queries on range can also be solved.

## B and B+ Trees

Databases also use a Tree like data structure to store indexes. But they don't use a TreeMap. They use a B Tree or a B+ Tree. Here, each node can have multiple children. This helps further reduce the height of the tree, making queries faster. We will learn about these later.

## Cons of Indexes

While we have seen how indexes help make the read queries faster, like everything in engineering, they also have their cons. Let's try to think of those. What are the 4 types of operations we can do on a database? Out of these, which operations may require us to do extra work because of indexes?

Yes, whenever we update data, we may also have to update the corresponding nodes in the index. This will require us to do extra work and thus slow down those operations. 

Also, do you think we can store index only on memory? Well technically yes, but memory is volatile. If something goes wrong, we may have to recreate complete index again. Thus, often a copy of index is also stored on disk. This also requires extra space. There are two big problems that can arise with the use of index:
1. Writes will be slower
2. Extra storage


Thus, it is recommended to use index if and only if you see the need for it. Don't create indexes prematurely. 

## Indexes on Multiple Columns

How do you decide on which columns to create an index? Let's revisit how an index works. If I create an index on the `id` column, the tree map used for storing data will allow for faster retrieval based on that column. However, a query like: 

```sql
select * from students where psp = 90.1;
```

will not be faster with this index. The index on `id` has no relevance to the `psp` column, and the query will perform just as slowly as before. Therefore, we need to create an index on the column that we are querying.

We can also create index on 2 columns. Imagine a students table with columns like:

`id | name | email | batch_id | psp |`

We are writing a query like this:

```sql
select * from students where name = 'Naman';
```

Let's say I create an index on (id, name). Let's see how the index will look like:

When create index on these 2 columns, it is indexed according to id first and then if there is a tie it, will be indexed on name. So, there can be a name with different ids and we will not be able to filter it, as name is just a tie breaker here.

Thus, if we create an index on (id, name), it will actually not help us on the filter of name column. 

## Indexing on Strings

Now let's think of a scenario. How often do we need to use a query like this:

```sql
SELECT * FROM user WHERE email = 'abc@scaler.com';
```

But this query is very slow, so we will definitely create an index on the email column. So, the map that is created behind the scenes using indexing will have email mapped to the corresponding block in the memory.

Now, instead of creating index on whole email, we can create an index for the first part of the email (text before @) and have list of blocks (for more than one email having same first part) mapped to it. Hence, the space is saved.

Typically, with string columns, index is created on prefix of the column instead of the whole column. It gives enough increase in performance.

Consider the query:
```sql
SELECT * FROM user
WHERE address LIKE '%ambala%';
```

We can see that indexing will not help in such queries for pattern matching. In such cases, we use Full-Text Index about which we will discuss later.

## How to create index

Let's look at the syntax using `film` table:
```sql
CREATE INDEX idx_film_title_release
ON film(title, release_year);
```

Good practices for creating index:
1. Prefix the index name by 'idx'
2. Format for index name - idx\<underscore>\<table name>\<underscore>\<attribute name1>\<underscore>\<attribute name2>...


Now, let's use the index in a query:
```sql
EXPLAIN ANALYZE SELECT * FROM film
WHERE title = 'Shawshank Redemption';
```

If you look at the log of this query, "Index lookup on film using idx_film_title_release" is printed. If we remove the index and run the above query again, we can see that the time in executing the query is different. In case where indexing is not used, it takes more time to execute and more rows are searched to find the title.


## Agenda

 - Need for concurrency
 - Problems that arise with concurrency
 - Introduction to transactions
 - Commit / Rollback
 - ACID
 - Is ACID boolean
 - Durability levels
 - Isolation levels


## Need for concurrency

Till now, all our SQL queries were written with the assumption that there is no interference from any other operation on the machine. 
Basically, all operations are being run sequentially. 

That's however like there being only one queue in immigration. Leads to things being slow and large wait time for someone in the queue.
In such a case, what do you do? 
Correct. Open multiple counters so that there are multiple *parallel* lines. 

Very similarily, in a database, there could be multiple people trying to run their queries at the same time. If DB chooses to run them sequentially, it will become really slow. Machines have multi-core CPUs. So, Database can think of running multiple queries concurrently which will increase it's throughput and reduce the wait time for people trying to run their queries. 

## Problems that arise with concurrency 

However, concurrency is not all good. It can lead to some issues around data integrity and unexpected behavior. Let's explore one such case.

Imagine we have a database for a bank. 
What's one common transaction in a bank? Transfer money from person X to person Y. 

What would be steps of doing that money transaction (let's say transfer 500 INR from X to Y):

```
  1. Read balA = current balance of user X. 
  2. If balA >= 500:
  3.   update current balane of user X to be (balA - 500)
  4.   Read balB = current balance of user Y
  5.   update current balance of user Y to be (balB + 500)

```


Let's imagine there are 2 money transactions happening at the same time - Person A transferring 700 INR to Person B, and Person A transferring 800 INR to Person C. 
Assume current balance of A is 1000, B is 5000, C is 2000. 

It is possible that Step 1 (`Read balA = current balance of A`) gets exectuted for both money transaction at the same time. So, both money transaction find balA = 1000. And hence step 2 (balance being larger than the money being transferred) passes for both. Then step 3 gets executed for both money transactions (let's say). A's balance will be updated to 300 by money transaction 1 and then to 200 by money transaction 2. 
A's balance at the end will be 200, with both B and C getting the money and ending at 5700 and 2800 respectively. 

Total sum of money does not add up. Seems like the bank owes more money now. 
If you see, if both money transactions had happened one after another (after first had completely finished), then this issue would not have occurred. 
How do we avoid this? 

## Introduction to transactions. 

Let's understand the solution to the above in 2 parts. 

 1. What guidelines does the database management system give to the end user to be able to solve the above. Basically, what should I do as the end user, and the guarantees provided by my database. 
 2. How does the DB really solve it internally? What's happening behind the scene. 

Let's first look at 1. What tools does the DBMS give to me to be able to avoid situations like the above. 

In the above case, doing a money transaction involved 5 steps (multiple SQL queries). 
Database says why don't you group these tasks into a single unit called **Transactions**. 

Formally, Transactions group a set of tasks into a single execution unit. Each transaction begins with a specific task and ends when all the tasks in the group successfully complete. If any of the tasks fail, the transaction fails. Therefore, a transaction has only two results: success or failure.

For example, a transaction example could be:

```sql
BEGIN TRANSACTION

UPDATE film SET title = "TempTitle1" WHERE id = 10;
UPDATE film SET title = "TempTitle2" WHERE id = 100;

COMMIT
```

The above transaction has 2 SQL statements. These statements do not get finalized on the disk until commit command is executed. If any statement fails, all updates are rolled back (like undo operation). 
You can also explicitly write `ROLLBACK` which undoes all operations till the last commit. 

Database basically indicates that if you want a group of operations to happen together and you want database to handle all concurrency, put them in a single transaction and then send it to the database. 
If you do so, database promises the following. 

## ACID

If you send a transaction to a DBMS, it sets the following expectations to you:

 - **ATOMICITY:** All or none. Either all operations in the transactions will succeed or none will. 
 - **CONSISTENCY:** Correctness / Validity. All operations will be executed correctly and will leave the database in a consistent state before and after the transaction. For example, in the money transfer example, consistency was violated because the money amount sum should have stayed the same, but it was not. 
 - **ISOLATION:** Multiple transactions can be executed concurrently without interfering with each other. Isolation is one of the factors helping with consistency. 
 - **DURABILITY:** Updates/Writes to the database are permanent and will not be lost. They are persisted. 


However, there is one caveat to the above. Atomicity is boolean - all transactions are definitely atomic. 
But all the remaining parameters are not really boolean but have levels. That is so, because there is a tradeoff. To make my database support highest amount of isolation and consistency, I will have to compromise performance which we will see later. So, based on your application requirement, your DBMS lets you configure the level of isolation or durability. Let's discuss them one by one. 

### Durability levels

The most basic form of durability is writing updates to disk. However, someone can argue that what if my hard disk has a failure which causes me to loose information stored on the hard disk. 
I can choose then to have replica and all commits are forwarded to replicas as well. That has cost of latency and cost of additional machines. 
We will discuss more about master slave and replication during system design classes. 

## Isolation Levels

Before we explore isolation levels, let's understand how would database handle concurrency between multiple transactions happening at the same time. 
Typically, you would take locks to block other operations from interfering with your current transactions. [You'll study more about locks during concurrency class]. 
When you take a lock on a table row for example, any other transaction which also might be trying to access the same row would wait for you to complete. Which means with a lot of locks, overall transactions become slower, as they may be spending a lot of time waiting for locks to be released. 

Locks are of 2 kinds:
 - Shared Locks: Which means multiple transactions could be reading the same entity at the same time. However, a transaction that intends to write, will have to wait for ongoing reads to finish, and then would have to block all other reads and writes when it is writing/updating the entity. 
 - Exclusive Locks: Exclusive lock when taken blocks all reads and writes from other transaction. They have to wait till this transaction is complete. 
There are other kind of locks as well, but not relevant to this discussion for now.

A database can use a combination of the above to achieve isolation during multiple transactions happening at the same time. 
Note that the locks are acquired on rows of the table instead of the entire table. More granular the lock, better it is for performance. 

As we can see that locks interfere with performance, database lets you choose isolation levels. Lower the level, more the performance, but lower the isolation/consistency levels. 

The isolation levels are the following:

### Read uncommitted.

This is most relaxed isolation level. In READ UNCOMMITTED isolation level, there isn’t much isolation present between the transactions at all, ie ., No locks.
This is the lowest level of isolation, and does almost nothing. It means that transactions can read data being worked with by other transactions, even if the changes aren’t committed yet. This means the performance is going to be really fast. 

However, there are major challenges to consistency. 
Let's consider a case. 

| Time | Transaction 1 | Transaction 2 |
| ---  | ------------- | ------------- |
| 1 | Update row #1, balance updated from 500 to 1000 | | 
| 2 | | Select row #1, gets value as 1000 |
| 3 | Rollback (balance reverted to 500) | | 

T1 reverts the balance to 500. However, T2 is still using the balance as 1000 because it read a value which was not committed yet. This is also called as `dirty read`. 
`Read uncommitted` has the problem of dirty reads when concurrent transactions are happening. 

**Example usecase:** Imagine you wanted to maintain count of live users on hotstar live match. You want very high performance, and you don't really care about the exact count. If count is off by a little, you don't mind. So, you won't mind compromising consistency for performance. Hence, read uncommitted is the right isolation level for such a use case. 

### Read committed

The next level of isolation is READ_COMMITTED, which adds a little locking into the equation to avoid dirty reads. In READ_COMMITTED, transactions can only read data once writes have been committed. Let’s use our two transactions, but change up the order a bit: T2 is going to read data after T1 has written to it, but then T1 gets rolled back (for some reason).

| Time | Transaction 1 | Transaction 2 |
| ---  | ------------- | ------------- |
| 1 | Selects row #1 | |
| 2 | Updates row #1, acquires lock | |
| 3	| | Tries to select row #1, but blocked by T1’s lock |
| 4 | Rolls back transaction | |
| 5 | | Selects row #1 |

READ_COMMITTED helps avoid a dirty read here: if T2 was allowed to read row #1 at Time 3, that read would be invalid; T1 ended up getting rolled back, so the data that T2 read was actually wrong. Because of the lock acquired at Time 2 (thanks READ_COMMITTED!), everything works smoothly and T2 waits to execute its SELECT query.

**This is the default isolation levels in some DBMS like Postgres.**

However, this isolation level has a problem of **Non-repeatable reads.** Let's understand what that is.

Consider the following. 

| Time | Transaction 1 | Transaction 2 |
| ---  | ------------- | ------------- |
| 1 | Selects emails with low psp | |
| 2 | | update some low psp users with a better psp, acquires lock |
| 3 | | commit, lock released |
| 4	| Select emails with low psp again | |

At timestamp 4, I might want to read the emails again because I might want to update the status of having scheduled reminder emails to them. However, I will get a different set of emails in the same transaction (timestamp 1 vs timestamp 4). This issues is called non-repeatable reads and can happen in the current isolation level. 

### Repeatable reads

The third isolation level is repeatable reads. This is the default isolation levels in many DBMS including MySQL. 

The primary difference in repeable reads is the following:
 - Every transaction reads all the committed rows required for executing reads and writes before the start of the transaction and stores it locally in memory as a snapshot. That way, if you read the same information multiple times in the same transaction, you will get the same entries. 
 - Locking mechanism:
   - Writes acquire exclusive locks (same as read committed)
   - Reads with write intent (SELECT FOR UPDATE) acquire exclusive locks. 

Further reading: https://ssudan16.medium.com/database-isolation-levels-explained-61429c4b1e31 

| Time | Transaction 1 | Transaction 2 |
| ---- | ------------- | ------------- |
| 1 | Selects row #1 **for update**, acquires lock on row #1 | |
| 2	|  | Tries to update row #1, but is blocked by T1’s lock |
| 3 | updates row #1, commits transaction | |
| 4 | | Updates row #1 |

The first example we took of money transfer could work if select for update is properly used in transactions with this isolation level. 
However, this still has the following issue:
 - Normal reads do not take any lock. So, it is possible while I have a local copy in my snapshot, the real values in DB have changed. Reads are not strongly consistent. 
 - Phantom reads: A very corner case, but the table might change if there are new rows inserted while the transaction is ongoing. Since new rows were not part of the snapshot, it might cause inconsistency in new writes, reads or updates. 

### Serializable Isolation level

This is the strictest isolation level in a DB. It's the same as repeatable reads with the following differences:
 - All reads acquire a shared lock. So, they don't let updates happen till they are completed. 
 - No snapshots required anymore.
 - Range locking - To avoid phantom reads, this isolation level also locks a few entries in the range close to what is being read. 

**Example usecase:** This is the isolation levels that banks use because they want strong consistency with every single piece of their information. 
However, systems that do not require as strict isolation levels (like Scaler or Facebook) would then use Read Committed OR Repeatable Reads. 




## Agenda

- What is Schema Design
- What can go wrong
- Normalisation
- How to approach Schema Design
- Cardinality
    - How to find cardinality in relations
    - How to represent different cardinalities
- Nuances when representing relations

## What is Schema Design

Let's understand what Schema is. Schema refers to the structure of the database. Broadly speaking, schema gives information about the following:
- Structure of a database
- Tables in a database
- Columns in a table
- Primary Key
- Foreign Key
- Index
- Pictorial representation of how the DB is structured.

In general, 'Design' refers to the pictorial reference for solving how should something be formed considering the constraints. Prototyping, blueprinting or a plan, or structuring how something should exist is called Design.

Before any table or database is created for a software, a design document is formed consisting:
- Schema
- Class Diagram
- Architectural Diagram

## What can go wrong


#### Example 1:
Let's say Flipkart has a table for t-shirts. T-shirt has a column named color. 
Some t-shirts could have multiple colors. What do you put in the color column then? Maybe I put all the colors comma separated. 

So, something like, 

| tshirt_id | collar_type | size | color |
|-----------|-------------|------|-------|
| 1 | Round | M | red |
| 2 | Round | L | red, green | 
| 3 | Round | L | blue, red | 

How do you find all t-shirts of color red here. 

```sql
SELECT * FROM tshirt WHERE color LIKE "%red%"
```

The above query is going to do full-text search on color. You'll not be able to make it fast as it cannot leverage the power of indexing. 
And for that reason, some of your queries will always be slow. 


#### Example 2: 

Let's say we want to store classes and their instructor. Instead of creating 2 separate tables, I choose to put all information in one single table. 


| class_id | topic | instructor_id | instructor_name | Instructor_email |
|----------|-------|---------------|-----------------|----------------|
| 1 | Transactions | 4 | Anshuman | abcd@abcd.com |
| 2 | Indexing  | 4 | Anshuman | abcd@abcd.com |
| 3 | Schema Design | 4 | Anshuman | abcd@abcd.com |
| 4 | SQL-1 | 6 | Ayush | ayush@abcd.com | 

This has the following problems:
 - Update problem: If name for Anshuman needs to be updated, it has to be updated in all 3 rows containing Anshuman. Missing even a single row causes inconsistency. 
 - Delete problem: If you delete the class #4, you end up loosing all infomation about the instructor Ayush. 
 - Insert problem: If a new instructor has been onboarded, there is no way to record their information. I cannot create a row with dummy entries. The only way to save their information is when they have a class assigned. 

Bad design. 
As you can see, if you start with bad design, it causes tons of issues around performance, data integrity in the future. If you design your schema well, 50% of the battle is won. Let's see principles used for good schema design. 

## Normalisation

Normalization is the process to eliminate data redundancy and enhance data integrity in the table. It is a systematic technique of decomposing tables to eliminate data redundancy (repetition) and undesirable characteristics like Insertion, Update, and Deletion anomalies.

To understand, if we are using the technique properly, various normalized forms are defined. Let's look at them one by one. 

### 1-NF

A table is referred to as being in its First Normal Form if atomicity of the table is 1.
Here, atomicity states that a single cell cannot hold multiple values. It must hold only a single-valued attribute.
The First normal form disallows the multi-valued attribute, composite attribute, and their combinations.

So, example 1 above is not in 1-NF form. 
However, if all your table columns contain atomic values, then your schema satisfies 1-NF form.

How do you solve example 1 to make it 1-NF? 
Create another table called tshirt_color and have a unique row for every tshirt-id, color combination. 

### 2-NF

A table is said to be in the second normal form if and only if:
 - The table is already in 1-NF form. 
 - If the proper subset of candidate key determines non-prime attribute, it is called partial dependency. A table should not have partial dependencies.

Let's see with an example (Example 2). 


| class_id | topic | instructor_id | instructor_name | Instructor_email |
|----------|-------|---------------|-----------------|----------------|
| 1 | Transactions | 4 | Anshuman | abcd@abcd.com |
| 2 | Indexing  | 4 | Anshuman | abcd@abcd.com |
| 3 | Schema Design | 4 | Anshuman | abcd@abcd.com |
| 4 | SQL-1 | 6 | Ayush | ayush@abcd.com | 

Here, instructor_name cannot alone decide the class_id or the topic or instructor_id. Various instructors could have the same name with different instructor ID. Hence, instructor_name is a non prime attribute. 
instructor_name can be derived from instructor_id which is a proper subset of the key (instructor_id alone cannot be the key). Hence, the above table violates 2-NF form. 

How do you solve to make it 2-NF? 
Only keep instructor_id in the table. Move all other instructor relalted parameters like instructor_name, instructor_email to another table where you have one entry for every unique instructor. 


## How to approach Schema Design

Let's learn about this using a familiar example. You are asked to build a software for Scaler which can handle some base requirements.

The requirements are as follows:
1. Scaler will have multiple batches.
2. For each batch, we need to store the name, start month and current instructor.
3. Each batch of Scaler will have multiple students.
4. Each batch has multiple classes.
5. For each class, store the name, date and time, instructor of the class.
6. For every student, we store their name, graduation year, University name, email, phone number. 
7. Every student has a buddy, who is also a student.
8. A student may move from one batch to another.
9. For each batch a student moves to, the date of starting is stored.
10. Every student has a mentor.
11. For every mentor, we store their name and current company name. 
12. Store information about all mentor sessions (time, duration, student, mentor, student rating, mentor rating).
13. For every batch, store if it is an Academy-batch or a DSML-batch.

Representation of schema doesn't matter. What matters is that you have all the tables needed to satisfy the requirements. Considering above requirements, how will you design a schema? Let's see the steps involved in creating the schema design.

Steps:
1. **Create the tables:** For this we need to identify the tables needed. To identify the tables,
    - Find all the nouns that are present in requirements.
    - For each noun, ask if you need to store data about that entity in your DB.
    - If yes, create the table; otherwise, move ahead.

    Here, such nouns are batches, instructors (if we just need to store instructor name then it will be a column in batches table. But if we need to store information about instructor then we need to make a separate table), students, classes, mentor, mentor session.
    
    Note that, a good convention about names:
Name of a table should be plural, because it is storing multiple values. Eg. 'mentor_sessions'. Name of a column is singular and in snake-case.

2. **Add primary key (id) and all the attributes** about that entity in all the tables created above.
    
    Expectation with the primary key is that:
    - It should rarely change. Because indexing is done on PK (primary key) and the data on disk is sorted according to PK. Hence, these are updated with every change in primary key.
    - It should ideally be a datatype which is easy to sort and has smaller size. Have a separate integer/big integer column called 'id' as a primary key. For eg. twitter's algorithm ([Snowflake](https://blog.twitter.com/engineering/en_us/a/2010/announcing-snowflake)) to generate the key (id) for every tweet.
    - A good convention to name keys is \<tablename>\<underscore>id. For example, 'batch_id'.

    Now, for writing attributes of each table, just see which attributes are of that entity itself. For `batches`, coulmns will be `name`, `start_month`. `current_instructor` will not be a column as we don't just want to store the name of current instructor but their details as well. So, it is not just one attribute, there will be a relation between `batches` and `instructors` table for this. So we will get these tables:

`batches`
| batch_id | name | start_month |
|----------|------|-------------|

`instructors`
| instructor_id | name | email | avg_rating |
|---------------|------|-------|------------|

`students`
| student_id | name | email | phone_number | grad_year | univ_name |
|------------|------|-------|--------------|-----------|-----------|

`classes`
| class_id | name | schedule_time |
|----------|------|---------------|

`mentors`
| mentor_id | name | company_name |
|-----------|------|--------------|

`mentor_sessions`
| mentor_session_id | time | duration | student_rating | mentor_rating |
|-------------------|------|----------|----------------|---------------|

3. **Representing relations:** For understanding this step, we need to look into cardinality.

## Cardinality

When two entities are related to each other, there is a questions: how many of one are related to how many of the other.

For example, for two tables students and batches, cardinality represents how many students are related to how many batches and vice versa.

- 1:1 cardinality means 1 student belongs to only 1 batch and 1 batch has only 1 students.
- 1:m cardinality means 1 student can belong to multiple batches and 1 batch has only 1 student.
- m:1 cardinality means 1 student belongs to only 1 batch and 1 batch can have multiple students.
- m:m cardinality means multiple students can belong to multiple batches, and vice versa.

In cardinality, `1` means an entity can be associated to 1 instance at max, [0, 1]. `m` means an entity can be associated with zero or more instances, [0, 1, 2, ... inf]

### Steps to calculate cardinality

If you want to calculate relationship between `noun1` and `noun2`, then you can do the following:
 - *Step 1:* If you take one example of `noun2`, how many noun1 are related to this example object. Output : Either `1` or `many`
 - *Step 2:* If you take one example of `noun1`, how many noun2 are related to this example object. Output : Either `1` or `many`
 
Take output from step1 (o1) and output from step2 (o2). o1:o2 is your relationship.

Let's take an example. 
What is the cardinality between employee and department. Assume that an employee can be part of only one department. 

 - Step 1: Example of department: Finance. How many employees can be part of Finance. Answer: **many**
 - Step 2: Example of employee: Sudhanshu. How many department can Sudhanshu be part of? Answer: **one**

So, answer = **many-to-one**

**Example 2:** What is the cardinality between ticket and seat in apps like bookMyShow? 

In one ticket, we can book multiple seats.
One seat can be booked in only 1 ticket.

So, the final cardinality between ticket and seat is **one-to-many**

**Example 3:**  Consider a monogamous community. What is the cardinality between husband and wife?

| husband | --- married to --- | wife |
| ------- | ------------------ | ---- |
| 1       | -->                | 1    |
| 1       | <--                | 1    |


In a monogamous community, 1 man is married to 1 woman and vice versa. Hence, the cardinality is **one-to-one**

**Example 4:** What is the cardinality between class and current instructor at Scaler?
Answer: many-to-one

## How to represent different cardinalities

When we have a 1:1 cardinality, the `id` column of any one relation can be used as an attribute in another relation. It is not suggested to include the both the respective `id` column of the two relations in each other because it may cause update anomaly in future transactions.

For 1:m and m:1 cardinalities, the `id` column of `1` side relation is included as an attribute in `m` side relation.

For m:m cardinalities, create a new table called a **mapping table** or **lookup table** which stores the ids of both tables according to their associations.

For example, for tables `orders` and `products` in previous quiz have m:m cardinality. So, we will create a new table `orders_products` to accomodate the relation between order ids and products ids.

`orders_products`
| order_id | product_id |
| -------- | ---------- |
| 1        | 1          |
| 1        | 2          |
| 1        | 3          |
| 2        | 2          |
| 2        | 4          |
| 3        | 1          |
| 3        | 5          |
| 4        | 5          |


We will cover case studies for the next class - applying the principles learnt. 



## Agenda

- Scaler Schema Design - continued
- Deciding Primary Keys of a mapping table
- Representing Foreign keys and indexes
- Case Study - Schema design of Netflix


## Steps to design schema 

Let's go over the steps to design schema one more time. 
1. Figure out entities. Nouns from the given requirements need to be split between entities and attributes. 
2. Figure out relationships. Based on cardinality, we decide the tables/columns needed. 
3. Do we see attributes that should be enum instead? [Described later in the notes]
4. Find out the primary keys in every table. Add foreign key wherever applicable. 
5. Find out common query patterns and build index on them. Keep iterating as you discover more frequent use cases. 


## Scaler Schema Design

For reference from previous class, Scaler Schema Design:

The requirements are as follows:
1. Scaler will have multiple batches.
2. For each batch, we need to store the name, start month and current instructor.
3. Each batch of Scaler will have multiple students.
4. Each batch has multiple classes.
5. For each class, store the name, date and time, instructor of the class.
6. For every student, we store their name, graduation year, University name, email, phone number. 
7. Every student has a buddy, who is also a student.
8. A student may move from one batch to another.
9. For each batch a student moves to, the date of starting is stored.
10. Every student has a mentor.
11. For every mentor, we store their name and current company name. 
12. Store information about all mentor sessions (time, duration, student, mentor, student rating, mentor rating).
13. For every batch, store if it is an Academy-batch or a DSML-batch.

## Step 1: Find entities (Nouns)

Let's use the above description to list out entities (nouns)
1. batches (attributes: name, start month)
2. instructors (name)
3. students (name, graduationYear, universityName, email, phoneNumber)
4. classes (name, date, time)
5. mentor (name, currentCompanyName)
6. mentor_sessions (time, duration, student_rating, mentor_rating)

Quick note here:
 - Not all nouns become entities. 
 - For example, name is a noun. But it's an attribute of a class and not a separate entity in itself. 

## Step 2: Relationships

1. Point number 2 in the requirement tells us there is a relationship between batch and current instructor. 
    Cardinality: m:1 
    Hence, we add current_instructor_id column to batches table. 

2. Point number 3 tells us that each batch can have multiple students. And a student is in one batch at a time. They can move, but at a time, they are exactly in one batch. So, there is a relationship between batch and students. 
    Cardinality: 1:m 
    Hence, we can add batch_id as a column in students table.
However, here comes the tricky part. Imagine, I want to track all dates when the student moved. Which means the relationship becomes many:many (current + historical batches). I might still have the batch_id in students table to indicate current batch, but I will need a separate table to maintain all historical batches along with their move date. 
When a student is moved from one batch to another, this date is an attribute of the relation between `students` and `batches`. So, we will create a new table like this:

`student_batches`

| student_id | batch_id | move_date |
|------------|----------|-----------|

As we have included `batch_id` here, we can remove it from `students` table but that will decrease the performance because everytime we will have to query on this new table also. So, for ease, we will keep the `batch_id` in `students` also.

3. Point number 4 tells us that each batch has multiple classes. Whether a class only has one batch or multiple batches is not specified. Let's assume, that we want the ability to have multiple batches attend a class. 
    Cardinality: m:m
    We will need a separate batch_classes table. 

4. Point number 5 tells us there is a relationship between classes and instructor. What is the cardinality between `class` and `instructor`. As this is m:1 cardinality, instructor_id will be included in `classes`.

5. Point number 7 tells us that every student has a buddy. 
Here, the cardinality of the buddy relation between a student and another student is m:1. 

| student | --- buddy --- | student |
| ------- | ------------- | ------- |
| 1       | -->           | 1       |
| m       | <--           | 1       |  > 

So, the `students` table will have one more column called `buddy_id`.

6. Point number 10 tells us that there is a relationship between student and mentor. A student has one mentor, but a mentor can have many students. 
   Cardinality: m:1
So, we will include mentor_id as a column in the students table. 

7. Finally, point number 12 tells us mentor_sessions has a relationship with `mentors` and `students`. 
    Cardinality between `mentor_sessions` and `students` : m:1
    Cardinality between `mentor_sessions` and `mentors`  : m:1
    So, we add `student_id` and `mentor_id` columns to `mentor_sessions` table. 

**Hence, the final table structure after step 1 and 2:**

`batches`

| batch_id | name | start_month | curr_inst_id |
|----------|------|-------------|--------------|

`instructors`
| instructor_id | name |
| ------------- | ---- | 

`classes`

| class_id | name | schedule_time | instructor_id |
|----------|------|---------------| ------------- |

`batch_classes`

| batch_id | class_id |
| -------- | -------- | 

`student_batches`

| student_id | batch_id | move_date |
|------------|----------|-----------|

`students`

| student_id | name | email | phone_number | grad_year | univ_name | batch_id | buddy_id | mentor_id |
|------------|------|-------|--------------|-----------|-----------|----------| -------- | --------- |

`mentors`

| mentor_id | name | currentCompanyName |
|-----------|------|--------------------|

`mentor_sessions`

| mentor_session_id | time | duration | student_rating | mentor_rating | student_id | mentor_id |
|-------------------|------|----------|----------------|---------------| ---------- | --------- |

## Step 3: Identify Enums

Now, for the batch type, it can be DSML or Academy. Here, the batch type is enum (enum represents one of the given fixed set of values). 

Eg: 
```
enum Gender{
    male,
    female
};
```

So, we will have a `batch_types` table. 

`batch_types`

| id | value |
| -- | ----- |

Cardinality between `batches` and `batch_types` will be m:1. In `batches` table we will have `batch_type_id`.

`batches`

| batch_id | name | start_month | curr_inst_id | batch_type_id |
|----------|------|-------------|--------------| ------------- |

### How to represent enum

1. Using strings
    Cons: The problem in storing enums this way is that it will take a lot of space. It will have slow string comparison.

    Pros: Readability. No joins are required.

    `batches`

    | batch_id | name | type    |
    | -------- | ---- | ------- |
    | 1        | b1   | DSML    |
    | 2        | b2   | Academy |
    | 3        | b3   | Academy |
    | 4        | b4   | DSML    |

2. Using integers
    Here, 0 means DSML type batch and 1 means Academy type batch.
    
    Cons: No readability. We can not add or delete values (enums) in between as it will cause discrepencies. Also, what a particular value represents is not in the database.

    `batches`

    | batch_id | name | type_id |
    | -------- | ---- | ------- |
    | 1        | b1   | 0       |
    | 2        | b2   | 1       |
    | 3        | b3   | 1       |
    | 4        | b4   | 0       |

3. Lookup table
    It will have id and value columns where each type is stored as separate. The `type_id` of `batches` will refer to the `id` column of `batch_types`. All the above cons are solved with this method. 
    
    **batch_types**
    
    | id | value      |
    | -- | ---------- | 
    | 1  | Academy    |
    | 2  | DSML       | 
    | 3  | Neovarsity |
    | 4  | SST        |
    
So, the best way to represent enums is to use lookup table.


## Step 4: Deciding Primary Keys of a mapping table
    
### Example from previous discussion:

For `student_batches` the primary key will be (student_id, batch_id).

`student_batches`

| student_id | batch_id | move_date |
|------------|----------|-----------|

If in case we have our table like this, the primary key will be `id`. Size of index will be lesser here. 

`student_batches`

| id | student_id | batch_id | move_date |
| -- |------------|----------|-----------|

### Example 2
1. Scaler has exams.
2. For each batch a student joins, they will have to take exams of that batch.
3. Each exam is associated to a batch.

`exams`

| id | name | start_date | end_date   |
| -- | ---- | ---------- | ---------- |

Between batch and exam, each exam is associated to a batch, we will have to create a mapping table. One batch can have multiple exams, One exam can be present fo multiple batches. 

`exam_batches`

| exam_id | batch_id |
| ------- | -------- |

Similarly we also have a table called `student_batches`.

`student_batches`

| student_id | batch_id | date |
|------------|----------|------|

To figure out which student went through which exams, we will need to join `student_batches` with `exam_batches`. Basically, we are forming a relation between two mapping tables.

### Example 3

1. One student can belong to multiple batches.
2. Every batch has exams.
3. Same exam may happen on different batches on different dates.
4. If a students moves the batch, they may have to give some exams again.

`student_batches`

| student_id | batch_id | date |
|------------|----------|------|

Cardinality between batches ad exams is m:m. So, we will have a `batch_exams` table. Date is also an attribute of this relation.

`batch_exams`

| batch_id | exam_id | date |
| -------- | ------- | ---- |

Between students and exams also the cardinality is m:m. But if we have (student_id, exam_id) as primary key of the new `student_exams` table, it will not allow one student to take a particular exam twice. So, we will have to add `batch_id` also in PK. The below `student_batch_exams` will be our new table.

`student_batch_exams`

| student_id | batch_id | exam_id | marks |
| ---------- | -------- | ------- | ----- | 

Hence, we can see that sometimes a mapping may also have a relation with another entity. In these cases, not having a primary key can cause problems. 

**Advantages of a separate key:**
If a relation is being mapped to another entity or relation, it saves space.

**Advantages of NO separate key:**
Queries on first column will become faster because the table will be sorted by that column. A mapping table is often used for relationships and thus will require joins. Having no separate key makes things faster.

## Step 5: Representing Foreign keys and indexes

There are 2 steps here. First establishing foreign key relationships and then indexes for frequent use-cases. 

### Step 5.1: Foreign Keys

Typically, when you have a relationship table, which exists because there is a relationship between entity1 and entity2, then it's usually recommended to have a foreign key relationship between the relationship table and the entity it references. 

For example, consider the following table which exists due to m:m cardinality relationship between `batches` and `classes`. 

`batch_classes`

| batch_id | class_id |
| -------- | -------- | 

If we expect that whenever we query this table, we will need to get the associated batch and class details (which is almost always the case), then it makes sense to have a foreign key relationship with `batches` and `classes` table. 

```sql
ALTER TABLE batch_classes ADD CONSTRAINT fk_batch FOREIGN KEY (batch_id) REFERENCES batches(batch_id);
ALTER TABLE batch_classes ADD CONSTRAINT fk_class FOREIGN KEY (class_id) REFERENCES classes(class_id);
```

Very similarily, all other relationships we discussed in step 2, are eligible for a foreign key constraint. 

*Note that however, it is not mandatory to specify foreign key relationships. Foreign key relationships help with data consistency - so, incase you expect that the column I am referring to, must be unique - then specifying a foreign key constraint will enforce that (MySQL automatically then creates an index on that column - the foreign table column -  unless one already exists).*

### Step 5.2: Identify Indexes

The second step is to list down the frequent use-cases and explore if the queries I have to write for the frequent use-cases - are they fast or not? 
If they are not, then it warrants creating an index to avoid full table scans. 

Let's say that the learners often search mentor by a name. This is a use case. On which column of which table will you create an index for this? You have to create an index on `name` column of `mentors` table.

`mentors`
| mentor_id | name | company_name |
|-----------|------|--------------|

As a rule of thumb, given a query, look at the join conditions and where condition, followed by Order by with limit. If your query is slow, creating an index on those columns helps. **Please refer to the quizzes done during the class to understand this better.**

After drawing the complete Schema, mention the indexes.
This was all about Schema Design!

## Case Study - Netflix Schema Design

Let's go over the problem statement first. 

[Netflix Schema Design](https://docs.google.com/document/d/1xQbcv-smnV_JY6NUb4gz2owwPaQMWdoWty6PZyFEsq8/edit?usp=sharing)

**Problem Statement**
Design Database Schema for a system like Netflix with following Use Cases.
**Use Cases**
1. Netflix has users.
2. Every user has an email and a password.
3. Users can create profiles to have separate independent environments.
4. Each profile has a name and a type. Type can be KID or ADULT.
5. There are multiple videos on netflix.
6. For each video, there will be a title, description and a cast.
7. A cast is a list of actors who were a part of the video. For each actor we need to know their name and list of videos they were a part of.
8. For every video, for any profile who watched that video, we need to know the status (COMPLETED/ IN PROGRESS).
9. For every profile for whom a video is in progress, we want to know their last watch timestamp.

Let's approach this problem as one should in an interview.

1. Finding all the nouns to create tables.

- `users` 
- `profiles`
- `videos`
- `actors` (cast is nothing but a mapping between videos and actors)

1.2. Enums:

- `profile_type` (lookup table)
- `watch_status_type` (enum, it is an attribute of relation between profile and videos)

1.3. Finding attributes of particular entites.
    
    `users`
    | id | email | password |
    | -- | ----- | -------- |
    
    `profiles`
    | id | name | 
    | -- | ---- |
    
    `profile_type`
    | id | value | 
    | -- | ----- |
    
    `videos`
    | id | name | description |
    | -- | ---- | ----------- |
    
    `actors`
    | id | name | 
    | -- | ---- |
    
    `watch_status_type`
    | id | value | 
    | -- | ----- |
    
2. Representing relationships.

    Now, there are no relationships in the first and second use cases. Moving forward, what is the cardinality between `users` and `profiles`? One user can have multiple profiles but one profile is associated with one user. Therefore, it is 1:m, id of user will be in `profiles` table.
    
    `profiles`
    | id | name | user_id |
    | -- | ---- | ------- |
    
    What is the cardinality between `profiles` and `profile_type`? It is m:1, `profiles` will have another column `profile_type_id`.
    
    `profiles`
    | id | name | user_id | profile_type_id |
    | -- | ---- | ------- | --------------- |
    
    What is the cardinality between `videos` and `actors`? One video can have multiple actors and one actor could be in multiple videos. So, it is m:m. 
    
    `video_actors`
    | video_id | actor_id | 
    | -------- | -------- |
    
    Status is an information about relation between `videos` and `profiles`. Hence, a new table is created. Last watch timestamp is also an attribute on these two.
    
    `video_profiles`
    | video_id | profile_id | watch_status_type_id | last_watched_ts |
    | -------- | ---------- | -------------------- | --------------- |

3. Enum is already done in step 1.2.

4. Let's identify primary key for every table. 

 - users : new column `id`
 - profiles: new column `id`
 - profile_type: new column `id`
 - videos: new column `id`
 - actors: new column `id`
 - video_actors: (video_id, actor_id)
 - video_profiles: (profile_id, video_id)
 - watch_status: new column `id`

5. Indexes required. 

 - Use case 1: Log IN. 

```sql
SELECT password FROM users WHERE email = xyz
```

Index on `email` in `users`

 - Get all profiles for a given user

```sql
SELECT id, name, profile_type_id FROM profiles WHERE user_id = xyz 
```

Index on `user_id` in `profiles`

 - Recently played videos

```sql
SELECT video_id FROM video_profiles WHERE profile_id = xyz AND watch_status = 2 ORDER BY last_watched_ts DESC LIMIT 10
```

Index on (profile_id, watch_status)


And so on. 


## Agenda

 - Views 
 - Window function

## Views

Imagine in sakillaDB, I frequently have queries of the following type:
 - Given an actor, give me the name of all films they have acted in. 
 - Given a film, give me the name of all actors who have acted in it. 

Getting the above requires a join across 3 tables, `film`, `film_actor` and `actor`. 

Why is that an issue?
 - Writing these queries time after time is cumbersome. Infact imagine queries that are even more complex - requiring joins across a lot of tables with complex conditions. Writing those everytime with 100% accuracy is difficult and time-taking. 
 - Not every team would understand the schema really well to pull data with ease. And understanding the entire schema for a large, complicated system would be hard and would slow down teams. 

So, what's the solution? 
Databases allow for creation of views. Think of views as an alias which when referred is replaced by the query you store with the view.

So, a query like the following:

```sql
CREATE OR REPLACE view actor_film_name AS

SELECT
   concat(a.first_name, a.last_name) AS actor_name,
   f.title AS file_name
FROM actor a
  JOIN film_actor fa 
    ON fa.actor_id = a.actor_id 
  JOIN film f
    ON f.film_id = fa.film_id
```


**Note that a view is not a table.** It runs the query on the go, and hence data redundancy is not a problem. 

### Operating with views

Once a view is created, you can use it in queries like a table. Note that in background the view is replaced by the query itself with view name as alias. 
Let's see with an example. 

```sql
SELECT film_name FROM
actor_film_name WHERE actor_name = "JOE SWANK"
```

OR 

```sql
SELECT actor_name FROM
actor_file_name WHERE film_name = "AGENT TRUMAN"
```

If you see, with views it's super simple to write queries that I write frequently. Lesser chances to make an error.
Note that however, actor_file_name above is not a separate table but more of an alias.

An easy way to understand that is that assume every occurrence of `actor_file_name` is replaced by

```sql
(SELECT
   concat(a.first_name, a.last_name) AS actor_name,
   f.title AS file_name
FROM actor a
  JOIN film_actor fa 
    ON fa.actor_id = a.actor_id 
  JOIN film f
    ON f.film_id = fa.film_id) AS actor_file_name
```

**Caveat:** Certain DBMS natively support materialised views. Materialised views are views with a difference that the views also store results of the query. This means there is redundancy and can lead to inconsistency / performance concerns with too many views. But it helps drastically improve the performance of queries using views. MySQL for example does not support materialised views. Materialised views are tricky and should not be created unless absolutely necessary for
performance. 

#### How to best leverage views

Imagine there is an enterprise team at Scaler which helps with placements of the students. 
Should they learn about the entire Scaler schema? Not really. They are only concerned with student details, their resume, Module wise PSP, Module wise Mock Interview clearance, companies details and student status in the companies where they have applied.  

In such a case, can we create views which gets all of the information in 1 or 2 tables? If we can, then they need to only understand those 2 tables and can work with that. 

#### More operations on views

**How to get all views in the database:**

```sql
SHOW FULL TABLES WHERE table_type = 'VIEW';
```

**Dropping a view** 

```sql
DROP VIEW actor_file_name;
```

**Updating a view**

```sql
ALTER view actor_film_name AS

 SELECT
    concat(a.first_name, a.last_name) AS actor_name,
    f.title AS file_name
 FROM actor a
   JOIN film_actor fa
     ON fa.actor_id = a.actor_id
   JOIN film f
     ON f.film_id = fa.film_id
```

**Note:** Not recommended to run update on views to update the data in the underlying tables. Best practice to use views for reading information. 

**See the original create statement for a view**

```sql
SHOW CREATE TABLE actor_film_name
```

## Window Function

Imagine you have an `employees` table with the following columns. 

```sql
employees
emp_no    |  department  | salary
  1       |   Tech       | 60,000
  2       |   Tech       | 50,000
  3       |    HR        | 40,000
  4       |    HR        | 60,000
```

If I ask you to fetch the average salary for every department, what would you do? 
Yes, you would use a group_by to fetch the avg salary in a department. 

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
```

which will print 

```
department  |  AVG(salary)
 Tech       |   55000
 HR         |   50000
```

However, what if I ask you to print every row in the employees table along with the avg salary of the department. 
You can use WINDOW function for that. Window function is exactly like group by, just that it prints it's output for every row. 

**Syntax:**

```sql
SELECT 
  emp_no, 
  department, 
  salary,
  AVG(salary) OVER (PARTITION BY department) AS dept_avg
FROM employees
```

The term `OVER` indicates that I am using a window function. 
Just like group by, window function would need to define what is a group like. For that, it uses PARTITION BY. `PARTITION BY department` creates 2 groups/windows - one for Tech, one for HR. 
In each group, you calculate the aggregate function specified before `OVER`.

So, the above query yields:

```sql
employees
emp_no    |  department  | salary | dept_avg
  1       |   Tech       | 60,000 |  55000
  2       |   Tech       | 50,000 |  55000
  3       |    HR        | 40,000 |  50000
  4       |    HR        | 60,000 |  50000
```

What happens if there is no Partition by? What's the group then?
Correct. The entire table becomes the group. 

So, the following query:

```sql
SELECT 
  emp_no, 
  department, 
  salary,
  AVG(salary) OVER () AS dept_avg
FROM employees
```

yields


```sql
employees
emp_no    |  department  | salary | dept_avg
  1       |   Tech       | 60,000 |  52500
  2       |   Tech       | 50,000 |  52500
  3       |    HR        | 40,000 |  52500
  4       |    HR        | 60,000 |  52500
```

You can have multiple window function in the same SQL statement. For example, how do I print MAX, MIN and AVG salary in every department along with the employee? 

```sql
SELECT 
  emp_no, 
  department, 
  salary,
  AVG(salary) OVER (PARTITION BY department) AS dept_avg,
  MAX(salary) OVER (PARTITION BY department) AS dept_max,
  MIN(salary) OVER (PARTITION BY department) AS dept_min
FROM employees
```

This would yield:

```sql
employees
emp_no    |  department  | salary | dept_avg | dept_max | dept_min 
  1       |   Tech       | 60,000 |  55000   |  60000   | 50000
  2       |   Tech       | 50,000 |  55000   |  60000   | 50000
  3       |    HR        | 40,000 |  50000   |  60000   | 40000
  4       |    HR        | 60,000 |  50000   |  60000   | 40000
```

*You can have multiple window functions with different partition by in a SQL query. Just that it would do more work - twice as expensive. It would create different groups / windows in parallel and then calculate the aggregate value.*

Window function also allows you to order entries in a certain order within a group / partition / window. For example, if I wanted that within a single department, entries are sorted based on salary in descending order, I can write:


```sql
SELECT 
  emp_no, 
  department, 
  salary,
  AVG(salary) OVER (PARTITION BY department ORDER BY salary DESC) AS dept_avg
FROM employees
```

which would yield:

```sql
employees
emp_no    |  department  | salary | dept_avg
  1       |   Tech       | 60,000 |  55000
  2       |   Tech       | 50,000 |  55000
  4       |    HR        | 60,000 |  50000
  3       |    HR        | 40,000 |  50000
```

### Aggregate function which work only with Window function. 

**RANK()** - Gives the rank of every entry in the group/window/partition it belongs to. It is recommended to specify a order by clause in window function when using rank(). Ranking is done based on the ordering of entries within a partitio. 
Imagine I wanted to print all employees along with their department rank based on salary. 

```sql
SELECT 
  emp_no, 
  department, 
  salary,
  RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS dept_rank
FROM employees
```

which yields


```sql
employees
emp_no    |  department  | salary | dept_rank
  1       |   Tech       | 60,000 |  1
  2       |   Tech       | 50,000 |  2
  4       |    HR        | 60,000 |  1
  3       |    HR        | 40,000 |  2
```

In the absence of partition by, the entire table becomes one large group and hence salaries are ranked in the entire company. 

```sql
SELECT 
  emp_no, 
  department, 
  salary,
  RANK() OVER (ORDER BY salary DESC) AS company_rank
FROM employees
```

yields


```sql
employees
emp_no    |  department  | salary | company_rank
  1       |   Tech       | 60,000 |  1
  4       |    HR        | 60,000 |  1
  2       |   Tech       | 50,000 |  3
  3       |    HR        | 40,000 |  4
```

Note that 2 entries with the same salary got the same rank. How do I know that I need to compare salaries (because that's whats specified in order by clause). Conflicting entries get the same rank. And next entry (after the duplicate/conflicting entries) gets a number which it would have gotten had the entries been different. 
If you want the next entry to get the next natural number, then you can use the **dense_rank()** function which works exactly like the rank() function with the only difference being how the next entry is assigned a rank in case of duplicate values. 

**DENSE_RANK()** - Explained above. 

**ROW_NUMBER()** - Imagine in the above rank() example, you don't want same ranks assigned to entries with the same value. In that case, you can use row_number(). 

```sql
SELECT 
  emp_no, 
  department, 
  salary,
  ROW_NUMBER() OVER (ORDER BY salary DESC) AS company_rank
FROM employees
```

yields

```sql
employees
emp_no    |  department  | salary | company_rank
  1       |   Tech       | 60,000 |  1
  4       |    HR        | 60,000 |  2
  2       |   Tech       | 50,000 |  3
  3       |    HR        | 40,000 |  4
```


**LAG(column) / LEAD(column)**: Imagine in the above context, I wanted to print the value from the previous row in the group, or the next row in the group, then I use the lead or lag functions.
LAG(column) - As the name indicates, it prints the column value from the previous row in the group. 
LEAD(column) - column value from the next row in the group. 
For example, what if I wanted to print the next higher salary than me in the department (or the next lower) along with my rank. 

```sql
SELECT 
  emp_no, 
  department, 
  salary,
  RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS dept_rank,
  LAG(salary) OVER (PARTITION BY department ORDER BY salary DESC) AS next_higher_salary
FROM employees
```

yields 

```sql
employees
emp_no    |  department  | salary | dept_rank | next_higher_salary
  1       |   Tech       | 60,000 |  1        |  NULL
  2       |   Tech       | 50,000 |  2        |  60000
  4       |    HR        | 60,000 |  1        |  NULL
  3       |    HR        | 40,000 |  2        |  60000
```
