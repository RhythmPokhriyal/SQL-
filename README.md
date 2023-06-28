    ------
# SQL PROJECT - DATA MANIPULATION
------
## This project covers

####    1 - Creating a Database
####    2 - Creating Multiple tables
####    3 - Entering records in the tables
####    4 - Show of tables, structure of tables
####    5 - JOINS (INNER, LEFT), Aggregate Functions, IFNULL, CASE, IF, Sorting

-----------

## Create a new Database named as 'revs'

    CREATE DATABASE revs;
    
  ![DB](https://user-images.githubusercontent.com/119749518/215277864-28df7ddc-9656-474e-a07f-dc388de6da26.png)


## Creating 3 new tables in the newly created database

    CREATE TABLE reviewers (
        id INT PRIMARY KEY AUTO_INCREMENT,
        first_name VARCHAR(50) NOT NULL,
        last_name VARCHAR(50) NOT NULL
    );
 
    CREATE TABLE series (
        id INT PRIMARY KEY AUTO_INCREMENT,
        title VARCHAR(100),
        released_year YEAR,
        genre VARCHAR(100)
    );

    CREATE TABLE reviews (
        id INT PRIMARY KEY AUTO_INCREMENT,
        rating DECIMAL(2 , 1 ),
        series_id INT,
        reviewer_id INT,
        FOREIGN KEY (series_id)             #adding Foreign key Constraint
            REFERENCES series (id),         #referencing to series table, id column  
        FOREIGN KEY (reviewer_id)           #adding Foreign key Constrain
            REFERENCES reviewers (id)       #referencing to series table, id column
    );

![table creation 1](https://user-images.githubusercontent.com/119749518/215277900-a704ef23-3f91-47b6-8414-446c5d6bc70b.png)
![table creation 2](https://user-images.githubusercontent.com/119749518/215277908-12e08f65-17d2-4a88-9aed-66736b34cf02.png)


## Inserting rows in the 3 tables created

    INSERT INTO series (title, released_year, genre) VALUES
        ('Archer', 2009, 'Animation'),
        ('Arrested Development', 2003, 'Comedy'),
        ("Bob's Burgers", 2011, 'Animation'),
        ('Bojack Horseman', 2014, 'Animation'),
        ("Breaking Bad", 2008, 'Drama'),
        ('Curb Your Enthusiasm', 2000, 'Comedy'),
        ("Fargo", 2014, 'Drama'),
        ('Freaks and Geeks', 1999, 'Comedy'),
        ('General Hospital', 1963, 'Drama'),
        ('Halt and Catch Fire', 2014, 'Drama'),
        ('Malcolm In The Middle', 2000, 'Comedy'),
        ('Pushing Daisies', 2007, 'Comedy'),
        ('Seinfeld', 1989, 'Comedy'),
        ('Stranger Things', 2016, 'Drama');


    INSERT INTO reviewers (first_name, last_name) VALUES
        ('Thomas', 'Stoneman'),
        ('Wyatt', 'Skaggs'),
        ('Kimbra', 'Masters'),
        ('Domingo', 'Cortes'),
        ('Colt', 'Steele'),
        ('Pinkie', 'Petit'),
        ('Marlon', 'Crafford');


    INSERT INTO reviews(series_id, reviewer_id, rating) VALUES
        (1,1,8.0),(1,2,7.5),(1,3,8.5),(1,4,7.7),(1,5,8.9),
        (2,1,8.1),(2,4,6.0),(2,3,8.0),(2,6,8.4),(2,5,9.9),
        (3,1,7.0),(3,6,7.5),(3,4,8.0),(3,3,7.1),(3,5,8.0),
        (4,1,7.5),(4,3,7.8),(4,4,8.3),(4,2,7.6),(4,5,8.5),
        (5,1,9.5),(5,3,9.0),(5,4,9.1),(5,2,9.3),(5,5,9.9),
        (6,2,6.5),(6,3,7.8),(6,4,8.8),(6,2,8.4),(6,5,9.1),
        (7,2,9.1),(7,5,9.7),
        (8,4,8.5),(8,2,7.8),(8,6,8.8),(8,5,9.3),
        (9,2,5.5),(9,3,6.8),(9,4,5.8),(9,6,4.3),(9,5,4.5),
        (10,5,9.9),
        (13,3,8.0),(13,4,7.2),
        (14,2,8.5),(14,3,8.9),(14,4,8.9);
        
![insert values 1](https://user-images.githubusercontent.com/119749518/215277919-9cc9977e-0b7d-4968-9d26-5669c1ded2d9.png)


## Let's check if the tables are created

    SHOW TABLES;

![show tables](https://user-images.githubusercontent.com/119749518/215277936-34e85e8a-0536-4e64-aa92-51286a63212c.png)

    
## Let's check the structure of tables

    DESC reviewers;
    
    DESC reviews;
    
    DESC series;

![Str(reviewers)](https://user-images.githubusercontent.com/119749518/215277951-5a405a5a-f8ef-4f00-bc52-550be54349b7.png)
![str(reviews)](https://user-images.githubusercontent.com/119749518/215277953-9e274ef7-a780-4419-adfb-4bc6b730eb4b.png)
![str(series)](https://user-images.githubusercontent.com/119749518/215277954-78dbd376-b1ed-4c1e-85e9-001660866ed8.png)
 
## Let's check if the records are created in the 3 tables

    SELECT * FROM reviewers;

    SELECT * FROM reviews;
    
    SELECT * FROM series;
    
 ![reviewers table data](https://user-images.githubusercontent.com/119749518/215277986-1ec58eaa-351d-4ca7-ab2d-d10cbee48340.png)

 ![reviews table data](https://user-images.githubusercontent.com/119749518/215277997-56dac8c3-83a0-443b-8cac-d7fe184c375a.png)

 ![series table data](https://user-images.githubusercontent.com/119749518/215278006-fc36c5f8-ebb1-4516-89b1-ae7c820d9356.png)


--------
## Now the data is ready for manipulation
--------
### The Average Rating of all titles which are sorted by lowest to highest

    SELECT
        title,
        AVG(rating) AS Average_rating
    FROM
        series
    JOIN reviews ON series.id = reviews.series_id
    GROUP BY
        title
    ORDER BY
        Average_rating;
    
![image](https://user-images.githubusercontent.com/119749518/215279026-959493f9-d27f-4c54-97f0-e8785f47c1a5.png)

### The rating seems far stretched, using ROUND function to correct it

    SELECT
        title,
        ROUND(AVG(rating), 2) AS Average_rating     
    FROM
        series
    JOIN reviews ON series.id = reviews.series_id
    GROUP BY
        title
    ORDER BY
        Average_rating;
    
![image](https://user-images.githubusercontent.com/119749518/215279250-543637df-afd9-4a27-8eaf-abbe47c1cd16.png)
   
    
##  JOIN 2 tables to find the rating provided by each Reviewer
 
     SELECT
        CONCAT(first_name, ' ', last_name) AS 'Name of Reviewer',
        rating
    FROM
        reviewers
    JOIN reviews ON reviewers.id = reviews.reviewer_id;
 
 ![image](https://user-images.githubusercontent.com/119749518/215279522-9a4638da-72ff-4c18-9fb8-da562d757753.png)

## Finding such titles where reviews were not provided

    SELECT
        title
    FROM
        series
    LEFT JOIN reviews ON series.id = reviews.series_id
    WHERE
        rating IS NULL;
        
    ![image](https://user-images.githubusercontent.com/119749518/215280017-3e12d731-f4b4-4b7a-9b3b-6f48d4162d39.png)

## Average rating by Genre

    SELECT
        genre AS Genre,
        ROUND(AVG(rating), 2) AS 'Average Rating'
    FROM
        series
    JOIN reviews ON series.id = reviews.series_id
    GROUP BY
        genre;
        
   ![image](https://user-images.githubusercontent.com/119749518/215280629-72752440-4aaa-4d54-9587-04ff91c8af5e.png)

 
## Case Function Usage - Finding Reviewer, Total number of times the reviews were provided from a single reviewer, Minimum rating, Maximum rating, Average rating and Status column to show different statuses based on rating

    SELECT
        CONCAT(first_name, ' ', last_name) AS Reviewer,
        COUNT(rating) AS COUNT,
        IFNULL(MIN(rating), 0) AS MIN,
        IFNULL(MAX(rating), 0) AS MAX,
        IFNULL(ROUND(AVG(rating), 2), 0) AS Average,
     CASE 
        WHEN COUNT(rating) > 0 THEN 'ACTIVE' 
        ELSE 'INACTIVE'
    END AS Status
    FROM
        reviewers
    LEFT JOIN reviews ON reviewers.id = reviews.reviewer_id
    GROUP BY
        Reviewer
    ORDER BY
        Status;

 
![image](https://user-images.githubusercontent.com/119749518/215283271-56f6c5f4-481a-47a9-a4ac-f713c5382796.png)

## The same result can also be achieved by using IF function

    SELECT
            CONCAT(first_name, ' ', last_name) AS Reviewer,
            COUNT(rating) AS COUNT,
            IFNULL(MIN(rating), 0) AS MIN,
            IFNULL(MAX(rating), 0) AS MAX,
            IFNULL(ROUND(AVG(rating), 2), 0) AS Average,
            IF(COUNT(rating) > 0, 'ACTIVE', 'INACTIVE') AS Status           # using IF and not CASE
        FROM
            reviewers
        LEFT JOIN reviews ON reviewers.id = reviews.reviewer_id
        GROUP BY
            Reviewer
        ORDER BY
            Status;
 
![image](https://user-images.githubusercontent.com/119749518/215284030-8d90f5a0-db61-47e1-925d-309fecb47687.png)


## Combining 3 tables with JOIN to get Title, Rating and Reviewer

    SELECT
        title AS Title,
        rating AS Rating,
        CONCAT(first_name, ' ', last_name) AS Reviewer
    FROM
        series
    JOIN reviews ON series.id = reviews.series_id
    JOIN reviewers ON reviewers.id = reviews.reviewer_id;
    
  ![image](https://user-images.githubusercontent.com/119749518/215284879-eefbb92f-9b15-4b74-908b-fd9391dfd085.png)


# -----------------------THANK YOU------------------------
