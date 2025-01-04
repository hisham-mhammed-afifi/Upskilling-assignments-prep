# Complete Guide to Database Design with Real-World Use Cases

## **1. Understanding Database Relationships**

### **Types of Relationships**

1. **One-to-One (1:1)**

   - **Description**: One record in an entity corresponds to one record in another entity.
   - **Example**: A user and their profile. Each user has one profile, and each profile belongs to one user.
   - **Real-World Use Case**: Storing sensitive information separately, such as a user’s financial details.

2. **One-to-Many (1:N)**

   - **Description**: One record in an entity can relate to multiple records in another entity.
   - **Example**: A customer and their orders. A single customer can place many orders.
   - **Real-World Use Case**: An e-commerce platform where a customer makes multiple purchases.

3. **Many-to-Many (M:N)**

   - **Description**: Multiple records in one entity relate to multiple records in another entity.
   - **Example**: Students and courses. A student can enroll in multiple courses, and a course can have multiple students.
   - **Real-World Use Case**: Educational platforms where students and courses need flexible associations.
   - **Implementation**: A junction table (e.g., `StudentCourse`) stores the relationship.

### **Cardinality and Obligation**

- **Cardinality**:
  - **1:1**: One entity links to exactly one entity in another table.
  - **1:N**: One entity links to many entities in another table.
  - **M:N**: Many entities in one table link to many in another table.
- **Obligation**:
  - **Mandatory**: A relationship where both entities must have corresponding records (e.g., every employee must belong to a department).
  - **Optional**: A relationship where one entity may not have a corresponding record (e.g., an employee might not have any assigned tasks yet).

---

## **2. Attributes and Functional Dependencies**

### **Attribute Relationships**

- Attributes within an entity may have **functional dependencies**, meaning one attribute determines another.
  - **Example**: In a `Customer` table, the `Zip Code` determines the `City`, and the `City` determines the `State`.
- These relationships guide **normalization**, ensuring that data is stored efficiently and without redundancy.

### **Normalization**

- **1NF (First Normal Form)**: Ensure each table column contains atomic values (no repeating groups).
- **2NF (Second Normal Form)**: Eliminate partial dependencies.
- **3NF (Third Normal Form)**: Remove transitive dependencies.

---

## **3. Practical Scenarios and Use Cases**

### **Scenario 1: Employee and Car Relationship**

**Problem:** Track which employee drives which car, and record the time spent driving.

**Entities:**

1. `Employee`
   - Attributes: `employee_id`, `name`, `department`.
2. `Car`
   - Attributes: `car_id`, `license_plate`, `model`.
3. `EmployeeCar` (Junction Table)
   - Attributes: `employee_id`, `car_id`, `start_time`, `end_time`, `purpose` (e.g., delivery, personal use).

**Schema Definition:**

```sql
CREATE TABLE Employee (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department VARCHAR(50)
);

CREATE TABLE Car (
    car_id INT PRIMARY KEY,
    license_plate VARCHAR(20) NOT NULL,
    model VARCHAR(50) NOT NULL
);

CREATE TABLE EmployeeCar (
    employee_id INT,
    car_id INT,
    start_time DATETIME NOT NULL,
    end_time DATETIME NOT NULL,
    purpose VARCHAR(100),
    PRIMARY KEY (employee_id, car_id, start_time),
    FOREIGN KEY (employee_id) REFERENCES Employee(employee_id),
    FOREIGN KEY (car_id) REFERENCES Car(car_id)
);
```

**Use Cases:**

- Log the time an employee spends driving with purpose:
  ```sql
  INSERT INTO EmployeeCar (employee_id, car_id, start_time, end_time, purpose)
  VALUES (1, 101, '2025-01-02 08:00:00', '2025-01-02 12:00:00', 'Delivery');
  ```
- Calculate total driving time for a specific purpose:
  ```sql
  SELECT purpose, SUM(TIMESTAMPDIFF(MINUTE, start_time, end_time)) AS total_time
  FROM EmployeeCar
  GROUP BY purpose;
  ```
- Find which car was driven the most by department:
  ```sql
  SELECT c.car_id, e.department, SUM(TIMESTAMPDIFF(MINUTE, ec.start_time, ec.end_time)) AS total_usage_time
  FROM EmployeeCar ec
  JOIN Employee e ON ec.employee_id = e.employee_id
  JOIN Car c ON ec.car_id = c.car_id
  GROUP BY c.car_id, e.department
  ORDER BY total_usage_time DESC;
  ```

---

### **Scenario 2: Healthcare System**

**Problem:** Track doctors, patients, and appointments with additional diagnosis details.

**Entities:**

1. `Doctor`
   - Attributes: `doctor_id`, `name`, `specialization`.
2. `Patient`
   - Attributes: `patient_id`, `name`, `dob`.
3. `Appointment` (Junction Table)
   - Attributes: `appointment_id`, `doctor_id`, `patient_id`, `date_time`, `diagnosis`.

**Schema Definition:**

```sql
CREATE TABLE Doctor (
    doctor_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    specialization VARCHAR(50)
);

CREATE TABLE Patient (
    patient_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    dob DATE NOT NULL
);

CREATE TABLE Appointment (
    appointment_id INT PRIMARY KEY,
    doctor_id INT,
    patient_id INT,
    date_time DATETIME NOT NULL,
    diagnosis TEXT,
    FOREIGN KEY (doctor_id) REFERENCES Doctor(doctor_id),
    FOREIGN KEY (patient_id) REFERENCES Patient(patient_id)
);
```

**Use Cases:**

- Track the number of appointments for each specialization:
  ```sql
  SELECT d.specialization, COUNT(*) AS appointment_count
  FROM Appointment a
  JOIN Doctor d ON a.doctor_id = d.doctor_id
  GROUP BY d.specialization;
  ```
- List all appointments for a specific patient:
  ```sql
  SELECT a.date_time, d.name AS doctor_name, a.diagnosis
  FROM Appointment a
  JOIN Doctor d ON a.doctor_id = d.doctor_id
  WHERE a.patient_id = 123;
  ```

---

### **Scenario 3: Library Management System**

**Problem:** Track books, borrowers, and borrowing history, including return dates and fines.

**Entities:**

1. `Book`
   - Attributes: `book_id`, `title`, `author`.
2. `Borrower`
   - Attributes: `borrower_id`, `name`, `membership_date`.
3. `BorrowingHistory` (Junction Table)
   - Attributes: `borrow_id`, `book_id`, `borrower_id`, `borrow_date`, `return_date`, `fine_amount`.

**Schema Definition:**

```sql
CREATE TABLE Book (
    book_id INT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    author VARCHAR(100) NOT NULL
);

CREATE TABLE Borrower (
    borrower_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    membership_date DATE NOT NULL
);

CREATE TABLE BorrowingHistory (
    borrow_id INT PRIMARY KEY,
    book_id INT,
    borrower_id INT,
    borrow_date DATE NOT NULL,
    return_date DATE,
    fine_amount DECIMAL(10, 2),
    FOREIGN KEY (book_id) REFERENCES Book(book_id),
    FOREIGN KEY (borrower_id) REFERENCES Borrower(borrower_id)
);
```

**Use Cases:**

- List overdue books:
  ```sql
  SELECT bh.book_id, b.title, bh.borrower_id, bh.return_date
  FROM BorrowingHistory bh
  JOIN Book b ON bh.book_id = b.book_id
  WHERE bh.return_date IS NULL AND bh.borrow_date < CURDATE() - INTERVAL 30 DAY;
  ```
- Calculate total fines for a borrower:
  ```sql
  SELECT borrower_id, SUM(fine_amount) AS total_fine
  FROM BorrowingHistory
  WHERE borrower_id = 456;
  ```

---

## **4. Best Practices**

1. **Normalization**: Reduce redundancy and ensure data consistency.
2. **Indexes**: Optimize frequently queried columns (e.g., foreign keys).
3. **Constraints**: Use primary and foreign keys to enforce relationships.
4. **Data Integrity**: Use triggers or constraints to validate data (e.g., `return_date > borrow_date`).
5. **Extensibility**: Design junction tables to accommodate additional attributes easily.

---
