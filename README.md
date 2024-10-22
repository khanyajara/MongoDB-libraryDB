Project Title: Library Management System

Objective: Create a Library Management System to manage a collection of books, authors, and patrons.


Instructions:



First initialise your mongo shell, type in the following on your cmd terminal:

mongosh

Create Database LibraryDB

To create a Library database or switch to it type in the following command in your cmd : 

use LibraryDB


Create Collections 
To create collections type in the following commands :

db.createCollection("Books")
db.createCollection("Authors")
db.createCollection("Patrons")

Insert Documents (Insert multiple documents using insertMany method)

TO insert documents we usually type in "insertOne" but in this case we type in the following:


for Book colllection

db.Books.insertMany([ { _id: 1, title: "1984", author_id: 1, genres: ["Dystopian", "Political Fiction"], published_year: 1949, available: true }, { _id: 2, title: "To Kill a Mockingbird", author_id: 2, genres: ["Southern Gothic", "Bildungsroman"], published_year: 1960, available: true }, { _id: 3, title: "The Great Gatsby", author_id: 3, genres: ["Tragedy"], published_year: 1925, available: true }, { _id: 4, title: "Brave New World", author_id: 4, genres: ["Dystopian", "Science Fiction"], published_year: 1932, available: true }, { _id: 5, title: "The Catcher in the Rye", author_id: 5, genres: ["Realist Novel", "Bildungsroman"], published_year: 1951, available: true }, { _id: 6, title: "Moby-Dick", author_id: 6, genres: ["Adventure Fiction"], published_year: 1851, available: true }, { _id: 7, title: "Pride and Prejudice", author_id: 7, genres: ["Romantic Novel"], published_year: 1813, available: true }, { _id: 8, title: "War and Peace", author_id: 8, genres: ["Historical Novel"], published_year: 1869, available: true }, { _id: 9, title: "Crime and Punishment", author_id: 9, genres: ["Philosophical Novel"], published_year: 1866, available: true }, { _id: 10, title: "The Hobbit", author_id: 10, genres: ["Fantasy"], published_year: 1937, available: true } ])


This should return something like this :

{
  acknowledged: true,
  insertedIds: {
    '0': 1,
    '1': 2,
    '2': 3,
    '3': 4,
    '4': 5,
    '5': 6,
    '6': 7,
    '7': 8,
    '8': 9,
    '9': 10
  }
}
 to check all the add Books type in :

 db.Books.find()

 if you are looking for a specific book then type in :
 db.Books.find({title:'The Hobbit'})



 Find All Books by a Specific Author (author_id: 5)  type in the following command:
 db.Books.find({author_id: 5})

[
  {
    _id: 5,
    title: 'The Catcher in the Rye',
    author_id: 5,
    genres: [ 'Realist Novel', 'Bildungsroman' ],
    published_year: 1951,
    available: true
  }
]

Find All Available Books, type in the following command:


 db.Books.find({available:true})




for Authors collection 

type in the following command:

db.Authors.insertMany  ([ { _id: 1, name: "George Orwell", nationality: "British", birth_year: 1903, death_year: 1950 }, { _id: 2, name: "Harper Lee", nationality: "American", birth_year: 1926, death_year: 2016 }, { _id: 3, name: "F. Scott Fitzgerald", nationality: "American", birth_year: 1896, death_year: 1940 }, { _id: 4, name: "Aldous Huxley", nationality: "British", birth_year: 1894, death_year: 1963 }, { _id: 5, name: "J.D. Salinger", nationality: "American", birth_year: 1919, death_year: 2010 }, { _id: 6, name: "Herman Melville", nationality: "American", birth_year: 1819, death_year: 1891 }, { _id: 7, name: "Jane Austen", nationality: "British", birth_year: 1775, death_year: 1817 }, { _id: 8, name: "Leo Tolstoy", nationality: "Russian", birth_year: 1828, death_year: 1910 }, { _id: 9, name: "Fyodor Dostoevsky", nationality: "Russian", birth_year: 1821, death_year: 1881 }, { _id: 10, name: "J.R.R. Tolkien", nationality: "British", birth_year: 1892, death_year: 1973 } ])

This should return something like this :

{
  acknowledged: true,
  insertedIds: {
    '0': 1,
    '1': 2,
    '2': 3,
    '3': 4,
    '4': 5,
    '5': 6,
    '6': 7,
    '7': 8,
    '8': 9,
    '9': 10
  }
}


Patrons Collections  

please type in the following command: 

db.Patrons.insertMany([ { _id: 1, name: "Alice Johnson", email: "alice@example.com", borrowed_books: [] }, { _id: 2, name: "Bob Smith", email: "bob@example.com", borrowed_books: [1, 2] }, { _id: 3, name: "Carol White", email: "carol@example.com", borrowed_books: [] }, { _id: 4, name: "David Brown", email: "david@example.com", borrowed_books: [3] }, { _id: 5, name: "Eve Davis", email: "eve@example.com", borrowed_books: [] }, { _id: 6, name: "Frank Moore", email: "frank@example.com", borrowed_books: [4, 5] }, { _id: 7, name: "Grace Miller", email: "grace@example.com", borrowed_books: [] }, { _id: 8, name: "Hank Wilson", email: "hank@example.com", borrowed_books: [6] }, { _id: 9, name: "Ivy Taylor", email: "ivy@example.com", borrowed_books: [] }, { _id: 10, name: "Jack Anderson", email: "jack@example.com", borrowed_books: [7, 8] } ])

This should return something like this :

{
  acknowledged: true,
  insertedIds: {
    '0': 1,
    '1': 2,
    '2': 3,
    '3': 4,
    '4': 5,
    '5': 6,
    '6': 7,
    '7': 8,
    '8': 9,
    '9': 10
  }
}


UPDATE

Update Book Availability (Using $set), mark a book (_id: 3 as borrowed.)

Please type in the following command to update book Status:
db.Books.updateOne({_id: 3}, {$set: {Status:"Borrowed", available: false}})


Add a Genre to a Book (using $addToSet)(_id:8)

to add another Genre to a book , type in the following command:
 db.Books.updateOne({_id:8}, {$addToSet: {genres:['Strategy']}})

 or 

  db.Books.updateOne({_id:8}, {$addToSet: {genres:'Strategy'}})  without the "[]"


Add a borrowed book to a patron’s record (_id: 5)
first find all Patrons, type in :
db.Patrons.find()

then to update patrons borrowed book record , type in this command:
db.Patrons.updateOne({_id: 5}, {$set: {borrowed_books: [5]}})



DELETE

Delete a Book by Title (title: "Brave New World”)

To delete a book by Title , type in the following comand:
 db.Books.deleteOne({title:'Brave New World'})

if you are successful with delete, you will recieve this :
{ acknowledged: true, deletedCount: 1 }

Delete an Author (_id: 3)
lets first find all Authors to confirm the one we'll delete , type in :
db.Authors.find()

now that you see the list , type in the following to delete the specific Author by _id

db.Authors.deleteOne({_id: 5})


this will show you this :

{ acknowledged: true, deletedCount: 1 }





Advanced Queries with Operators

Find Books Published After 1950 (Using $gt)
type in the following command:


 db.Books.find( {published_year: {$gt:1950}})



Find All American Authors (Using $eq)
type in the following :

 db.Authors.find({nationality: {$eq:'American'}})

Set All Books To Available (Using $set)

to set all books to available , then type the following:
db.Books.updateMany({}, {$set: {available: true}})


Find All Books That Are Available And Published After 1950

 db.Books.find({available:true},{ published_year:1950})"#MongoDB-libraryDB" 
