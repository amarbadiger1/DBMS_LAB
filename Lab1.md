Here’s the full SQL script, including table creation, inserting sample values, and executing the queries.  

---

## **Creating Tables**  

```sql
CREATE TABLE BRANCH (
    Branchid INT PRIMARY KEY,
    Branchname VARCHAR(50) NOT NULL,
    HOD VARCHAR(50) NOT NULL
);

CREATE TABLE STUDENT (
    USN VARCHAR(10) PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Address VARCHAR(100),
    Branchid INT,
    Sem INT,
    FOREIGN KEY (Branchid) REFERENCES BRANCH(Branchid)
);

CREATE TABLE AUTHOR (
    Authorid INT PRIMARY KEY,
    Authorname VARCHAR(50) NOT NULL,
    Country VARCHAR(50),
    Age INT
);

CREATE TABLE BOOK (
    Bookid INT PRIMARY KEY,
    Bookname VARCHAR(100) NOT NULL,
    Authorid INT,
    Publisher VARCHAR(100),
    Branchid INT,
    FOREIGN KEY (Authorid) REFERENCES AUTHOR(Authorid),
    FOREIGN KEY (Branchid) REFERENCES BRANCH(Branchid)
);

CREATE TABLE BORROW (
    USN VARCHAR(10),
    Bookid INT,
    Borrowed_Date DATE,
    PRIMARY KEY (USN, Bookid),
    FOREIGN KEY (USN) REFERENCES STUDENT(USN),
    FOREIGN KEY (Bookid) REFERENCES BOOK(Bookid)
);
```

---

## **Inserting Data**  

### **Inserting Branches**  

```sql
INSERT INTO BRANCH (Branchid, Branchname, HOD) VALUES
(1, 'MCA', 'Dr. Smith'),
(2, 'CSE', 'Dr. Johnson'),
(3, 'ECE', 'Dr. Williams');
```

---

### **Inserting Students**  

```sql
INSERT INTO STUDENT (USN, Name, Address, Branchid, Sem) VALUES
('S101', 'Alice', 'New York', 1, 2),
('S102', 'Bob', 'Los Angeles', 1, 2),
('S103', 'Charlie', 'Chicago', 2, 3),
('S104', 'David', 'Houston', 2, 4),
('S105', 'Eve', 'San Francisco', 3, 2);
```

---

### **Inserting Authors**  

```sql
INSERT INTO AUTHOR (Authorid, Authorname, Country, Age) VALUES
(1, 'J.K. Rowling', 'UK', 55),
(2, 'George Orwell', 'UK', 46),
(3, 'Mark Twain', 'USA', 74),
(4, 'Jane Austen', 'UK', 41);
```

---

### **Inserting Books**  

```sql
INSERT INTO BOOK (Bookid, Bookname, Authorid, Publisher, Branchid) VALUES
(101, 'Harry Potter', 1, 'Bloomsbury', 1),
(102, '1984', 2, 'Secker & Warburg', 1),
(103, 'The Adventures of Tom Sawyer', 3, 'American Publishing', 2),
(104, 'Pride and Prejudice', 4, 'T. Egerton', 2),
(105, 'Animal Farm', 2, 'Secker & Warburg', 3);
```

---

### **Inserting Borrowed Books**  

```sql
INSERT INTO BORROW (USN, Bookid, Borrowed_Date) VALUES
('S101', 101, '2024-03-10'),
('S101', 102, '2024-03-15'),
('S102', 102, '2024-03-12'),
('S102', 105, '2024-03-20'),
('S103', 103, '2024-03-05'),
('S103', 104, '2024-03-08'),
('S104', 104, '2024-03-18'),
('S105', 101, '2024-03-25');
```

---

## **Queries**  

### **1. List the details of Students who are all Studying in 2nd sem MCA**  

```sql
SELECT * FROM STUDENT
WHERE Sem = 2 AND Branchid = (SELECT Branchid FROM BRANCH WHERE Branchname = 'MCA');
```

---

### **2. List the students who have not borrowed any books**  

```sql
SELECT * FROM STUDENT
WHERE USN NOT IN (SELECT DISTINCT USN FROM BORROW);
```

---

### **3. Display the USN, Student name, Branch_name, Book_name, Author_name, Books_Borrowed_Date of 2nd sem MCA Students who borrowed books**  

```sql
SELECT S.USN, S.Name, B.Branchname, BK.Bookname, A.Authorname, BO.Borrowed_Date
FROM STUDENT S
JOIN BORROW BO ON S.USN = BO.USN
JOIN BOOK BK ON BO.Bookid = BK.Bookid
JOIN AUTHOR A ON BK.Authorid = A.Authorid
JOIN BRANCH B ON S.Branchid = B.Branchid
WHERE S.Sem = 2 AND B.Branchname = 'MCA';
```

---

### **4. Display the number of books written by each Author**  

```sql
SELECT A.Authorid, A.Authorname, COUNT(B.Bookid) AS TotalBooks
FROM AUTHOR A
JOIN BOOK B ON A.Authorid = B.Authorid
GROUP BY A.Authorid, A.Authorname;
```

---

### **5. Display the student details who borrowed more than two books**  

```sql
SELECT S.*
FROM STUDENT S
JOIN BORROW B ON S.USN = B.USN
GROUP BY S.USN
HAVING COUNT(B.Bookid) > 2;
```

---

### **6. Display the student details who borrowed books of more than one Author**  

```sql
SELECT S.*
FROM STUDENT S
JOIN BORROW B ON S.USN = B.USN
JOIN BOOK BK ON B.Bookid = BK.Bookid
GROUP BY S.USN
HAVING COUNT(DISTINCT BK.Authorid) > 1;
```

---

### **7. Display the Book names in descending order of their names**  

```sql
SELECT Bookname FROM BOOK ORDER BY Bookname DESC;
```

---

### **8. List the details of students who borrowed the books which are all published by the same Publisher**  

```sql
SELECT S.*
FROM STUDENT S
JOIN BORROW B ON S.USN = B.USN
JOIN BOOK BK ON B.Bookid = BK.Bookid
WHERE BK.Publisher IN (
    SELECT Publisher FROM BOOK GROUP BY Publisher HAVING COUNT(Bookid) > 1
);
```

---

This script fully sets up the database, inserts data, and runs queries. Let me know if you need any changes! 🚀