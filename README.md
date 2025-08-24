# Problem-Solving-Case---BookMyShow
SQL case study inspired by BookMyShow. Includes normalized database design (1NF–BCNF), sample data, and queries to fetch shows and timings for a given theatre and date.

# Detailed Description:-
This project is a database design and SQL case study inspired by BookMyShow, a popular movie ticket booking platform.

 Part 1 (P1)
Identification of entities, attributes, and relationships.
Creation of normalized database structures (1NF → 2NF → 3NF → BCNF).
SQL scripts to create tables and insert sample data.

 Part 2 (P2)
SQL query to list all shows for a given theatre on a selected date, along with their show timings.

# Solution
Part 1 (P1) – Database Design

**Objectives:**

- Identify entities, attributes, and relationships.
- Create normalized table structures (1NF → 2NF → 3NF → BCNF).
- Write SQL scripts to create tables and insert sample data.

**Example Entities & Attributes:**

| Entity   | Attributes                                      |
|----------|-----------------------------------------------|
| Theatre  | TheatreID, Name, Location                      |
| Movie    | MovieID, Title, Duration, Language, Genre     |
| Show     | ShowID, MovieID, TheatreID, ShowDate, StartTime, EndTime |
| Ticket   | TicketID, ShowID, SeatNumber, Price           |
| Customer | CustomerID, Name, Email                        |

**Sample Table Creation (SQL):**

```sql
CREATE TABLE Theatre (
    TheatreID INT PRIMARY KEY,
    Name VARCHAR(100),
    Location VARCHAR(100)
);

CREATE TABLE Movie (
    MovieID INT PRIMARY KEY,
    Title VARCHAR(100),
    Duration INT,
    Language VARCHAR(50),
    Genre VARCHAR(50)
);

CREATE TABLE Show (
    ShowID INT PRIMARY KEY,
    MovieID INT,
    TheatreID INT,
    ShowDate DATE,
    StartTime TIME,
    EndTime TIME,
    FOREIGN KEY (MovieID) REFERENCES Movie(MovieID),
    FOREIGN KEY (TheatreID) REFERENCES Theatre(TheatreID)
);

CREATE TABLE Ticket (
    TicketID INT PRIMARY KEY,
    ShowID INT,
    SeatNumber VARCHAR(10),
    Price DECIMAL(10,2),
    FOREIGN KEY (ShowID) REFERENCES Show(ShowID)
);

CREATE TABLE Customer (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100),
    Email VARCHAR(100)
);


##  Sample Data

This section contains **sample entries** for all tables in the BookMyShow database to help test queries and relationships.

---

###  Theatre

| TheatreID | Name        | Location   |
|-----------|------------|-----------|
| 1         | PVR Cinemas | Amritsar  |
| 2         | Cinepolis   | Delhi     |
| 3         | INOX       | Mumbai    |

**SQL Insert Example:**
```sql
INSERT INTO Theatre VALUES (1, 'PVR Cinemas', 'Amritsar');
INSERT INTO Theatre VALUES (2, 'Cinepolis', 'Delhi');
INSERT INTO Theatre VALUES (3, 'INOX', 'Mumbai');

### Movie

| MovieID | Title     | Duration | Language | Genre  |
| ------- | --------- | -------- | -------- | ------ |
| 1       | Inception | 148      | English  | Sci-Fi |
| 2       | Dangal    | 161      | Hindi    | Drama  |
| 3       | Avengers  | 180      | English  | Action |

```sql
INSERT INTO Movie VALUES (1, 'Inception', 148, 'English', 'Sci-Fi');
INSERT INTO Movie VALUES (2, 'Dangal', 161, 'Hindi', 'Drama');
INSERT INTO Movie VALUES (3, 'Avengers', 180, 'English', 'Action');


### Show

| ShowID | MovieID | TheatreID | ShowDate   | StartTime | EndTime |
| ------ | ------- | --------- | ---------- | --------- | ------- |
| 1      | 1       | 1         | 2025-08-24 | 18:00     | 20:30   |
| 2      | 2       | 2         | 2025-08-24 | 15:00     | 17:45   |
| 3      | 3       | 3         | 2025-08-24 | 20:00     | 23:00   |

```sql
INSERT INTO Show VALUES (1, 1, 1, '2025-08-24', '18:00', '20:30');
INSERT INTO Show VALUES (2, 2, 2, '2025-08-24', '15:00', '17:45');
INSERT INTO Show VALUES (3, 3, 3, '2025-08-24', '20:00', '23:00');

### Ticket
| TicketID | ShowID | SeatNumber | Price  |
| -------- | ------ | ---------- | ------ |
| 1        | 1      | A1         | 250.00 |
| 2        | 1      | A2         | 250.00 |
| 3        | 2      | B1         | 200.00 |

```sql
INSERT INTO Ticket VALUES (1, 1, 'A1', 250.00);
INSERT INTO Ticket VALUES (2, 1, 'A2', 250.00);
INSERT INTO Ticket VALUES (3, 2, 'B1', 200.00);

### Customer
| CustomerID | Name  | Email                                         |
| ---------- | ----- | --------------------------------------------- |
| 1          | R M   | [rm@example.com]     |
| 2          | Pooja | [pooja@example.com] |
| 3          | Aman  | [aman@example.com]  |

```sql
INSERT INTO Customer VALUES (1, 'R M', 'rm@example.com');
INSERT INTO Customer VALUES (2, 'Pooja', 'pooja@example.com');
INSERT INTO Customer VALUES (3, 'Aman', 'aman@example.com');


##  Part 2 (P2) – Fetch Shows

**Objective:**  
List all shows for a given theatre on a selected date, including show timings.

**SQL Query Example:**

```sql
SELECT 
    s.ShowID,
    m.Title AS MovieName,
    t.Name AS TheatreName,
    s.ShowDate,
    s.StartTime,
    s.EndTime
FROM Show s
JOIN Movie m ON s.MovieID = m.MovieID
JOIN Theatre t ON s.TheatreID = t.TheatreID
WHERE s.TheatreID = 1
  AND s.ShowDate = '2025-08-24';

**Sample Output:**

| ShowID | MovieName | TheatreName | ShowDate   | StartTime | EndTime |
|--------|-----------|------------|------------|-----------|---------|
| 1      | Inception | PVR Cinemas | 2025-08-24 | 18:00     | 20:30   |

