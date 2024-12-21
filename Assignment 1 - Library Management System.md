```txt
Client Request:
"Hi, I run a library, and I need a system to help manage our operations. We have books with details like title, author, publisher, year published, and series information. Each book can belong to a category (e.g., Fiction, Non-Fiction, Science), and I’d like to store the categories separately. Each book can be written by multiple authors, and published by one publisher.
We have members with details like name, address, phone number, and date joined. Some members are premium members who can borrow more books and have an annual fee. I need to track borrowings, including the borrow date, return date, and the librarian who facilitated the transaction. Oh, and I also need to manage librarians with details like name, employee ID, and work shifts. Can you make it easy to generate reports showing the most borrowed books, most active members, and transactions by a specific librarian?"

```

### **Client Request Analysis: Library Management System**

---

### **1. Introduction:**

The client operates a library and is seeking a system to manage various library operations. This includes managing books, members, librarians, borrowings, and generating reports. The system must track books, their categories, authors, publishers, and borrowing details. Additionally, the client requires functionality for managing members, particularly differentiating between regular and premium members, as well as tracking librarian activities and generating relevant reports.

---

### **2. Business Requirements:**

#### **2.1 Books Management:**

- **Book Details:** The system must store books with attributes such as:
  - Title
  - Author(s) (Multiple authors per book)
  - Publisher (One publisher per book)
  - Year Published
  - Series (If applicable)
- **Categories:** Books can belong to categories (e.g., Fiction, Non-Fiction, Science). These categories must be stored separately, indicating a **one-to-many** relationship between books and categories.

#### **2.2 Authors and Publishers:**

- **Authors:** Each book can be written by multiple authors. This suggests a **many-to-many** relationship between books and authors.
- **Publisher:** Each book can have one publisher. This is a **one-to-many** relationship, where one publisher can publish multiple books.

#### **2.3 Members Management:**

- **Member Details:** The system must store member details such as:
  - Name
  - Address
  - Phone Number
  - Date Joined
- **Premium Membership:** The system must differentiate between regular and premium members. Premium members:
  - Can borrow more books than regular members.
  - Have an associated annual fee.

#### **2.4 Borrowing System:**

- **Track Borrowings:** The system must track borrowings with the following details:
  - Borrow Date
  - Return Date
  - Librarian who facilitated the transaction
- **Borrowing Limits:** The system should handle different borrowing limits based on member type (regular vs. premium).

#### **2.5 Librarians Management:**

- **Librarian Details:** The system must store librarian details such as:
  - Name
  - Employee ID
  - Work Shifts (Shifts per day, week, etc.)
- **Transaction Management:** Each borrowing transaction must be associated with a specific librarian.

#### **2.6 Reporting Requirements:**

- **Reports Needed:**
  - **Most Borrowed Books:** A report to show the most borrowed books, potentially filtered by time period (e.g., weekly, monthly, annually).
  - **Most Active Members:** A report showing members who borrow the most books.
  - **Librarian Transactions:** A report showing transaction activity by a specific librarian, detailing the number of borrowings managed by them.

---

### **3. Functional Requirements:**

- **CRUD Operations:** The system must allow users (admins) to Create, Read, Update, and Delete books, authors, publishers, members, and librarians.
- **Member Management:** The system must allow adding, updating, and managing member data, including premium membership status and borrowing limits.
- **Transaction Management:** A system to log and manage borrowings and returns, ensuring each transaction is tied to a librarian.
- **Report Generation:** Automated report generation based on criteria such as most borrowed books, active members, and librarian performance.
- **User Roles:** The system should allow for multiple user roles, such as:
  - **Admin** (full access to manage the system)
  - **Librarian** (ability to process borrowings/returns)
  - **Member** (view borrowing history, account details)

---

### **4. Data Modeling (ERD):**

- **Books Table:** Includes title, publisher, year published, and series.
- **Authors Table:** Many-to-many relationship with books.
- **Categories Table:** One-to-many relationship with books.
- **Members Table:** Includes details for both regular and premium members.
- **Transactions Table:** Includes borrow date, return date, and librarian ID.
- **Librarians Table:** Includes name, employee ID, and work shift information.

---

### **5. Non-Functional Requirements:**

- **Performance:** The system should handle large volumes of data (e.g., books, members, transactions).
- **Security:** The system should have role-based access control to ensure data security and privacy.
- **Scalability:** The system should be scalable to accommodate future growth (e.g., new branches, more books, and members).
- **Usability:** The system must be user-friendly for both librarians and members, with intuitive interfaces for managing books and transactions.

---

### **6. User Stories and Use Cases:**

- **User Story 1:** As an **admin**, I want to add new books with multiple authors and categories, so that I can manage the library’s collection effectively.
- **User Story 2:** As a **member**, I want to borrow books based on my membership type, so that I can borrow more books if I am a premium member.
- **User Story 3:** As a **librarian**, I want to record the borrow date, return date, and the librarian facilitating the transaction, so that the borrowing process is tracked accurately.
- **User Story 4:** As a **library manager**, I want to generate a report showing the most borrowed books over the last month, so I can analyze popular items.
- **Use Case:** **Borrow Book:** A member selects a book, a librarian records the borrowing transaction, and the system updates the member’s borrowing history and available borrowing limit.

---

### **7. Risk Assessment:**

- **Data Integrity:** Ensuring the relationships between books, authors, categories, and transactions are maintained correctly.
- **Scalability:** Ensuring that the system can scale to accommodate an increasing number of books, members, and transactions.
- **Security:** Ensuring that sensitive member data (e.g., address, phone number) is securely stored and only accessible by authorized users.

---

### **8. Final Deliverables:**

- **Business Requirements Document (BRD)**: Detailed documentation of all business needs and system requirements.
- **Functional Specification Document (FSD)**: Clear specification of the system’s functionality, including reports, workflows, and interfaces.
- **Entity-Relationship Diagram (ERD)**: A visual representation of the data model and relationships.
- **Wireframes/UI Designs**: Initial designs for key user interfaces such as member dashboards, librarian transaction management, and admin report generation screens.
- **Test Cases:** To ensure that the system works as intended.

---

### ERD Design for Library Management System

**Entities and Attributes**:

1. **Books**

   - Attributes: `BookID` (PK), `Title`, `PublisherID` (FK), `YearPublished`, `Series`
   - Relationships:
     - **Categories** (One-to-many): Each book belongs to one category.
     - **Authors** (Many-to-many): Each book can have multiple authors.

2. **Authors**

   - Attributes: `AuthorID` (PK), `Name`, `Bio`
   - Relationships:
     - **Books** (Many-to-many): An author can write multiple books, and each book can have multiple authors.

3. **Publishers**

   - Attributes: `PublisherID` (PK), `Name`, `Address`
   - Relationships:
     - **Books** (One-to-many): Each publisher can publish multiple books.

4. **Categories**

   - Attributes: `CategoryID` (PK), `CategoryName`
   - Relationships:
     - **Books** (One-to-many): A book belongs to one category.

5. **Members**

   - Attributes: `MemberID` (PK), `Name`, `Address`, `PhoneNumber`, `DateJoined`, `MembershipType`, `AnnualFee`
   - Relationships:
     - **Transactions** (One-to-many): A member can have multiple borrowing transactions.
     - **MembershipType**: Premium vs. Regular, with varying borrowing limits (handled via a system of roles or through a “MembershipType” field in the member’s table).

6. **Transactions**

   - Attributes: `TransactionID` (PK), `MemberID` (FK), `BookID` (FK), `LibrarianID` (FK), `BorrowDate`, `ReturnDate`
   - Relationships:
     - **Books** (Many-to-one): Each transaction is for a specific book.
     - **Members** (Many-to-one): Each transaction is tied to a member.
     - **Librarians** (Many-to-one): A librarian facilitates the borrowing process.

7. **Librarians**
   - Attributes: `LibrarianID` (PK), `Name`, `EmployeeID`, `WorkShifts`
   - Relationships:
     - **Transactions** (One-to-many): A librarian can facilitate multiple borrowing transactions.

---

### Relationships and Cardinality:

1. **Books-Authors (Many-to-Many)**:

   - Use a junction table, e.g., `BookAuthors` with `BookID` and `AuthorID` to establish the relationship between books and authors.

2. **Books-Categories (One-to-Many)**:

   - A book belongs to one category, but each category can have many books. Thus, `CategoryID` is a foreign key in the `Books` table.

3. **Books-Publishers (One-to-Many)**:

   - A book can only have one publisher, but each publisher can have multiple books. Thus, `PublisherID` is a foreign key in the `Books` table.

4. **Members-Transactions (One-to-Many)**:

   - A member can borrow multiple books (transactions), but each transaction is linked to one member. Thus, `MemberID` is a foreign key in the `Transactions` table.

5. **Books-Transactions (One-to-Many)**:

   - Each transaction is for one book, but a book can be borrowed multiple times. Thus, `BookID` is a foreign key in the `Transactions` table.

6. **Librarians-Transactions (One-to-Many)**:
   - A librarian manages multiple borrowing transactions, but each transaction is managed by one librarian. Thus, `LibrarianID` is a foreign key in the `Transactions` table.

---

### Handling Corner Cases:

1. **Multiple Authors**:

   - The junction table `BookAuthors` handles multiple authors for a single book by linking `BookID` and `AuthorID`.

2. **Premium and Regular Members**:

   - The `Members` table contains a `MembershipType` field to differentiate between regular and premium members. Premium members may also have an `AnnualFee` field to track their fee. Premium members can have different borrowing limits, managed via business logic in the system.

3. **Borrowing Limits**:

   - Borrowing limits are handled in the system’s business logic by checking the member’s `MembershipType`. Regular members have a lower borrowing limit than premium members, which can be enforced when the borrowing transaction is recorded.

4. **Overdue Books**:

   - The `Transactions` table will store the `ReturnDate`, allowing the system to flag overdue books based on the current date and return date.

5. **Shifts for Librarians**:
   - The `Librarians` table includes a `WorkShifts` field to store shift information, which can be detailed by day, week, or other relevant units.

---

### Data Model Diagram:

The ERD will include the following tables and relationships:

- **Books**

  - `BookID` (PK), `Title`, `PublisherID` (FK), `YearPublished`, `Series`
  - Relationships: Many-to-many with `Authors`, One-to-many with `Categories`, One-to-many with `Transactions`.

- **Authors**

  - `AuthorID` (PK), `Name`, `Bio`
  - Relationship: Many-to-many with `Books`.

- **Publishers**

  - `PublisherID` (PK), `Name`, `Address`
  - Relationship: One-to-many with `Books`.

- **Categories**

  - `CategoryID` (PK), `CategoryName`
  - Relationship: One-to-many with `Books`.

- **Members**

  - `MemberID` (PK), `Name`, `Address`, `PhoneNumber`, `DateJoined`, `MembershipType`, `AnnualFee`
  - Relationship: One-to-many with `Transactions`.

- **Transactions**

  - `TransactionID` (PK), `MemberID` (FK), `BookID` (FK), `LibrarianID` (FK), `BorrowDate`, `ReturnDate`
  - Relationships: Many-to-one with `Books`, Many-to-one with `Members`, Many-to-one with `Librarians`.

- **Librarians**
  - `LibrarianID` (PK), `Name`, `EmployeeID`, `WorkShifts`
  - Relationship: One-to-many with `Transactions`.

---

```mermaid

erDiagram
    BOOKS {
        int BookID PK
        string Title
        int PublisherID FK
        int YearPublished
        string Series
    }
    AUTHORS {
        int AuthorID PK
        string Name
        string Bio
    }
    PUBLISHERS {
        int PublisherID PK
        string Name
        string Address
    }
    CATEGORIES {
        int CategoryID PK
        string CategoryName
    }
    MEMBERS {
        int MemberID PK
        string Name
        string Address
        string PhoneNumber
        date DateJoined
        string MembershipType
        float AnnualFee
    }
    TRANSACTIONS {
        int TransactionID PK
        int MemberID FK
        int BookID FK
        int LibrarianID FK
        date BorrowDate
        date ReturnDate
    }
    LIBRARIANS {
        int LibrarianID PK
        string Name
        string EmployeeID
        string WorkShifts
    }

    BOOKS ||--o{ AUTHORS : "many-to-many"
    BOOKS }|--o{ CATEGORIES : "one-to-many"
    BOOKS }|--o{ TRANSACTIONS : "one-to-many"
    AUTHORS }|--o{ BOOKS : "many-to-many"
    PUBLISHERS ||--o{ BOOKS : "one-to-many"
    CATEGORIES ||--o{ BOOKS : "one-to-many"
    MEMBERS ||--o{ TRANSACTIONS : "one-to-many"
    TRANSACTIONS }|--o{ BOOKS : "many-to-one"
    TRANSACTIONS }|--o{ MEMBERS : "many-to-one"
    TRANSACTIONS }|--o{ LIBRARIANS : "many-to-one"
    LIBRARIANS ||--o{ TRANSACTIONS : "one-to-many"

```

---

### SQL Queries for the Library Management System

Based on the provided ERD design, here are the SQL queries needed to create the tables and establish the necessary relationships. I will break it down into several sections.

---

### 1. **Table Creation Queries:**

#### Books Table

```sql
CREATE TABLE Books (
    BookID INT PRIMARY KEY,
    Title VARCHAR(255),
    PublisherID INT,
    YearPublished INT,
    Series VARCHAR(255),
    CategoryID INT,
    FOREIGN KEY (PublisherID) REFERENCES Publishers(PublisherID),
    FOREIGN KEY (CategoryID) REFERENCES Categories(CategoryID)
);
```

#### Authors Table

```sql
CREATE TABLE Authors (
    AuthorID INT PRIMARY KEY,
    Name VARCHAR(255),
    Bio TEXT
);
```

#### Publishers Table

```sql
CREATE TABLE Publishers (
    PublisherID INT PRIMARY KEY,
    Name VARCHAR(255),
    Address TEXT
);
```

#### Categories Table

```sql
CREATE TABLE Categories (
    CategoryID INT PRIMARY KEY,
    CategoryName VARCHAR(255)
);
```

#### Members Table

```sql
CREATE TABLE Members (
    MemberID INT PRIMARY KEY,
    Name VARCHAR(255),
    Address TEXT,
    PhoneNumber VARCHAR(20),
    DateJoined DATE,
    MembershipType ENUM('Regular', 'Premium'),
    AnnualFee DECIMAL(10, 2)
);
```

#### Transactions Table

```sql
CREATE TABLE Transactions (
    TransactionID INT PRIMARY KEY,
    MemberID INT,
    BookID INT,
    LibrarianID INT,
    BorrowDate DATE,
    ReturnDate DATE,
    FOREIGN KEY (MemberID) REFERENCES Members(MemberID),
    FOREIGN KEY (BookID) REFERENCES Books(BookID),
    FOREIGN KEY (LibrarianID) REFERENCES Librarians(LibrarianID)
);
```

#### Librarians Table

```sql
CREATE TABLE Librarians (
    LibrarianID INT PRIMARY KEY,
    Name VARCHAR(255),
    EmployeeID VARCHAR(50),
    WorkShifts TEXT
);
```

#### Junction Table for Books-Authors (Many-to-Many Relationship)

```sql
CREATE TABLE BookAuthors (
    BookID INT,
    AuthorID INT,
    PRIMARY KEY (BookID, AuthorID),
    FOREIGN KEY (BookID) REFERENCES Books(BookID),
    FOREIGN KEY (AuthorID) REFERENCES Authors(AuthorID)
);
```

---

### 2. **Queries to Insert Data:**

#### Inserting a New Publisher

```sql
INSERT INTO Publishers (PublisherID, Name, Address)
VALUES (1, 'Pearson', '123 Publishing St, City, Country');
```

#### Inserting a New Author

```sql
INSERT INTO Authors (AuthorID, Name, Bio)
VALUES (1, 'John Doe', 'John Doe is a renowned author specializing in modern literature.');
```

#### Inserting a New Book

```sql
INSERT INTO Books (BookID, Title, PublisherID, YearPublished, Series, CategoryID)
VALUES (1, 'Introduction to SQL', 1, 2024, 'SQL for Beginners', 1);
```

#### Inserting a New Member

```sql
INSERT INTO Members (MemberID, Name, Address, PhoneNumber, DateJoined, MembershipType, AnnualFee)
VALUES (1, 'Alice Smith', '456 Library Lane, City, Country', '123-456-7890', '2024-01-01', 'Premium', 50.00);
```

#### Inserting a Transaction (Book Borrowing)

```sql
INSERT INTO Transactions (TransactionID, MemberID, BookID, LibrarianID, BorrowDate, ReturnDate)
VALUES (1, 1, 1, 1, '2024-10-01', '2024-10-15');
```

#### Inserting a New Librarian

```sql
INSERT INTO Librarians (LibrarianID, Name, EmployeeID, WorkShifts)
VALUES (1, 'Mark Johnson', 'L123', 'Mon-Fri 9am-5pm');
```

---

### 3. **Queries for Relationship Management:**

#### Assigning Authors to a Book (Many-to-Many Relationship)

```sql
INSERT INTO BookAuthors (BookID, AuthorID)
VALUES (1, 1);  -- Book 1 is written by Author 1
```

#### Retrieving All Books by an Author

```sql
SELECT b.Title
FROM Books b
JOIN BookAuthors ba ON b.BookID = ba.BookID
WHERE ba.AuthorID = 1;  -- Find all books written by Author 1
```

#### Retrieving All Authors for a Specific Book

```sql
SELECT a.Name
FROM Authors a
JOIN BookAuthors ba ON a.AuthorID = ba.AuthorID
WHERE ba.BookID = 1;  -- Find all authors of Book 1
```

#### Retrieving All Books Borrowed by a Member

```sql
SELECT b.Title, t.BorrowDate, t.ReturnDate
FROM Books b
JOIN Transactions t ON b.BookID = t.BookID
WHERE t.MemberID = 1;  -- Find all books borrowed by Member 1
```

#### Retrieving All Members Who Borrowed a Specific Book

```sql
SELECT m.Name, t.BorrowDate, t.ReturnDate
FROM Members m
JOIN Transactions t ON m.MemberID = t.MemberID
WHERE t.BookID = 1;  -- Find all members who borrowed Book 1
```

#### Retrieving Overdue Books (Books not returned)

```sql
SELECT b.Title, t.MemberID, t.ReturnDate
FROM Books b
JOIN Transactions t ON b.BookID = t.BookID
WHERE t.ReturnDate < CURDATE() AND t.ReturnDate IS NOT NULL;
```

#### Counting the Number of Transactions for a Member

```sql
SELECT COUNT(*) AS TransactionCount
FROM Transactions
WHERE MemberID = 1;  -- Count how many books Member 1 has borrowed
```

---

### 4. **Queries for Business Logic (Borrowing Limits):**

#### Checking Borrowing Limit Based on Membership Type (Assuming the system logic is implemented to limit transactions based on membership type)

```sql
SELECT
    CASE
        WHEN m.MembershipType = 'Premium' THEN 'Unlimited'
        WHEN m.MembershipType = 'Regular' THEN '5 Books'
    END AS BorrowingLimit
FROM Members m
WHERE m.MemberID = 1;  -- Check borrowing limit for Member 1
```

#### Retrieving Borrowed Books for a Regular Member to Enforce Borrowing Limit (Ensure they don't exceed the limit)

```sql
SELECT COUNT(*) AS BooksBorrowed
FROM Transactions
WHERE MemberID = 1 AND ReturnDate IS NULL;  -- Books currently borrowed by Member 1 (Not returned yet)
```

---

### 5. **Indexes for Performance Optimization:**

#### Creating Indexes on Foreign Keys (Improves JOIN performance)

```sql
CREATE INDEX idx_books_publisher_id ON Books(PublisherID);
CREATE INDEX idx_books_category_id ON Books(CategoryID);
CREATE INDEX idx_transactions_member_id ON Transactions(MemberID);
CREATE INDEX idx_transactions_book_id ON Transactions(BookID);
CREATE INDEX idx_transactions_librarian_id ON Transactions(LibrarianID);
```

#### Creating Index for Many-to-Many Relationship (Books-Authors)

```sql
CREATE INDEX idx_bookauthors_book_id ON BookAuthors(BookID);
CREATE INDEX idx_bookauthors_author_id ON BookAuthors(AuthorID);
```

---

## OOP Representaion:

---

## 1. Data Models

### Category

- A **one-to-many** relationship exists between categories and books (one category can be assigned to many books, and each book can have multiple categories).
- However, we will store categories in a `List<Category>` inside a `Book` for simplicity (many-to-many approach is also possible if you choose to store categories differently).

```csharp
public class Category
{
    public int Id { get; set; }
    public string Name { get; set; }

    public Category(int id, string name)
    {
        Id = id;
        Name = name;
    }

    // For better readability
    public override string ToString() => Name;
}
```

### Author

- A **many-to-many** relationship: one author can write multiple books, and one book can have multiple authors.

```csharp
public class Author
{
    public int Id { get; set; }
    public string Name { get; set; }

    public Author(int id, string name)
    {
        Id = id;
        Name = name;
    }

    public override string ToString() => Name;
}
```

### Publisher

- A **one-to-many** relationship: one publisher can publish multiple books, but each book has exactly one publisher.

```csharp
public class Publisher
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Address { get; set; }

    public Publisher(int id, string name, string address)
    {
        Id = id;
        Name = name;
        Address = address;
    }

    public override string ToString() => Name;
}
```

### Book

- Tracks the publisher (one-to-many relationship).
- Can have multiple authors (many-to-many).
- Can have multiple categories (one-to-many, or many-to-many with a bridging entity, depending on your preference).

```csharp
public class Book
{
    public int Id { get; set; }
    public string Title { get; set; }
    public Publisher Publisher { get; set; }
    public int YearPublished { get; set; }
    public string Series { get; set; }

    // Many-to-many: A book can have multiple authors
    public List<Author> Authors { get; set; } = new List<Author>();

    // Many-to-many or one-to-many: A book can have multiple categories
    public List<Category> Categories { get; set; } = new List<Category>();

    public Book(int id, string title, Publisher publisher, int yearPublished, string series)
    {
        Id = id;
        Title = title;
        Publisher = publisher;
        YearPublished = yearPublished;
        Series = series;
    }

    public override string ToString()
    {
        return $"{Title} ({YearPublished})";
    }
}
```

---

## 2. Members and Librarians

### Base Member Class

- Stores common fields: `Name`, `Address`, `PhoneNumber`, `DateJoined`.
- Defines an abstract `BorrowLimit` property to differentiate regular from premium members.

```csharp
public abstract class Member
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Address { get; set; }
    public string PhoneNumber { get; set; }
    public DateTime DateJoined { get; set; }

    // The number of books a member can borrow at once
    public abstract int BorrowLimit { get; }

    protected Member(int id, string name, string address, string phoneNumber, DateTime dateJoined)
    {
        Id = id;
        Name = name;
        Address = address;
        PhoneNumber = phoneNumber;
        DateJoined = dateJoined;
    }

    public override string ToString()
    {
        return $"{Name} (ID: {Id})";
    }
}
```

### Regular Member

- Inherits from `Member`.
- Has a fixed borrow limit (e.g., `5`).

```csharp
public class RegularMember : Member
{
    public override int BorrowLimit => 5;

    public RegularMember(int id, string name, string address, string phoneNumber, DateTime dateJoined)
        : base(id, name, address, phoneNumber, dateJoined)
    {
    }
}
```

### Premium Member

- Also inherits from `Member`.
- Higher borrow limit (e.g., `10`) and an annual fee attribute.

```csharp
public class PremiumMember : Member
{
    public override int BorrowLimit => 10;
    public decimal AnnualFee { get; set; }

    public PremiumMember(int id, string name, string address, string phoneNumber, DateTime dateJoined, decimal annualFee)
        : base(id, name, address, phoneNumber, dateJoined)
    {
        AnnualFee = annualFee;
    }
}
```

### Librarian

- Stores librarian-specific details: `EmployeeId`, `WorkShifts`.
- Responsible for facilitating transactions (we’ll see an example usage later).

```csharp
public class Librarian
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string EmployeeId { get; set; }
    public string WorkShifts { get; set; } // E.g., "Morning Shift", "Evening Shift"

    public Librarian(int id, string name, string employeeId, string workShifts)
    {
        Id = id;
        Name = name;
        EmployeeId = employeeId;
        WorkShifts = workShifts;
    }

    public override string ToString()
    {
        return $"{Name} (Employee ID: {EmployeeId})";
    }
}
```

---

## 3. Borrowing Transactions

### Transaction

- Tracks which book was borrowed, by which member, under which librarian, plus the dates.
- `BorrowDate` and `ReturnDate` (if returned).

```csharp
public class BorrowTransaction
{
    public int Id { get; set; }
    public Book Book { get; set; }
    public Member Member { get; set; }
    public Librarian Librarian { get; set; }
    public DateTime BorrowDate { get; set; }
    public DateTime? ReturnDate { get; set; } // Nullable, if not returned yet

    public BorrowTransaction(int id, Book book, Member member, Librarian librarian)
    {
        Id = id;
        Book = book;
        Member = member;
        Librarian = librarian;
        BorrowDate = DateTime.Now;
    }

    public void ReturnBook()
    {
        ReturnDate = DateTime.Now;
    }
}
```

---

## 4. Repositories (In-Memory for Demonstration)

We’ll create simple in-memory repositories to handle CRUD operations. In a real system, these might be EF Core repositories or similar database-backed services.

```csharp
public interface IRepository<T>
{
    void Add(T entity);
    T GetById(int id);
    IEnumerable<T> GetAll();
    void Update(T entity);
    void Delete(int id);
}
```

### BookRepository

```csharp
public class BookRepository : IRepository<Book>
{
    private readonly List<Book> _books = new List<Book>();

    public void Add(Book entity)
    {
        _books.Add(entity);
    }

    public Book GetById(int id)
    {
        return _books.FirstOrDefault(b => b.Id == id);
    }

    public IEnumerable<Book> GetAll()
    {
        return _books;
    }

    public void Update(Book entity)
    {
        var existing = GetById(entity.Id);
        if (existing != null)
        {
            existing.Title = entity.Title;
            existing.Publisher = entity.Publisher;
            existing.YearPublished = entity.YearPublished;
            existing.Series = entity.Series;
            existing.Authors = entity.Authors;
            existing.Categories = entity.Categories;
        }
    }

    public void Delete(int id)
    {
        var book = GetById(id);
        if (book != null)
        {
            _books.Remove(book);
        }
    }
}
```

### MemberRepository

```csharp
public class MemberRepository : IRepository<Member>
{
    private readonly List<Member> _members = new List<Member>();

    public void Add(Member entity)
    {
        _members.Add(entity);
    }

    public Member GetById(int id)
    {
        return _members.FirstOrDefault(m => m.Id == id);
    }

    public IEnumerable<Member> GetAll()
    {
        return _members;
    }

    public void Update(Member entity)
    {
        var existing = GetById(entity.Id);
        if (existing != null)
        {
            existing.Name = entity.Name;
            existing.Address = entity.Address;
            existing.PhoneNumber = entity.PhoneNumber;
            existing.DateJoined = entity.DateJoined;
            // If PremiumMember or RegularMember, handle accordingly
        }
    }

    public void Delete(int id)
    {
        var member = GetById(id);
        if (member != null)
        {
            _members.Remove(member);
        }
    }
}
```

### LibrarianRepository

```csharp
public class LibrarianRepository : IRepository<Librarian>
{
    private readonly List<Librarian> _librarians = new List<Librarian>();

    public void Add(Librarian entity)
    {
        _librarians.Add(entity);
    }

    public Librarian GetById(int id)
    {
        return _librarians.FirstOrDefault(l => l.Id == id);
    }

    public IEnumerable<Librarian> GetAll()
    {
        return _librarians;
    }

    public void Update(Librarian entity)
    {
        var existing = GetById(entity.Id);
        if (existing != null)
        {
            existing.Name = entity.Name;
            existing.EmployeeId = entity.EmployeeId;
            existing.WorkShifts = entity.WorkShifts;
        }
    }

    public void Delete(int id)
    {
        var librarian = GetById(id);
        if (librarian != null)
        {
            _librarians.Remove(librarian);
        }
    }
}
```

### TransactionRepository

```csharp
public class TransactionRepository : IRepository<BorrowTransaction>
{
    private readonly List<BorrowTransaction> _transactions = new List<BorrowTransaction>();

    public void Add(BorrowTransaction entity)
    {
        _transactions.Add(entity);
    }

    public BorrowTransaction GetById(int id)
    {
        return _transactions.FirstOrDefault(t => t.Id == id);
    }

    public IEnumerable<BorrowTransaction> GetAll()
    {
        return _transactions;
    }

    public void Update(BorrowTransaction entity)
    {
        var existing = GetById(entity.Id);
        if (existing != null)
        {
            existing.Book = entity.Book;
            existing.Member = entity.Member;
            existing.Librarian = entity.Librarian;
            existing.BorrowDate = entity.BorrowDate;
            existing.ReturnDate = entity.ReturnDate;
        }
    }

    public void Delete(int id)
    {
        var transaction = GetById(id);
        if (transaction != null)
        {
            _transactions.Remove(transaction);
        }
    }
}
```

---

## 5. Core Library System Service

A service class that orchestrates borrowing, returning, and reporting logic. This helps keep logic out of repositories (which are purely data-access oriented).

```csharp
public class LibraryService
{
    private readonly IRepository<Book> _bookRepo;
    private readonly IRepository<Member> _memberRepo;
    private readonly IRepository<Librarian> _librarianRepo;
    private readonly IRepository<BorrowTransaction> _transactionRepo;

    public LibraryService(
        IRepository<Book> bookRepo,
        IRepository<Member> memberRepo,
        IRepository<Librarian> librarianRepo,
        IRepository<BorrowTransaction> transactionRepo)
    {
        _bookRepo = bookRepo;
        _memberRepo = memberRepo;
        _librarianRepo = librarianRepo;
        _transactionRepo = transactionRepo;
    }

    /// <summary>
    /// Facilitates the borrowing of a book by a member under a specific librarian.
    /// Checks borrowing limits and throws an exception if exceeded.
    /// </summary>
    public void BorrowBook(int bookId, int memberId, int librarianId)
    {
        var book = _bookRepo.GetById(bookId);
        var member = _memberRepo.GetById(memberId);
        var librarian = _librarianRepo.GetById(librarianId);

        if (book == null) throw new Exception("Book not found.");
        if (member == null) throw new Exception("Member not found.");
        if (librarian == null) throw new Exception("Librarian not found.");

        // Check how many active transactions the member currently has
        var activeBorrows = _transactionRepo.GetAll()
            .Count(t => t.Member.Id == memberId && t.ReturnDate == null);

        if (activeBorrows >= member.BorrowLimit)
        {
            throw new Exception($"Member has reached the borrowing limit of {member.BorrowLimit}.");
        }

        // Create a new transaction
        var transaction = new BorrowTransaction(
            id: GenerateTransactionId(),
            book: book,
            member: member,
            librarian: librarian
        );

        _transactionRepo.Add(transaction);
        Console.WriteLine(
            $"Book '{book.Title}' borrowed by '{member.Name}' on {transaction.BorrowDate} facilitated by '{librarian.Name}'."
        );
    }

    /// <summary>
    /// Facilitates the returning of a book.
    /// </summary>
    public void ReturnBook(int transactionId)
    {
        var transaction = _transactionRepo.GetById(transactionId);
        if (transaction == null) throw new Exception("Transaction not found.");

        if (transaction.ReturnDate == null)
        {
            transaction.ReturnBook();
            _transactionRepo.Update(transaction);
            Console.WriteLine(
                $"Book '{transaction.Book.Title}' returned by '{transaction.Member.Name}' on {transaction.ReturnDate.Value}."
            );
        }
        else
        {
            Console.WriteLine("Book is already returned.");
        }
    }

    /// <summary>
    /// Generates an ID for transaction. In a real application, this might be DB-generated.
    /// </summary>
    private int GenerateTransactionId()
    {
        // In a real system, IDs often come from identity columns or GUIDs.
        // Here, we can just pick the next increment.
        var allTransactions = _transactionRepo.GetAll();
        return allTransactions.Any() ? allTransactions.Max(t => t.Id) + 1 : 1;
    }

    // -------------------------
    // Reporting / Query Methods
    // -------------------------

    /// <summary>
    /// Report: Most borrowed books over all time (or could filter by date range).
    /// </summary>
    public List<(Book Book, int BorrowCount)> GetMostBorrowedBooks(int top = 5)
    {
        var grouped = _transactionRepo.GetAll()
            .GroupBy(t => t.Book)
            .Select(g => new { Book = g.Key, BorrowCount = g.Count() })
            .OrderByDescending(x => x.BorrowCount)
            .Take(top)
            .Select(x => (x.Book, x.BorrowCount))
            .ToList();

        return grouped;
    }

    /// <summary>
    /// Report: Most active members by number of borrow transactions.
    /// </summary>
    public List<(Member Member, int BorrowCount)> GetMostActiveMembers(int top = 5)
    {
        var grouped = _transactionRepo.GetAll()
            .GroupBy(t => t.Member)
            .Select(g => new { Member = g.Key, BorrowCount = g.Count() })
            .OrderByDescending(x => x.BorrowCount)
            .Take(top)
            .Select(x => (x.Member, x.BorrowCount))
            .ToList();

        return grouped;
    }

    /// <summary>
    /// Report: Transactions managed by a specific librarian.
    /// </summary>
    public List<BorrowTransaction> GetTransactionsByLibrarian(int librarianId)
    {
        return _transactionRepo.GetAll()
            .Where(t => t.Librarian.Id == librarianId)
            .ToList();
    }
}
```

---

## 6. Demonstration / Usage

```csharp
public class Program
{
    public static void Main()
    {
        // Create repositories
        var bookRepo = new BookRepository();
        var memberRepo = new MemberRepository();
        var librarianRepo = new LibrarianRepository();
        var transactionRepo = new TransactionRepository();

        // Create the service
        var libraryService = new LibraryService(bookRepo, memberRepo, librarianRepo, transactionRepo);

        // Seed data
        SeedData(bookRepo, memberRepo, librarianRepo);

        // 1) Borrow Book Scenario
        libraryService.BorrowBook(bookId: 1, memberId: 101, librarianId: 201); // Book #1 borrowed by member #101
        libraryService.BorrowBook(bookId: 2, memberId: 102, librarianId: 201); // Book #2 borrowed by member #102

        // 2) Return Book Scenario
        //   Suppose the transaction for (bookId=1, memberId=101) is transactionId=1
        libraryService.ReturnBook(transactionId: 1); // Return book #1

        // 3) Generate Reports
        var topBorrowedBooks = libraryService.GetMostBorrowedBooks(5);
        Console.WriteLine("\n--- Most Borrowed Books ---");
        foreach (var entry in topBorrowedBooks)
        {
            Console.WriteLine($"{entry.Book.Title} - Borrowed {entry.BorrowCount} time(s).");
        }

        var topActiveMembers = libraryService.GetMostActiveMembers(5);
        Console.WriteLine("\n--- Most Active Members ---");
        foreach (var entry in topActiveMembers)
        {
            Console.WriteLine($"{entry.Member.Name} - {entry.BorrowCount} borrowings.");
        }

        var librarianTransactions = libraryService.GetTransactionsByLibrarian(librarianId: 201);
        Console.WriteLine("\n--- Transactions by Librarian 201 ---");
        foreach (var tx in librarianTransactions)
        {
            Console.WriteLine($"TX#{tx.Id}: Book '{tx.Book.Title}', Member '{tx.Member.Name}', BorrowDate = {tx.BorrowDate}, Returned = {tx.ReturnDate != null}");
        }
    }

    private static void SeedData(IRepository<Book> bookRepo, IRepository<Member> memberRepo, IRepository<Librarian> librarianRepo)
    {
        // Publishers
        var pub1 = new Publisher(1, "Penguin Random House", "Address A");
        var pub2 = new Publisher(2, "HarperCollins", "Address B");

        // Authors
        var author1 = new Author(1, "George Orwell");
        var author2 = new Author(2, "Jane Austen");

        // Categories
        var catFiction = new Category(1, "Fiction");
        var catScience = new Category(2, "Science");

        // Books
        var book1 = new Book(1, "1984", pub1, 1949, "Dystopian Series");
        book1.Authors.Add(author1);
        book1.Categories.Add(catFiction);

        var book2 = new Book(2, "Pride and Prejudice", pub2, 1813, "Romance Series");
        book2.Authors.Add(author2);
        book2.Categories.Add(catFiction);

        // Add books to repository
        bookRepo.Add(book1);
        bookRepo.Add(book2);

        // Members
        var regMember = new RegularMember(101, "Alice Johnson", "123 Main St", "555-1234", DateTime.Today.AddYears(-2));
        var premiumMember = new PremiumMember(102, "Bob Smith", "456 Elm St", "555-5678", DateTime.Today.AddYears(-1), annualFee: 99.99m);

        memberRepo.Add(regMember);
        memberRepo.Add(premiumMember);

        // Librarians
        var librarian = new Librarian(201, "John Librarian", "EMP001", "Morning Shift");
        librarianRepo.Add(librarian);
    }
}
```

### Explanation of the Flow

1. **Seeding Data**: We create some publishers, authors, categories, books, members (both **Regular** and **Premium**), and a librarian. This is purely for demonstration.
2. **Borrowing a Book**:
   - The `LibraryService.BorrowBook` method checks the member’s current active borrow count, compares it to their `BorrowLimit`, and throws an exception if exceeded. Otherwise, it creates a new `BorrowTransaction`.
3. **Returning a Book**:
   - The `LibraryService.ReturnBook` method marks the transaction as returned by setting the `ReturnDate`.
4. **Reporting**:
   - **Most Borrowed Books**: Uses grouping and sorting by the count of transactions.
   - **Most Active Members**: Groups transactions by member.
   - **Transactions by Librarian**: Filters transactions by a given librarian ID.

---
