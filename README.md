# Tarea 02 - SQL Bolt (Brando Guizado)

Enlace del cuestionario de SQL
[SQLBolt](https://sqlbolt.com/ "Da click al enlace y divertete")

---

### SQL Lesson 1: SELECT queries 101

**Respuestas del Ejercicio 01**

1. Find the title of each film
    ```SQL
    SELECT Title FROM movies;
    ```
2. Find the director of each film
    ```SQL
    SELECT Director FROM movies;
    ```
3. Find the title and director of each film
    ```SQL
    SELECT Title, Director FROM movies;
    ```
4. Find the title and year of each film
    ```SQL
    SELECT Title, Year FROM movies;
    ```
5. Find all the information about each film
    ```SQL
    SELECT * FROM movies;
    ```
---

### SQL Lesson 2: Queries with constraints (Pt. 1)

**Respuestas del Ejercicio 02**

1. Find the movie with a row id of 6
    ```SQL
    SELECT Title FROM movies Where id = 6;
    ```
2. Find the movies released in the years between 2000 and 2010
    ```SQL
    SELECT Title FROM movies Where Year >= 2000 and Year <= 2010;
    ```
3. Find the movies not released in the years between 2000 and 2010
    ```SQL
    SELECT Title FROM movies WHERE YEAR NOT BETWEEN 2000 and 2010;
    ```
4. Find the first 5 Pixar movies and their release year
    ```SQL
    SELECT * FROM movies WHERE year LIMIT 5;
    ```
---

### SQL Lesson 3: Queries with constraints (Pt. 2)

**Respuestas del Ejercicio 03**

1. Find all the Toy Story movies
    ```SQL
    SELECT Title FROM Movies WHERE Title LIKE "Toy story%"
    ```
2. Find all the movies directed by John Lasseter
    ```SQL
    SELECT Title FROM Movies WHERE Director = "John Lasseter";
    ```
3. Find all the movies (and director) not directed by John Lasseter
    ```SQL
    SELECT Title, Director FROM Movies WHERE Director != "John Lasseter";
    ```
4. Find all the WALL-* movies
    ```SQL
    SELECT * FROM movies WHERE Title LIKE "%wall-%";
    ```
---

### SQL Lesson 4: Filtering and sorting Query results

**Respuestas del Ejercicio 04**

1. List all directors of Pixar movies (alphabetically), without duplicates
    ```SQL
    SELECT DISTINCT Director FROM movies ORDER BY Director ASC;
    ```
2. List the last four Pixar movies released (ordered from most recent to least)
    ```SQL
    SELECT Title FROM movies ORDER BY Year DESC LIMIT 4;
    ```
3. List the first five Pixar movies sorted alphabetically
    ```SQL
    SELECT Title FROM movies ORDER BY Title ASC LIMIT 5;
    ```
4. List the next five Pixar movies sorted alphabetically
    ```SQL
    SELECT Title FROM movies ORDER BY Title ASC LIMIT 5 OFFSET 5;
    ```
---

### SQL Lesson 5: Review Simple SELECT Queries

**Respuestas del Ejercicio 05**

1. List all the Canadian cities and their populations
    ```SQL
    SELECT City, Population FROM north_american_cities WHERE Country = "Canada";
    ```
2. Order all the cities in the United States by their latitude from north to south
    ```SQL
    SELECT City FROM north_american_cities WHERE Country = "United States" ORDER BY Latitude DESC;
    ```
3. List all the cities west of Chicago, ordered from west to east
    ```SQL
    SELECT City FROM north_american_cities WHERE Longitude < -87.629798 ORDER BY Longitude;
    ```
4. List the two largest cities in Mexico (by population)
    ```SQL
    SELECT City FROM north_american_cities WHERE Country = "Mexico" ORDER BY Population DESC LIMIT 02;
    ```
5. List the third and fourth largest cities (by population) in the United States and their population
    ```SQL
    SELECT City FROM north_american_cities WHERE Country = "United States" ORDER BY Population DESC LIMIT 02 OFFSET 02;
    ```
---

### SQL Lesson 6: Multi-table queries with JOINs

**Respuestas del Ejercicio 06**

1. Find the domestic and international sales for each movie
    ```SQL
    SELECT Title, Domestic_sales, International_sales FROM movies INNER JOIN Boxoffice ON Id = Movie_id;
    ```
2. Show the sales numbers for each movie that did better internationally rather than domestically
    ```SQL
    SELECT Title, Domestic_sales, International_sales FROM movies INNER JOIN Boxoffice ON Id = Movie_id WHERE International_sales > Domestic_sales;
    ```
3. List all the movies by their ratings in descending order
    ```SQL
    SELECT Title, Rating FROM movies INNER JOIN Boxoffice ON Id = Movie_id ORDER BY Rating DESC;
    ```
---

### SQL Lesson 7: OUTER JOINs

**Respuestas del Ejercicio 07**

1. Find the list of all buildings that have employees
    ```SQL
    SELECT DISTINCT Building FROM Employees LEFT JOIN Buildings ON Building = Building_name;
    ```
2. Find the list of all buildings and their capacity
    ```SQL
    SELECT DISTINCT Building_name, Capacity FROM employees LEFT JOIN Buildings;
    ```
3. List all buildings and the distinct employee roles in each building (including empty buildings)
    ```SQL
    SELECT DISTINCT Building_name, Role FROM buildings LEFT JOIN Employees ON Building_name = Building;
    ```
---

### SQL Lesson 8: A short note on NULLs

**Respuestas del Ejercicio 08**

1. Find the name and role of all employees who have not been assigned to a building
    ```SQL
    SELECT Name, Role FROM employees WHERE Building IS NULL;    
    ```
2. Find the names of the buildings that hold no employees
    ```SQL
    SELECT Building_name FROM Buildings LEFT JOIN Employees ON Building_name = Building WHERE Name IS NULL;  
    ```
---

### SQL Lesson 9: Queries with expressions

**Respuestas del Ejercicio 09**

1. List all movies and their combined sales in millions of dollars 
    ```SQL
    SELECT Title, (Domestic_sales + International_sales)/1000000 AS Sales FROM movies LEFT JOIN Boxoffice ON Id = Movie_id;  
    ```
2. List all movies and their ratings in percent
    ```SQL
    SELECT Title, Rating*10 AS Rating_percent FROM movies LEFT JOIN Boxoffice ON Id = Movie_id;
    ```
3. List all movies that were released on even number years
    ```SQL
    SELECT * FROM movies LEFT JOIN Boxoffice ON Id = Movie_id WHERE Year % 2 = 0;
    ```
---

### SQL Lesson 10: Queries with aggregates (Pt. 1)

**Respuestas del Ejercicio 10**

1. List all movies and their combined sales in millions of dollars 
    ```SQL
    SELECT Name, MAX(Years_employed) AS Longest_time FROM employees;
    ```
2. For each role, find the average number of years employed by employees in that role
    ```SQL
    SELECT Role, AVG(Years_employed) AS Average_Year FROM employees GROUP BY Role;
    ```
3. Find the total number of employee years worked in each building
    ```SQL
    SELECT Building, SUM(Years_employed) AS Years_worked FROM employees GROUP BY Building;
    ```
---

### SQL Lesson 11: Queries with aggregates (Pt. 2)

**Respuestas del Ejercicio 11**

1. Find the number of Artists in the studio (without a HAVING clause)
    ```SQL
    SELECT Count(Name) AS Number_Artists FROM employees WHERE Role = "Artist" GROUP BY Role;
    ```
2. Find the number of Employees of each role in the studio
    ```SQL
    SELECT Role, COUNT(Name) AS Number_employees FROM employees GROUP BY Role;
    ```
3. Find the total number of years employed by all Engineers
    ```SQL
    SELECT Role, SUM(Years_employed) FROM employees WHERE Role = "Engineer" GROUP BY Role;
    ```

### SQL Lesson 12: Order of execution of a Query

**Respuestas del Ejercicio 12**

1. Find the number of movies each director has directed
    ```SQL
    SELECT Director, COUNT(Title) AS Movies_directed FROM movies GROUP BY Director;
    ```

2. Find the total domestic and international sales that can be attributed to each director
    ```SQL
    SELECT Director, SUM(Domestic_sales + International_sales) AS Sales FROM movies LEFT JOIN Boxoffice ON Id = Movie_id GROUP BY Director;
    ```
---

### SQL Lesson 13: Inserting rows

**Respuestas del Ejercicio 13**

1. Add the studio's new production, Toy Story 4 to the list of movies (you can use any director)
    ```SQL
    INSERT INTO Movies (Id, Title, Director, Year, Length_minutes) VALUES (15, "Toy Story 4", "Lee Unkrich", 2023, 110)
    ```
2. Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the BoxOffice table.
    ```SQL
    INSERT INTO Boxoffice (Movie_id, Rating, Domestic_sales, International_sales) VALUES (15, 8.7, 340000000, 270000000)
    ```
---

### SQL Lesson 14: Updating rows

**Respuestas del Ejercicio 14**

1. The director for A Bug's Life is incorrect, it was actually directed by John Lasseter 
    ```SQL
    UPDATE Movies SET Director = "John Lasseter" WHERE Id = 2;
    ```
2. The year that Toy Story 2 was released is incorrect, it was actually released in 1999
    ```SQL
    UPDATE Movies SET Year = "1999" WHERE Id = 3;
    ```
3. Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich 
    ```SQL
    UPDATE Movies SET Title = "Toy Story 3", Director = "Lee Unkrich" WHERE Id = 11;
    ```
---

### SQL Lesson 15: Deleting rows

**Respuestas del Ejercicio 15**

1. This database is getting too big, lets remove all movies that were released before 2005.
    ```SQL
    DELETE FROM Movies WHERE Year < 2005;
    ```
2. Andrew Stanton has also left the studio, so please remove all movies directed by him.
    ```SQL
    DELETE FROM Movies WHERE Director = "Andrew Stanton";
    ```
---

### SQL Lesson 16: Creating tables

**Respuestas del Ejercicio 16**

1. Create a new table named Database with the following columns:
– Name A string (text) describing the name of the database
– Version A number (floating point) of the latest version of this database
– Download_count An integer count of the number of times this database was downloaded
This table has no constraints.
    ```SQL
    CREATE TABLE Database (Name TEXT, Version FLOAT, Download_Count INTEGER);
    ```
---

### SQL Lesson 17: Altering tables

**Respuestas del Ejercicio 17**

1. Add a column named Aspect_ratio with a FLOAT data type to store the aspect-ratio each movie was released in.
    ```SQL
    ALTER TABLE Movies ADD COLUMN Aspect_ratio FLOAT;
    ```
2. Add another column named Language with a TEXT data type to store the language that the movie was released in. Ensure that the default for this language is English.
    ```SQL
    ALTER TABLE Movies ADD COLUMN Language TEXT DEFAULT "English";
    ```
---

### SQL Lesson 18: Dropping tables

**Respuestas del Ejercicio 18**

1. We've sadly reached the end of our lessons, lets clean up by removing the Movies table
    ```SQL
    DROP TABLE Movies;
    ```
2. And drop the BoxOffice table as well
    ```SQL
    DROP TABLE BoxOffice;
    ```
---

![testFinalizado](https://sqlbolt.com/cs/images/sqlbolt_complete.png)