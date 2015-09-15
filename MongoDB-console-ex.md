####Terms

Database- a structured set of data held in a computer, especially one that is accessible in various ways.

Collection- A collection is made up of socuments. They can be indexed, which improves lookup and sorting performance.

Document- Made up of zero or more fields. This can safetly be thought of as a row.

Cursor- This is the primary method for the read operation. When you ask Mongo for data, it returns a pointer to the result set called a cursor, which we can do things to, such as counting or skipping ahead, before actually pulling data.

Field- Fields are contianed within documents. They are made up of key value pairs.

CRUD- Create, Read, Update, Delete

Relational Database- The model of DB orginizes data into one or more tables, or relation of columns and rows, with unique keys for each row. A relationship exists amoung the columns within the table and moung the tables. These type of databases fall into the category called, SQL.

Non-Relational Database- Type of database that falls into the category called, NoSQL. A collection of key value pairs, graph DB, or wide-column stores.

CAP Theorem- A therom that states that it is impossible for a distributed system to simultaneously provide all three of the following: **consistency**(all nodes see the same data at the same time), **availability**(a garuntee that every request recieves a response about whether it succeded or failed), and partition **tolerence**(the system continues to operate despite arbitrary partitioning due to network failures.).

Schema-A DB schema is a way to logically group objects such as tables, views, stored data, etc. Think of schema as a contianer of objects.

#### Questions

Do MongoDB databases have schemas?

Yes, it uses dynamic schemas. You can create collections without defining the structure, the fields, or the type of values.

What are typical uses for MongoDB?

MongoBD's flexible schema makes it particularly well suited for strong information for product data mangement and e-commerce websites and solutions.

MongoDB's fundamental practices and approaches, using familiar problems and simple examples, makes it a good use case for content management systems.

What is Mongoose?

A wonderful tool that we use on top of mongo, which allows us to mongo in express

What is a Mongoose Model?

Models are fancy constructors from our `Schema` definitions. Instances of these models represent documents which can be save and retrieved from our database. All document creation and retrieved from the database is hanfeled by these models.

####Challenges

1. Write the terminal command to start the mongo server

		mongod

2. Write the terminal command to enter a mongo shell
	
		mongo
	
	Make sure to open a new terminal window, not to interfere with the mongo server.
	
3. Show all databases

		show dbs
		
		db.adminCommand('listDatabases')
		
		db.getMongo().getDBNames()

4. Use the library database

		use library
		
5. Show all the collections inside the library database

		db.getCollectionNames()
		
		show collections


6. Using the insert method Add an author with the name of "John", age of 37

		db.authors.insert({name: "John",
		age: "37"
		});


7. Using the insert method Add another author with the name of "Jane", age of 42 and give her a property of books which is an empty array.
		
		db.authors.insert({name: "Jane",
		age: "42",
		books:[]
		});

8. Use findOne to select an author with an age greater than or equal to 42. Change that authors age to 33, then use the save method to persist the change.

		var jane = db.authors.findOne({age:			{$gte:"42"}})
		jane.age = 33
		db.authors.save(jane)


9. Find all of the authors

		db.authors.find()


10. Find an author with the name of John

		db.authors.find({
		name: "John"
		})

11. Find all of the authors but limit the search to one

		db.authors.find().limit(1)

12. Find an author whose name is not equal to "John" using the $ne operator

		db.authors.find({
		name: {$ne: "John"}
		})

13. Update an author who has a name of "John" and change his name to "James" (without using the set method)

		db.authors.update({name:"John"},		
		{name:"James"},{upsert:true})

14. Update an author named "James" and using the set operator, set his name back to John and age to 37.

		db.authors.update({name:"James"},{$set			{name:"Jack"",age:"37"}})
	
15. Delete an author whose name is "John"
	
		db.authors.remove({name:"John"})

16. Delete all of the authors

		db.authors.remove()

17. Create an author whose name is "John" and has an empty array of books
	
		db.authors.insert({
		name:"John",
		books:[]
		});

18. Update John and Using the $push operator add the string "Of Mice and Men" into the books array.

		 db.authors.update({name:"John"},{$push:	     {books:"Of Mice and Men"}});

19. Update John and using the $push and $each operators add the strings "Grapes of Wrath", "The Pearl", "East of Eden", "50 Shades of Gray" into the books array.

		db.authors.update({name:"John"},{$push:		{books:	{$each:["The Pearl", "East of Eden", 		"50 Shades of Gray"]}}})

20. Sorry - John Steinbeck didn't write 50 Shades of Gray, using the $pull operator, remove that book from the array.

		db.authors.update({name:"John"},{$pull:		{books:"50 	Shades of Gray"}})
	
21. Finally, using the $in operator, update an author who has a book "Of Mice and Men" or "The Pearl" in the books array and change their name to "John Steinbeck"

	
		db.authors.update({books:{$in:["Of Mice and 		Men", "The Pearl"]},{$set:{name:"John 			Steinbeck"}})