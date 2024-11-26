# Library Management System using MongoDB

This project outlines the implementation of a **Library Management System** using the MongoDB shell (`mongosh`). It demonstrates database creation, collections setup, CRUD operations, and advanced queries.

## Features
- **Database Name:** LibraryDB
- **Collections:**
  - `Books`: Manages book details.
  - `Authors`: Stores information about authors.
  - `Patrons`: Keeps track of library patrons.
- **Commands Included:**
  - Create a database and collections.
  - Insert multiple documents using `insertMany`.
  - Perform CRUD operations.
  - Execute advanced MongoDB queries.

---

## Prerequisites
1. **Install MongoDB**: Download MongoDB from [here](https://www.mongodb.com/try/download/community).
2. **Install and Configure Mongosh**: Ensure `mongosh` is installed and accessible in your terminal.
3. **Start MongoDB server**:
   ```bash
   mongod
   ```

---

## Step-by-Step Guide

### 1. Start MongoDB Shell
Open the terminal and start the shell:
```bash
mongosh
```
Verify connection:
```bash
show dbs
```

### 2. Create Database
Switch to the **LibraryDB** database:
```bash
use LibraryDB
```

### 3. Create Collections and Insert Data

#### a. `Books` Collection
Insert data into the `Books` collection:
```javascript
db.Books.insertMany([
  { _id: 1, title: "1984", author_id: 1, genres: ["Dystopian", "Political Fiction"], published_year: 1949, available: true },
  { _id: 2, title: "To Kill a Mockingbird", author_id: 2, genres: ["Southern Gothic", "Bildungsroman"], published_year: 1960, available: true },
  { _id: 3, title: "The Great Gatsby", author_id: 3, genres: ["Tragedy"], published_year: 1925, available: true },
  { _id: 4, title: "Brave New World", author_id: 4, genres: ["Dystopian", "Science Fiction"], published_year: 1932, available: true },
  { _id: 5, title: "The Catcher in the Rye", author_id: 5, genres: ["Realist Novel", "Bildungsroman"], published_year: 1951, available: true },
  { _id: 6, title: "Moby-Dick", author_id: 6, genres: ["Adventure Fiction"], published_year: 1851, available: true },
  { _id: 7, title: "Pride and Prejudice", author_id: 7, genres: ["Romantic Novel"], published_year: 1813, available: true },
  { _id: 8, title: "War and Peace", author_id: 8, genres: ["Historical Novel"], published_year: 1869, available: true },
  { _id: 9, title: "Crime and Punishment", author_id: 9, genres: ["Philosophical Novel"], published_year: 1866, available: true },
  { _id: 10, title: "The Hobbit", author_id: 10, genres: ["Fantasy"], published_year: 1937, available: true }
]);
```

#### b. `Authors` Collection
Insert data into the `Authors` collection:
```javascript
db.Authors.insertMany([
  { _id: 1, name: "George Orwell", nationality: "British", birth_year: 1903, death_year: 1950 },
  { _id: 2, name: "Harper Lee", nationality: "American", birth_year: 1926, death_year: 2016 },
  { _id: 3, name: "F. Scott Fitzgerald", nationality: "American", birth_year: 1896, death_year: 1940 },
  { _id: 4, name: "Aldous Huxley", nationality: "British", birth_year: 1894, death_year: 1963 },
  { _id: 5, name: "J.D. Salinger", nationality: "American", birth_year: 1919, death_year: 2010 },
  { _id: 6, name: "Herman Melville", nationality: "American", birth_year: 1819, death_year: 1891 },
  { _id: 7, name: "Jane Austen", nationality: "British", birth_year: 1775, death_year: 1817 },
  { _id: 8, name: "Leo Tolstoy", nationality: "Russian", birth_year: 1828, death_year: 1910 },
  { _id: 9, name: "Fyodor Dostoevsky", nationality: "Russian", birth_year: 1821, death_year: 1881 },
  { _id: 10, name: "J.R.R. Tolkien", nationality: "British", birth_year: 1892, death_year: 1973 }
]);
```

#### c. `Patrons` Collection
Insert data into the `Patrons` collection:
```javascript
db.Patrons.insertMany([
  { _id: 1, name: "Alice Johnson", email: "alice@example.com", borrowed_books: [] },
  { _id: 2, name: "Bob Smith", email: "bob@example.com", borrowed_books: [1, 2] },
  { _id: 3, name: "Carol White", email: "carol@example.com", borrowed_books: [] },
  { _id: 4, name: "David Brown", email: "david@example.com", borrowed_books: [3] },
  { _id: 5, name: "Eve Davis", email: "eve@example.com", borrowed_books: [] },
  { _id: 6, name: "Frank Moore", email: "frank@example.com", borrowed_books: [4, 5] },
  { _id: 7, name: "Grace Miller", email: "grace@example.com", borrowed_books: [] },
  { _id: 8, name: "Hank Wilson", email: "hank@example.com", borrowed_books: [6] },
  { _id: 9, name: "Ivy Taylor", email: "ivy@example.com", borrowed_books: [] },
  { _id: 10, name: "Jack Anderson", email: "jack@example.com", borrowed_books: [7, 8] }
]);
```

---

## CRUD Operations

### READ
1. Find all books:
   ```javascript
   db.Books.find().pretty();
   ```
2. Find a specific book by title:
   ```javascript
   db.Books.find({ title: "To Kill a Mockingbird" }).pretty();
   ```
3. Find all books by a specific author:
   ```javascript
   db.Books.find({ author_id: 5 }).pretty();
   ```
4. Find all available books:
   ```javascript
   db.Books.find({ available: true }).pretty();
   ```

### UPDATE
1. Mark a book as borrowed:
   ```javascript
   db.Books.updateOne({ _id: 3 }, { $set: { available: false } });
   ```
2. Add a genre to a book:
   ```javascript
   db.Books.updateOne({ _id: 8 }, { $addToSet: { genres: "Classic" } });
   ```
3. Add a borrowed book to a patron’s record:
   ```javascript
   db.Patrons.updateOne({ _id: 5 }, { $addToSet: { borrowed_books: 10 } });
   ```

### DELETE
1. Delete a book by title:
   ```javascript
   db.Books.deleteOne({ title: "Brave New World" });
   ```
2. Delete an author:
   ```javascript
   db.Authors.deleteOne({ _id: 3 });
   ```

---

## Advanced Queries

1. Find books published after 1950:
   ```javascript
   db.Books.find({ published_year: { $gt: 1950 } }).pretty();
   ```
2. Find all American authors:
   ```javascript
   db.Authors.find({ nationality: { $eq: "American" } }).pretty();
   ```
3. Set all books to available:
   ```javascript
   db.Books.updateMany({}, { $set: { available: true } });
   ```
4. Find available books published after 1950:
   ```javascript
   db.Books.find({ available: true, published_year: { $gt: 1950 } }).pretty();
   ```
5. Find authors whose names contain "George":
   ```javascript
   db.Authors.find({ name: { $regex: "George" } }).pretty();
   ```
6. Increment the published year of "1869" by 1:
   ```javascript
   db.Books.updateMany({ published_year: 1869 }, { $inc: { published_year: 1 } });
   ```

---

## Verification
1. Verify database creation:
   ```bash
   show dbs
   ```
2. Verify collections:
   ```bash
   show collections
   ```
3. Verify inserted data:
   ```javascript
   db.Books.find().pretty();
   db.Authors.find().pretty();
   db.Patrons.find().pretty();
   ```

---



