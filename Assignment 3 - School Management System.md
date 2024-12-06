```txt
Client Request:
"I’m the principal of a school, and I need a system to keep track of students, teachers, and the classes we offer. For students, I need details like ID, name, age, class, enrollment date, and their grades in each subject. Teachers should have their own profiles, including name, ID, subject specialization, and phone number.
We also offer courses that teachers can teach, and each course can have multiple sections assigned to different teachers. Students enroll in these courses, so I need to track which student is in which course and their attendance. Additionally, I’d like to manage extracurricular activities, with details on which students and teachers are involved. Later, we might want to add a feature for scheduling exams and managing results."

```

### **Client Request Analysis: School Management System**

---

### **1. Introduction:**

The client, a school principal, requires a system to track students, teachers, classes, courses, attendance, and extracurricular activities. The system should manage student and teacher profiles, as well as handle course enrollments, attendance, and possibly exams in the future. This solution should also allow tracking of extracurricular activities and manage the teachers assigned to each course section.

---

### **2. Business Requirements:**

#### **2.1 Student Management:**

- **Student Details:** The system should store the following student information:
  - **ID**
  - **Name**
  - **Age**
  - **Class** (Which grade or class the student belongs to)
  - **Enrollment Date**
  - **Grades:** The system must store the grades for each student in every subject they are enrolled in.
- **Course Enrollment:** Students should be able to enroll in courses. The system needs to track which students are enrolled in which courses.
- **Attendance:** The system should track student attendance in each course and store the attendance records for reporting.

#### **2.2 Teacher Management:**

- **Teacher Profiles:** Teachers should have profiles that include:
  - **Name**
  - **ID**
  - **Subject Specialization**
  - **Phone Number**
- **Course Assignments:** Teachers are assigned to specific courses, and each course can have multiple sections taught by different teachers. The system must allow for the assignment of teachers to specific courses and sections.

#### **2.3 Course Management:**

- **Course Details:** The system should store information about each course, including:
  - **Course Name**
  - **Course Description**
  - **Teachers:** Multiple teachers can be assigned to different sections of the same course.
  - **Sections:** Each course can have multiple sections, with teachers assigned to each section.
- **Course Enrollment:** Students should be able to enroll in courses, and the system should track which students are enrolled in which sections of the courses.

#### **2.4 Extracurricular Activities:**

- **Activity Management:** The system should store information about extracurricular activities, including:
  - **Activity Name**
  - **Description**
  - **Participants:** Students and teachers involved in each activity (could be a list of students and teachers associated with the activity).

#### **2.5 Exam and Results Management (Future Feature):**

- **Exam Scheduling:** Although not required immediately, the system should be capable of adding a feature in the future to manage exam schedules.
- **Results Tracking:** The system should be able to store and manage student exam results once the feature is added.

---

### **3. Functional Requirements:**

- **CRUD Operations:** The system must allow users to Create, Read, Update, and Delete:
  - Student records (ID, name, class, grades)
  - Teacher profiles (name, specialization, phone)
  - Course and section details (course name, teacher assignments)
  - Extracurricular activities (activity name, participants)
  - Attendance records
- **Course Enrollment:** Students should be able to enroll in and unenroll from courses, with attendance tracking.
- **Teacher Assignment:** Teachers should be assigned to one or more courses, with the ability to add/remove them from sections.
- **Attendance Tracking:** The system should allow teachers or administrators to mark student attendance for each class and track participation.
- **Reporting:** The system should be able to generate reports such as:
  - **Student Grades Report:** Showing grades for each subject enrolled by students.
  - **Course Enrollment Report:** List of students enrolled in each course.
  - **Attendance Report:** Detailed attendance records for each student in each course.
  - **Extracurricular Participation Report:** List of students and teachers involved in extracurricular activities.

---

### **4. Data Modeling (ERD):**

- **Students Table:** Includes student ID, name, age, class, enrollment date, and a foreign key to the grades table.
- **Teachers Table:** Includes teacher ID, name, specialization, and phone number.
- **Courses Table:** Includes course name, description, and a link to course sections.
- **Sections Table:** Stores section details and the teacher assigned to each section (many-to-one relationship with teachers).
- **Enrollments Table:** Tracks which students are enrolled in which courses/sections.
- **Grades Table:** Stores student grades for each subject and course.
- **Attendance Table:** Tracks attendance for each student in each course section.
- **Extracurricular Activities Table:** Links students and teachers to extracurricular activities.

---

### **5. Non-Functional Requirements:**

- **Performance:** The system should be able to efficiently handle data for a large number of students, teachers, courses, and extracurricular activities.
- **Scalability:** The system must be scalable to accommodate new courses, students, and teachers as the school grows.
- **Security:** Sensitive information such as student records, grades, and personal data must be securely stored, and access should be restricted based on user roles (administrators, teachers, etc.).
- **Usability:** The system should have an intuitive interface for users with varying levels of technical expertise, including school administrators and teachers.

---

### **6. User Stories and Use Cases:**

- **User Story 1:** As a **school administrator**, I want to add new students, teachers, courses, and extracurricular activities to the system, so that I can manage all school data in one place.
- **User Story 2:** As a **teacher**, I want to mark student attendance and record grades for each subject, so that I can track student performance.
- **User Story 3:** As a **student**, I want to enroll in courses, view my grades, and track my attendance in each course.
- **User Story 4:** As an **administrator**, I want to generate reports that show student grades, course enrollments, attendance, and extracurricular activities, so that I can analyze school performance.

- **Use Case:** **Teacher Assigning Courses:** A teacher is assigned to a course section. The system updates the section with the teacher’s details, and students can enroll in the course.

---

### **7. Risk Assessment:**

- **Data Accuracy:** Ensuring that student grades, attendance, and course enrollments are accurately recorded and reported.
- **User Access Control:** Managing different user roles (administrators, teachers, students) and ensuring they can access only the data they are authorized to view or edit.
- **Future Features Integration:** The addition of the exam and results management feature should be planned in such a way that it integrates smoothly with existing systems (grades, attendance).

---

### **8. Final Deliverables:**

- **Business Requirements Document (BRD):** Detailed requirements for student, teacher, course, attendance, and extracurricular activity management.
- **Functional Specification Document (FSD):** Documentation of the system’s features, including course enrollments, attendance tracking, and reporting.
- **Entity-Relationship Diagram (ERD):** A visual representation of the system’s database schema and relationships.
- **Wireframes/UI Designs:** Initial user interface designs for the administrative dashboard, teacher dashboard, and student portal.
- **Test Cases:** To ensure the functionality of student, teacher, and course management modules.

---

### ERD for School Management System

#### 1. **Entities and Attributes:**

1. **Student**

   - **Attributes:**
     - `Student_ID` (PK)
     - `Name`
     - `Age`
     - `Class_ID` (FK to Class)
     - `Enrollment_Date`
   - **Relationships:**
     - Enrolled in multiple **Enrollments**
     - Has multiple **Grades**
     - Participates in multiple **ExtracurricularActivities**

2. **Teacher**

   - **Attributes:**
     - `Teacher_ID` (PK)
     - `Name`
     - `Subject_Specialization`
     - `Phone_Number`
   - **Relationships:**
     - Assigned to multiple **Sections**
     - Participates in multiple **ExtracurricularActivities**

3. **Class**

   - **Attributes:**
     - `Class_ID` (PK)
     - `Class_Name`
     - `Grade_Level`
   - **Relationships:**
     - Has multiple **Students**

4. **Course**

   - **Attributes:**
     - `Course_ID` (PK)
     - `Course_Name`
     - `Course_Description`
   - **Relationships:**
     - Contains multiple **Sections**
     - Associated with multiple **Grades**

5. **Section**

   - **Attributes:**
     - `Section_ID` (PK)
     - `Course_ID` (FK to Course)
     - `Teacher_ID` (FK to Teacher)
   - **Relationships:**
     - Belongs to one **Course**
     - Managed by one **Teacher**
     - Includes multiple **Enrollments**
     - Records multiple **Attendances**

6. **Enrollment**

   - **Attributes:**
     - `Enrollment_ID` (PK)
     - `Student_ID` (FK to Student)
     - `Section_ID` (FK to Section)
     - `Enrollment_Date`
   - **Relationships:**
     - Links one **Student** to one **Section**

7. **Grade**

   - **Attributes:**
     - `Grade_ID` (PK)
     - `Student_ID` (FK to Student)
     - `Course_ID` (FK to Course)
     - `Grade_Value`
     - `Date_Recorded`
   - **Relationships:**
     - Assigned to one **Student**
     - Pertains to one **Course**

8. **Attendance**

   - **Attributes:**
     - `Attendance_ID` (PK)
     - `Student_ID` (FK to Student)
     - `Section_ID` (FK to Section)
     - `Date`
     - `Status` (Present, Absent, Late, Excused)
   - **Relationships:**
     - Records attendance for one **Student**
     - Pertains to one **Section**

9. **ExtracurricularActivity**

   - **Attributes:**
     - `Activity_ID` (PK)
     - `Activity_Name`
     - `Description`
   - **Relationships:**
     - Includes multiple **Participants**

10. **Participant**
    - **Attributes:**
      - `Participant_ID` (PK)
      - `Activity_ID` (FK to ExtracurricularActivity)
      - `Student_ID` (FK to Student, Nullable)
      - `Teacher_ID` (FK to Teacher, Nullable)
    - **Relationships:**
      - Links one **ExtracurricularActivity** to either one **Student** or one **Teacher**

#### 2. **Relationships and Cardinality:**

1. **Student-Class (Many-to-One):**

   - Each **Student** belongs to one **Class**.
   - Each **Class** has multiple **Students**.

2. **Course-Section (One-to-Many):**

   - Each **Course** can have multiple **Sections**.
   - Each **Section** belongs to one **Course**.

3. **Teacher-Section (One-to-Many):**

   - Each **Teacher** can manage multiple **Sections**.
   - Each **Section** is managed by one **Teacher**.

4. **Student-Enrollment-Section (Many-to-Many):**

   - **Students** can enroll in multiple **Sections**.
   - **Sections** can have multiple **Students**.
   - Managed via the **Enrollment** entity.

5. **Student-Grade-Course (Many-to-Many):**

   - **Students** receive grades in multiple **Courses**.
   - **Courses** have grades from multiple **Students**.
   - Managed via the **Grade** entity.

6. **Student-Attendance-Section (Many-to-Many):**

   - **Students** have attendance records for multiple **Sections**.
   - **Sections** have attendance records for multiple **Students**.
   - Managed via the **Attendance** entity.

7. **Student-ExtracurricularActivity (Many-to-Many):**

   - **Students** can participate in multiple **ExtracurricularActivities**.
   - **ExtracurricularActivities** can have multiple **Students** participating.
   - Managed via the **Participant** entity.

8. **Teacher-ExtracurricularActivity (Many-to-Many):**
   - **Teachers** can participate in multiple **ExtracurricularActivities**.
   - **ExtracurricularActivities** can have multiple **Teachers** participating.
   - Managed via the **Participant** entity.

#### 3. **Corner Cases:**

1. **Students with No Enrollments:**

   - **Scenario:** A student has not enrolled in any **Section** yet.
   - **Handling:** Allow creation of **Student** records without associated **Enrollment** entries. Ensure system functionalities account for zero enrollments.

2. **Courses with No Sections:**

   - **Scenario:** A **Course** exists but has no **Sections** assigned.
   - **Handling:** Permit creation of **Course** records without initial **Sections**. Enable adding **Sections** later without affecting existing data integrity.

3. **Sections with No Students:**

   - **Scenario:** A **Section** has been created but no **Students** are enrolled yet.
   - **Handling:** Allow **Sections** to exist without any **Enrollments**. Ensure that reports and functionalities handle empty **Sections** gracefully.

4. **Teachers with Multiple Specializations:**

   - **Scenario:** A **Teacher** specializes in multiple subjects.
   - **Handling:** Consider creating a separate **Subject** entity and establishing a many-to-many relationship between **Teachers** and **Subjects** if needed in the future.

5. **Participants in Extracurricular Activities:**

   - **Scenario:** **Participants** can be either **Students** or **Teachers**.
   - **Handling:** Use the **Participant** entity with nullable foreign keys (`Student_ID`, `Teacher_ID`). Implement constraints to ensure that at least one of these fields is populated.

6. **Grades Without Enrollment:**

   - **Scenario:** Assigning a **Grade** to a **Student** for a **Course** they are not enrolled in.
   - **Handling:** Enforce referential integrity by ensuring that a **Grade** can only be assigned if an **Enrollment** exists linking the **Student** to a **Section** of the **Course**.

7. **Attendance Record for Non-Enrolled Students:**

   - **Scenario:** Recording **Attendance** for a **Student** not enrolled in the **Section**.
   - **Handling:** Implement validation to ensure that **Attendance** entries are only created for **Students** enrolled in the respective **Section**.

8. **Handling Transfers or Drops:**

   - **Scenario:** **Students** transfer between **Classes** or drop **Courses**.
   - **Handling:** Allow updates to the `Class_ID` in the **Student** entity and manage **Enrollments** accordingly. Maintain historical data if necessary for reporting.

9. **Self-Referencing in Classes or Teachers:**

   - **Scenario:** A **Teacher** mentors other **Teachers**.
   - **Handling:** If applicable, implement a self-referencing relationship within the **Teacher** entity to denote mentorship.

10. **Security and Role-Based Access:**
    - **Scenario:** Restrict access to sensitive data based on user roles (e.g., administrators, teachers).
    - **Handling:** While not directly represented in the ERD, ensure that the system's architecture enforces role-based permissions to protect data integrity and privacy.

#### 4. **Data Model Diagram:**

While a visual ERD cannot be provided here, the following is a structured summary of the relationships:

- **Student** (1) → (_) **Enrollment** (_) ← (1) **Section**
- **Section** (1) → (\*) **Attendance**
- **Section** (1) → (\*) **Enrollment**
- **Course** (1) → (\*) **Section**
- **Teacher** (1) → (\*) **Section**
- **Student** (1) → (_) **Grade** (_) ← (1) **Course**
- **ExtracurricularActivity** (1) → (_) **Participant** (_) ← (1) **Student**
- **ExtracurricularActivity** (1) → (_) **Participant** (_) ← (1) **Teacher**
- **Class** (1) → (\*) **Student**

#### 5. **Additional Tables (If Needed):**

1. **Subject** (Optional)
   - **Attributes:**
     - `Subject_ID` (PK)
     - `Subject_Name`
   - **Relationships:**
     - Many-to-many with **Teacher** if teachers can specialize in multiple subjects.

#### 6. **Conclusion:**

The ERD for the School Management System comprehensively covers the core functionalities required by the client, including managing students, teachers, courses, sections, enrollments, grades, attendance, and extracurricular activities. By addressing potential corner cases, the design ensures robustness and flexibility, accommodating future expansions like exam management and additional subject specializations. Proper normalization and referential integrity are maintained to facilitate efficient data handling, reporting, and scalability.

---

### Visual Representation (Textual Description)

To better visualize the ERD, here's a textual outline of the primary relationships:

1. **Student** ↔ **Enrollment** ↔ **Section**

   - **Student** can have multiple **Enrollments**.
   - Each **Enrollment** links a **Student** to a **Section**.

2. **Section** ↔ **Course**

   - Each **Section** belongs to one **Course**.
   - Each **Course** can have multiple **Sections**.

3. **Teacher** ↔ **Section**

   - Each **Section** is managed by one **Teacher**.
   - Each **Teacher** can manage multiple **Sections**.

4. **Student** ↔ **Grade** ↔ **Course**

   - Each **Grade** links a **Student** to a **Course**.
   - Each **Course** can have multiple **Grades** from different **Students**.

5. **Section** ↔ **Attendance** ↔ **Student**

   - **Attendance** records link **Students** to their **Sections** on specific dates.

6. **ExtracurricularActivity** ↔ **Participant** ↔ **Student/Teacher**

   - **Participants** link **ExtracurricularActivities** to either **Students** or **Teachers**.

7. **Class** ↔ **Student**
   - Each **Class** includes multiple **Students**.
   - Each **Student** belongs to one **Class**.

---

```mermaid

erDiagram
    STUDENT {
        int Student_ID PK
        string Name
        int Age
        int Class_ID FK
        date Enrollment_Date
    }
    TEACHER {
        int Teacher_ID PK
        string Name
        string Subject_Specialization
        string Phone_Number
    }
    CLASS {
        int Class_ID PK
        string Class_Name
        string Grade_Level
    }
    COURSE {
        int Course_ID PK
        string Course_Name
        string Course_Description
    }
    SECTION {
        int Section_ID PK
        int Course_ID FK
        int Teacher_ID FK
    }
    ENROLLMENT {
        int Enrollment_ID PK
        int Student_ID FK
        int Section_ID FK
        date Enrollment_Date
    }
    GRADE {
        int Grade_ID PK
        int Student_ID FK
        int Course_ID FK
        float Grade_Value
        date Date_Recorded
    }
    ATTENDANCE {
        int Attendance_ID PK
        int Student_ID FK
        int Section_ID FK
        date Date
        string Status
    }
    EXTRACURRICULARACTIVITY {
        int Activity_ID PK
        string Activity_Name
        string Description
    }
    PARTICIPANT {
        int Participant_ID PK
        int Activity_ID FK
        int Student_ID FK
        int Teacher_ID FK
    }

    STUDENT }|--o{ CLASS : "belongs to"
    TEACHER }|--o{ SECTION : "manages"
    CLASS ||--o{ STUDENT : "has"
    COURSE ||--o{ SECTION : "has"
    SECTION }|--o{ ENROLLMENT : "includes"
    STUDENT }|--o{ ENROLLMENT : "enrolled in"
    STUDENT ||--o{ GRADE : "receives"
    COURSE ||--o{ GRADE : "pertains to"
    STUDENT }|--o{ ATTENDANCE : "has"
    SECTION ||--o{ ATTENDANCE : "records"
    EXTRACURRICULARACTIVITY ||--o{ PARTICIPANT : "includes"
    STUDENT ||--o{ PARTICIPANT : "participates"
    TEACHER ||--o{ PARTICIPANT : "participates"

```

---

### SQL Queries for the School Management System

Based on the provided ERD, I will review the necessary SQL queries for table creation, managing relationships, and handling the corner cases. This includes defining primary keys, foreign keys, and ensuring referential integrity.

---

### 1. **Table Creation Queries**

#### Student Table

```sql
CREATE TABLE Student (
    Student_ID INT PRIMARY KEY,
    Name VARCHAR(255),
    Age INT,
    Class_ID INT,
    Enrollment_Date DATE,
    FOREIGN KEY (Class_ID) REFERENCES Class(Class_ID)
);
```

#### Teacher Table

```sql
CREATE TABLE Teacher (
    Teacher_ID INT PRIMARY KEY,
    Name VARCHAR(255),
    Subject_Specialization VARCHAR(255),
    Phone_Number VARCHAR(20)
);
```

#### Class Table

```sql
CREATE TABLE Class (
    Class_ID INT PRIMARY KEY,
    Class_Name VARCHAR(255),
    Grade_Level INT
);
```

#### Course Table

```sql
CREATE TABLE Course (
    Course_ID INT PRIMARY KEY,
    Course_Name VARCHAR(255),
    Course_Description TEXT
);
```

#### Section Table

```sql
CREATE TABLE Section (
    Section_ID INT PRIMARY KEY,
    Course_ID INT,
    Teacher_ID INT,
    FOREIGN KEY (Course_ID) REFERENCES Course(Course_ID),
    FOREIGN KEY (Teacher_ID) REFERENCES Teacher(Teacher_ID)
);
```

#### Enrollment Table (Many-to-Many Relationship between Student and Section)

```sql
CREATE TABLE Enrollment (
    Enrollment_ID INT PRIMARY KEY,
    Student_ID INT,
    Section_ID INT,
    Enrollment_Date DATE,
    FOREIGN KEY (Student_ID) REFERENCES Student(Student_ID),
    FOREIGN KEY (Section_ID) REFERENCES Section(Section_ID)
);
```

#### Grade Table (Many-to-Many Relationship between Student and Course)

```sql
CREATE TABLE Grade (
    Grade_ID INT PRIMARY KEY,
    Student_ID INT,
    Course_ID INT,
    Grade_Value VARCHAR(10),
    Date_Recorded DATE,
    FOREIGN KEY (Student_ID) REFERENCES Student(Student_ID),
    FOREIGN KEY (Course_ID) REFERENCES Course(Course_ID)
);
```

#### Attendance Table (Many-to-Many Relationship between Student and Section)

```sql
CREATE TABLE Attendance (
    Attendance_ID INT PRIMARY KEY,
    Student_ID INT,
    Section_ID INT,
    Date DATE,
    Status ENUM('Present', 'Absent', 'Late', 'Excused'),
    FOREIGN KEY (Student_ID) REFERENCES Student(Student_ID),
    FOREIGN KEY (Section_ID) REFERENCES Section(Section_ID)
);
```

#### ExtracurricularActivity Table

```sql
CREATE TABLE ExtracurricularActivity (
    Activity_ID INT PRIMARY KEY,
    Activity_Name VARCHAR(255),
    Description TEXT
);
```

#### Participant Table (Many-to-Many Relationship between Students, Teachers, and ExtracurricularActivities)

```sql
CREATE TABLE Participant (
    Participant_ID INT PRIMARY KEY,
    Activity_ID INT,
    Student_ID INT,
    Teacher_ID INT,
    FOREIGN KEY (Activity_ID) REFERENCES ExtracurricularActivity(Activity_ID),
    FOREIGN KEY (Student_ID) REFERENCES Student(Student_ID),
    FOREIGN KEY (Teacher_ID) REFERENCES Teacher(Teacher_ID)
);
```

---

### 2. **Corner Cases Handling**

#### **1. Students with No Enrollments**

Students can be created without an Enrollment record. This is handled by allowing `Enrollment` to be a separate entity, which may or may not have entries for each student.

```sql
-- Creating a student without any enrollments
INSERT INTO Student (Student_ID, Name, Age, Class_ID, Enrollment_Date)
VALUES (1, 'John Doe', 16, 101, '2023-09-01');
```

#### **2. Courses with No Sections**

Courses can be created without any Sections. You can later add Sections to the course.

```sql
-- Creating a course without sections
INSERT INTO Course (Course_ID, Course_Name, Course_Description)
VALUES (1, 'Mathematics', 'Introduction to Algebra');
```

#### **3. Sections with No Students**

A Section can exist even if no students are enrolled. This is managed by the `Enrollment` table linking students to sections.

```sql
-- Creating a section without any students enrolled
INSERT INTO Section (Section_ID, Course_ID, Teacher_ID)
VALUES (1, 1, 101);  -- Assuming Course_ID 1 and Teacher_ID 101 exist
```

#### **4. Teachers with Multiple Specializations**

To handle teachers specializing in multiple subjects, a new `Subject` table can be introduced (optional).

```sql
-- Create a Subject table (if needed)
CREATE TABLE Subject (
    Subject_ID INT PRIMARY KEY,
    Subject_Name VARCHAR(255)
);

-- Linking Teachers to Multiple Subjects (Many-to-Many)
CREATE TABLE Teacher_Subject (
    Teacher_ID INT,
    Subject_ID INT,
    PRIMARY KEY (Teacher_ID, Subject_ID),
    FOREIGN KEY (Teacher_ID) REFERENCES Teacher(Teacher_ID),
    FOREIGN KEY (Subject_ID) REFERENCES Subject(Subject_ID)
);
```

#### **5. Participant Table for Extracurricular Activities**

Teachers and Students can both be participants in extracurricular activities. `Student_ID` and `Teacher_ID` are nullable to allow both possibilities.

```sql
-- Creating a participant entry for a student
INSERT INTO Participant (Participant_ID, Activity_ID, Student_ID, Teacher_ID)
VALUES (1, 1, 1, NULL);  -- Student 1 participates in Activity 1

-- Creating a participant entry for a teacher
INSERT INTO Participant (Participant_ID, Activity_ID, Student_ID, Teacher_ID)
VALUES (2, 1, NULL, 101);  -- Teacher 101 participates in Activity 1
```

#### **6. Grades Without Enrollment**

Grades must be linked to both the `Student` and `Course` via the `Enrollment` table. You cannot assign a grade unless a student is enrolled in a section for that course.

```sql
-- Ensuring Grade Assignment is Only Possible If Enrollment Exists
INSERT INTO Grade (Grade_ID, Student_ID, Course_ID, Grade_Value, Date_Recorded)
SELECT 1, 1, 1, 'A', '2023-12-01'
WHERE EXISTS (SELECT 1 FROM Enrollment WHERE Student_ID = 1 AND Section_ID IN (SELECT Section_ID FROM Section WHERE Course_ID = 1));
```

#### **7. Attendance Record for Non-Enrolled Students**

Attendance records are only valid if the student is enrolled in the section. This can be enforced in the application logic or via triggers.

```sql
-- Insert Attendance Only for Enrolled Students
INSERT INTO Attendance (Attendance_ID, Student_ID, Section_ID, Date, Status)
SELECT 1, 1, 1, '2023-12-01', 'Present'
WHERE EXISTS (SELECT 1 FROM Enrollment WHERE Student_ID = 1 AND Section_ID = 1);
```

#### **8. Handling Transfers or Drops**

To handle student transfers, you can update the `Class_ID` and remove or add `Enrollments` based on the transfer.

```sql
-- Transfer Student to Another Class
UPDATE Student
SET Class_ID = 102
WHERE Student_ID = 1;

-- Update Enrollment for Transfer
UPDATE Enrollment
SET Section_ID = 2
WHERE Student_ID = 1 AND Section_ID = 1;
```

#### **9. Self-Referencing for Teachers (Mentorship)**

If needed, create a `Mentor_ID` column to allow self-referencing in the `Teacher` table.

```sql
ALTER TABLE Teacher
ADD COLUMN Mentor_ID INT,
ADD FOREIGN KEY (Mentor_ID) REFERENCES Teacher(Teacher_ID);
```

---

### 3. **Additional Queries**

#### Get All Students in a Class

```sql
SELECT * FROM Student WHERE Class_ID = 101;
```

#### Get All Students in a Section

```sql
SELECT s.Student_ID, s.Name
FROM Student s
JOIN Enrollment e ON s.Student_ID = e.Student_ID
WHERE e.Section_ID = 1;
```

#### Get Grades for a Student in All Courses

```sql
SELECT c.Course_Name, g.Grade_Value
FROM Grade g
JOIN Course c ON g.Course_ID = c.Course_ID
WHERE g.Student_ID = 1;
```

#### Get Attendance for a Student in All Sections

```sql
SELECT sec.Section_ID, a.Date, a.Status
FROM Attendance a
JOIN Section sec ON a.Section_ID = sec.Section_ID
WHERE a.Student_ID = 1;
```

---
