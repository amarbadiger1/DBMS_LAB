Here’s the SQL script for **creating tables, inserting sample data, and executing the required queries** for the student enrollment and book adoption database.

---

## **Step 1: Create Tables**
```sql
CREATE TABLE STUDENT (
    regno VARCHAR(10) PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    major VARCHAR(50) NOT NULL,
    bdate DATE NOT NULL
);

CREATE TABLE COURSE (
    course_no INT PRIMARY KEY,
    cname VARCHAR(50) NOT NULL,
    dept VARCHAR(50) NOT NULL
);

CREATE TABLE TEXT (
    book_ISBN INT PRIMARY KEY,
    book_title VARCHAR(100) NOT NULL,
    publisher VARCHAR(50) NOT NULL,
    author VARCHAR(50) NOT NULL
);

CREATE TABLE ENROLL (
    regno VARCHAR(10),
    course_no INT,
    sem INT,
    marks INT,
    PRIMARY KEY (regno, course_no, sem),
    FOREIGN KEY (regno) REFERENCES STUDENT(regno),
    FOREIGN KEY (course_no) REFERENCES COURSE(course_no)
);

CREATE TABLE BOOK_ADOPTION (
    course_no INT,
    sem INT,
    book_ISBN INT,
    PRIMARY KEY (course_no, sem, book_ISBN),
    FOREIGN KEY (course_no) REFERENCES COURSE(course_no),
    FOREIGN KEY (book_ISBN) REFERENCES TEXT(book_ISBN)
);
```

---

## **Step 2: Insert Sample Data**
### **Insert Students**
```sql
INSERT INTO STUDENT (regno, name, major, bdate) VALUES
('S101', 'Alice', 'CSE', '2002-06-15'),
('S102', 'Bob', 'ECE', '2001-04-20'),
('S103', 'Charlie', 'MECH', '2003-09-10'),
('S104', 'David', 'CSE', '2000-12-25'),
('S105', 'Eve', 'ECE', '2002-03-18'),
('S106', 'Frank', 'MECH', '2001-08-08'),
('S107', 'Grace', 'CSE', '2003-07-25');
```

---

### **Insert Courses**
```sql
INSERT INTO COURSE (course_no, cname, dept) VALUES
(101, 'Database Systems', 'CSE'),
(102, 'Operating Systems', 'CSE'),
(103, 'Electronics', 'ECE'),
(104, 'Microprocessors', 'ECE'),
(105, 'Mechanics', 'MECH'),
(106, 'Thermodynamics', 'MECH');
```

---

### **Insert Books**
```sql
INSERT INTO TEXT (book_ISBN, book_title, publisher, author) VALUES
(1001, 'Database Fundamentals', 'Pearson', 'Elmasri'),
(1002, 'Operating Systems Concepts', 'Wiley', 'Silberschatz'),
(1003, 'Digital Electronics', 'McGraw-Hill', 'Morris Mano'),
(1004, 'Microprocessor Systems', 'Pearson', 'Ramesh Gaonkar'),
(1005, 'Engineering Mechanics', 'McGraw-Hill', 'Timoshenko'),
(1006, 'Thermal Engineering', 'Oxford', 'Rajput'),
(1007, 'Computer Networks', 'Pearson', 'Andrew Tanenbaum');
```

---

### **Insert Enrollments**
```sql
INSERT INTO ENROLL (regno, course_no, sem, marks) VALUES
('S101', 101, 2, 85),
('S102', 103, 2, 78),
('S103', 105, 3, 90),
('S104', 102, 2, 88),
('S105', 104, 3, 75),
('S106', 106, 3, 80),
('S107', 101, 2, 95),
('S101', 102, 2, 82),
('S103', 106, 3, 89),
('S104', 101, 2, 91);
```

---

### **Insert Book Adoptions**
```sql
INSERT INTO BOOK_ADOPTION (course_no, sem, book_ISBN) VALUES
(101, 2, 1001),
(102, 2, 1002),
(103, 2, 1003),
(104, 3, 1004),
(105, 3, 1005),
(106, 3, 1006),
(101, 2, 1007);
```

---

## **Step 3: Queries**
### **1. List student details along with their course details ordered by semester**
```sql
SELECT S.*, C.cname, E.sem, E.marks
FROM STUDENT S
JOIN ENROLL E ON S.regno = E.regno
JOIN COURSE C ON E.course_no = C.course_no
ORDER BY E.sem;
```

---

### **2. List student details in a particular department, ordered by semester**  
_(Example: 'CSE' department)_
```sql
SELECT S.*, C.cname, E.sem, E.marks
FROM STUDENT S
JOIN ENROLL E ON S.regno = E.regno
JOIN COURSE C ON E.course_no = C.course_no
WHERE C.dept = 'CSE'
ORDER BY E.sem;
```

---

### **3. List all book details for a particular course**  
_(Example: Course 101)_
```sql
SELECT T.*
FROM TEXT T
JOIN BOOK_ADOPTION B ON T.book_ISBN = B.book_ISBN
WHERE B.course_no = 101;
```

---

### **4. Find courses where more than 2 students are enrolled**
```sql
SELECT C.course_no, C.cname, COUNT(E.regno) AS Student_Count
FROM COURSE C
JOIN ENROLL E ON C.course_no = E.course_no
GROUP BY C.course_no
HAVING COUNT(E.regno) > 2;
```

---

### **5. Find publishers who have published more than 2 books**
```sql
SELECT publisher, COUNT(book_ISBN) AS Total_Books
FROM TEXT
GROUP BY publisher
HAVING COUNT(book_ISBN) > 2;
```

---

### **Final Notes**
- The **database structure** ensures relationships between students, courses, enrollments, books, and book adoptions.
- **Primary and foreign keys** maintain integrity.
- **Sample data** is provided for easy testing.
- **Queries cover enrollment details, department-wise students, book adoption, popular courses, and major publishers.**

This script is **fully executable** in MySQL or any SQL-based system. Let me know if you need modifications! 🚀