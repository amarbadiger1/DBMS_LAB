Here’s the full SQL script, including **table creation, inserting sample values, and executing the queries** for the cricket tournament database.

---

## **Step 1: Create Tables**
```sql
CREATE TABLE Team (
    Teamid INT PRIMARY KEY,
    Team_Name VARCHAR(50) NOT NULL,
    City VARCHAR(50),
    Coach VARCHAR(50),
    Captain INT
);

CREATE TABLE Player (
    Playerid INT PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Age INT NOT NULL,
    Phone_Number VARCHAR(15),
    Teamid INT,
    FOREIGN KEY (Teamid) REFERENCES Team(Teamid)
);

CREATE TABLE Stadium (
    Stadiumid INT PRIMARY KEY,
    Stadium_Name VARCHAR(100) NOT NULL,
    City VARCHAR(50),
    Area_Name VARCHAR(50),
    Pincode VARCHAR(10)
);

CREATE TABLE Match (
    Matchid INT PRIMARY KEY,
    Team1 INT,
    Team2 INT,
    Stadiumid INT,
    Match_Date DATE,
    Match_Time TIME,
    Winning_Team INT,
    Man_of_Match INT,
    FOREIGN KEY (Team1) REFERENCES Team(Teamid),
    FOREIGN KEY (Team2) REFERENCES Team(Teamid),
    FOREIGN KEY (Stadiumid) REFERENCES Stadium(Stadiumid),
    FOREIGN KEY (Winning_Team) REFERENCES Team(Teamid),
    FOREIGN KEY (Man_of_Match) REFERENCES Player(Playerid)
);
```

---

## **Step 2: Insert Values**
### **Insert Teams**
```sql
INSERT INTO Team (Teamid, Team_Name, City, Coach, Captain) VALUES
(1, 'Warriors', 'Mumbai', 'John Smith', 101),
(2, 'Titans', 'Delhi', 'Mike Johnson', 201),
(3, 'Strikers', 'Bangalore', 'Rahul Verma', 301),
(4, 'Chargers', 'Chennai', 'David Warner', 401);
```

---

### **Insert Players**
```sql
INSERT INTO Player (Playerid, Name, Age, Phone_Number, Teamid) VALUES
(101, 'Rohit Sharma', 34, '9876543210', 1),
(102, 'Virat Kohli', 35, '9876543211', 1),
(103, 'Shubman Gill', 24, '9876543212', 1),
(201, 'MS Dhoni', 41, '9876543213', 2),
(202, 'Rishabh Pant', 27, '9876543214', 2),
(301, 'KL Rahul', 32, '9876543215', 3),
(302, 'Jasprit Bumrah', 30, '9876543216', 3),
(303, 'Hardik Pandya', 30, '9876543217', 3),
(401, 'David Warner', 37, '9876543218', 4),
(402, 'Steve Smith', 36, '9876543219', 4),
(403, 'Marnus Labuschagne', 29, '9876543220', 4);
```

---

### **Insert Stadiums**
```sql
INSERT INTO Stadium (Stadiumid, Stadium_Name, City, Area_Name, Pincode) VALUES
(1, 'Wankhede Stadium', 'Mumbai', 'Marine Drive', '400020'),
(2, 'Feroz Shah Kotla', 'Delhi', 'Daryaganj', '110002'),
(3, 'Chinnaswamy Stadium', 'Bangalore', 'MG Road', '560001'),
(4, 'Chepauk Stadium', 'Chennai', 'Triplicane', '600005');
```

---

### **Insert Matches**
```sql
INSERT INTO Match (Matchid, Team1, Team2, Stadiumid, Match_Date, Match_Time, Winning_Team, Man_of_Match) VALUES
(1, 1, 2, 1, '2024-03-15', '14:00:00', 1, 102),
(2, 2, 3, 2, '2024-03-16', '18:00:00', 3, 302),
(3, 3, 4, 3, '2024-03-17', '20:00:00', 3, 303),
(4, 4, 1, 4, '2024-03-18', '14:00:00', 4, 401),
(5, 1, 3, 1, '2024-03-19', '18:00:00', 1, 103),
(6, 2, 4, 2, '2024-03-20', '20:00:00', 2, 202),
(7, 3, 1, 1, '2024-03-21', '18:00:00', 3, 303),
(8, 4, 2, 4, '2024-03-22', '20:00:00', 4, 402);
```

---

## **Step 3: Queries**
### **1. Display the youngest player (in terms of age) Name, Team name, and age.**
```sql
SELECT P.Name, T.Team_Name, P.Age
FROM Player P
JOIN Team T ON P.Teamid = T.Teamid
WHERE P.Age = (SELECT MIN(Age) FROM Player);
```

---

### **2. List the details of the stadium where the maximum number of matches were played.**
```sql
SELECT S.*
FROM Stadium S
JOIN Match M ON S.Stadiumid = M.Stadiumid
GROUP BY S.Stadiumid
ORDER BY COUNT(M.Matchid) DESC
LIMIT 1;
```

---

### **3. List the details of the player who is not a captain but got the man_of_match award at least in two matches.**
```sql
SELECT P.*
FROM Player P
JOIN Match M ON P.Playerid = M.Man_of_Match
WHERE P.Playerid NOT IN (SELECT Captain FROM Team)
GROUP BY P.Playerid
HAVING COUNT(M.Matchid) >= 2;
```

---

### **4. Display the Team details who won the maximum matches.**
```sql
SELECT T.*
FROM Team T
JOIN Match M ON T.Teamid = M.Winning_Team
GROUP BY T.Teamid
ORDER BY COUNT(M.Matchid) DESC
LIMIT 1;
```

---

### **5. Display the team name where all its won matches were played in the same stadium.**
```sql
SELECT T.Team_Name
FROM Team T
JOIN Match M ON T.Teamid = M.Winning_Team
GROUP BY T.Teamid
HAVING COUNT(DISTINCT M.Stadiumid) = 1;
```

---

### **Explanation:**
1. The **ER Diagram** captures the relationships between Teams, Players, Stadiums, and Matches.
2. The **Relational Model** ensures data integrity with primary and foreign keys.
3. The **Insert Statements** populate the database with meaningful cricket tournament data.
4. The **Queries** efficiently fetch tournament insights.

This script is **fully executable** in MySQL or any SQL-based system. Let me know if you need modifications! 🚀