# Vidya_lakshmi_scheme_SQL_Analysis
  A SQL-based data analysis project exploring the awareness and demographic reach of the Vidya Lakshmi scheme in India. 
-- Schema for the Vidya Lakshmi Scheme Awareness Project

-- Students Table
-- Stores demographic and awareness data for each student

#1 Database Schema 
--The database schema will be a single table to keep the project focused on the requested queries.
--This simplifies the joins and allows for more complex single-table operations.

CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(100) NOT NULL,
    age INT,
    gender VARCHAR(10), -- 'Male', 'Female', 'Other'
    state VARCHAR(50),
    is_rural_area BOOLEAN NOT NULL,
    is_aware BOOLEAN NOT NULL -- TRUE (1) if aware, FALSE (0) if unaware
);

#2 Sample Data 
--The sample data is designed to be diverse, representing different demographics and awareness levels.
--The state column is added to allow for queries with LIKE and other geographical filters.

-- Sample Data for Vidya Lakshmi Scheme Awareness Project
-- Sample Data for Vidya Lakshmi Scheme Awareness Project

-- Insert data into Students table

INSERT INTO Students (student_id, student_name, age, gender, state, is_rural_area, is_aware) VALUES
(1, 'Aarav Sharma', 21, 'Male', 'Maharashtra', FALSE, TRUE),
(2, 'Priya Singh', 23, 'Female', 'Uttar Pradesh', TRUE, TRUE),
(3, 'Rahul Verma', 19, 'Male', 'Delhi', FALSE, FALSE),
(4, 'Sneha Gupta', 20, 'Female', 'Rajasthan', TRUE, TRUE),
(5, 'Amit Kumar', 25, 'Male', 'Bihar', FALSE, FALSE),
(6, 'Neha Reddy', 22, 'Female', 'Telangana', TRUE, TRUE),
(7, 'Vijay Kumar', 24, 'Male', 'Tamil Nadu', FALSE, TRUE),
(8, 'Divya Patel', 20, 'Female', 'Gujarat', TRUE, FALSE),
(9, 'Suresh Joshi', 21, 'Male', 'Maharashtra', FALSE, TRUE),
(10, 'Kavita Singh', 23, 'Female', 'Uttar Pradesh', TRUE, FALSE),
(11, 'Rajesh Kumar', 22, 'Male', 'Delhi', FALSE, TRUE),
(12, 'Pooja Sharma', 20, 'Female', 'Rajasthan', FALSE, TRUE),
(13, 'Sandeep Kumar', 24, 'Male', 'Bihar', TRUE, FALSE),
(14, 'Anjali Singh', 21, 'Female', 'Uttar Pradesh', TRUE, TRUE),
(15, 'Vikram Rathore', 25, 'Male', 'Maharashtra', FALSE, TRUE),
(16, 'Riya Das', 19, 'Female', 'West Bengal', TRUE, FALSE),
(17, 'Ajay Patil', 20, 'Male', 'Maharashtra', FALSE, FALSE),
(18, 'Meera Saini', 22, 'Female', 'Rajasthan', TRUE, TRUE),
(19, 'Karan Sharma', 24, 'Male', 'Delhi', FALSE, TRUE),
(20, 'Sunita Yadav', 21, 'Female', 'Uttar Pradesh', TRUE, FALSE);


# 3 SQL Queries (queries.sql)
--This file is the core of your project. Each query demonstrates a specific SQL command or concept.

--Basic Filtering and Ordering (WHERE, AND, OR, ORDER BY)
# Query 1: Find all male students from a rural area who are aware of the scheme.

SELECT student_name, age, state
FROM Students
WHERE gender = 'Male' AND is_rural_area = TRUE AND is_aware = TRUE;

#Query 2: Find all students who are either from Maharashtra OR are unaware of the scheme, ordered by name.

SELECT student_name, age, state, is_aware
FROM Students
WHERE state = 'Maharashtra' OR is_aware = FALSE
ORDER BY student_name ASC;

# Query 3: Find all students whose names start with 'S' and are between 20 and 24 years old.

SELECT student_name, age, state
FROM Students
WHERE student_name LIKE 'S%' AND age BETWEEN 20 AND 24;

# Query 4: Find all students from states with 'Pradesh' in their name, or those from Rajasthan.

SELECT student_name, state
FROM Students
WHERE state LIKE '%Pradesh%' OR state = 'Rajasthan';

#  Query 5: Insert a new student record.
--This demonstrates how to add new data to the table.

INSERT INTO Students (student_id, student_name, age, gender, state, is_rural_area, is_aware)
VALUES (21, 'Arjun Menon', 26, 'Male', 'Kerala', FALSE, TRUE);

# Query 6: Update the awareness status for a specific student.
--This query can be used to correct or change a data point.

UPDATE Students
SET is_aware = TRUE
WHERE student_id = 16; 

# Query 7: Combine a list of aware students and a list of unaware students from Uttar Pradesh.
--This query uses UNION to merge two result sets into one.

SELECT student_name, 'Aware' AS awareness_status
FROM Students
WHERE is_aware = TRUE
UNION
SELECT student_name, 'Unaware' AS awareness_status
FROM Students
WHERE is_aware = FALSE AND state = 'Uttar Pradesh';

# Query 8: Use a CTE to find the percentage of rural awareness.
--A Common Table Expression (CTE) makes complex queries more readable.

WITH RuralStudents AS (
    SELECT COUNT(*) AS total_rural_students,
           SUM(CASE WHEN is_aware = TRUE THEN 1 ELSE 0 END) AS aware_rural_students
    FROM Students
    WHERE is_rural_area = TRUE
)
SELECT
    (CAST(aware_rural_students AS DECIMAL) / total_rural_students) * 100 AS rural_awareness_percentage
FROM RuralStudents;














































-- Insert data into Students table
