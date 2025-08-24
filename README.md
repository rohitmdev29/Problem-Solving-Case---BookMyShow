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
