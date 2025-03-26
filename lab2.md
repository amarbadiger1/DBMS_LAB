Here’s the SQL script for creating the **STUDENT** table, inserting sample data, and executing the required queries.

---

## **Step 1: Create the Table**
```sql
CREATE TABLE STUDENT (
    USN VARCHAR(10) PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Date_of_Birth DATE NOT NULL,
    Branch VARCHAR(50) NOT NULL,
    Mark1 INT,
    Mark2 INT,
    Mark3 INT,
    Total INT,
    GPA DECIMAL(3,2)
);
```

---

## **Step 2: Insert Sample Data**
```sql
INSERT INTO STUDENT (USN, Name, Date_of_Birth, Branch, Mark1, Mark2, Mark3, Total, GPA) VALUES
('1001', 'Sam', '2002-06-15', 'CSE', 85, 90, 88, NULL, NULL),
('1002', 'Sara', '2001-04-20', 'ECE', 80, 78, 85, NULL, NULL),
('1003', 'Arjun', '2003-09-10', 'MECH', 75, 85, 80, NULL, NULL),
('1004', 'Suman', '2000-12-25', 'CSE', 95, 92, 88, NULL, NULL),
('1005', 'Vikram', '2002-03-18', 'ECE', 88, 85, 90, NULL, NULL);
```

---

## **Step 3: Execute Queries**
### **1. Update the column total by adding mark1, mark2, and mark3**
```sql
UPDATE STUDENT
SET Total = Mark1 + Mark2 + Mark3;
```

---

### **2. Find the GPA score of all students**
_Assume GPA is calculated as `(Total / 30)`, where each mark is out of 100._  
```sql
UPDATE STUDENT
SET GPA = Total / 30;
```

_To retrieve the GPA:_
```sql
SELECT USN, Name, GPA FROM STUDENT;
```

---

### **3. Find the students who were born in a particular year (e.g., 2002)**
```sql
SELECT * FROM STUDENT
WHERE YEAR(Date_of_Birth) = 2002;
```

---

### **4. List the students who are studying in a particular branch (e.g., 'CSE')**
```sql
SELECT * FROM STUDENT
WHERE Branch = 'CSE';
```

---

### **5. Find the maximum GPA score of the student branch-wise**
```sql
SELECT Branch, MAX(GPA) AS Max_GPA
FROM STUDENT
GROUP BY Branch;
```

---

### **6. Find the students whose name starts with the alphabet "S"**
```sql
SELECT * FROM STUDENT
WHERE Name LIKE 'S%';
```

---

### **7. Find the students whose name ends with the alphabets "AR"**
```sql
SELECT * FROM STUDENT
WHERE Name LIKE '%AR';
```

---

### **8. Delete the student details whose USN is '1001'**
```sql
DELETE FROM STUDENT
WHERE USN = '1001';
```

---

This script **creates the STUDENT table, inserts sample data, updates the total and GPA columns, and executes the required queries**. Let me know if you need any modifications! 🚀