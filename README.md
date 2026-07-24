Student Marks Grade Tracker API

A simple RESTful API built with Flask and MySQL for managing students, their marks,
reports and summaries.

Features:

- Managing data of students (create, read, update, delete).
- Getting subject-wise marks for each student.
- Calculate percentages, grades, and marks.
- Generate student performance reports.

Prerequisites:

- Python 3.8+
- MySQL server

Installation:

1. Clone this repository.
git clone <your-github-repository-link>

2. Installing dependencies:

   pip install -r requirements.txt
   
3. Database Setup (MySQL)

Run these commands in MySQL:

CREATE DATABASE grade_tracker;
USE grade_tracker;

CREATE TABLE students (
    id         INT AUTO_INCREMENT PRIMARY KEY,
    name       VARCHAR(100) NOT NULL,
    email      VARCHAR(100) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE marks (
    id         INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT          NOT NULL,
    subject    VARCHAR(100) NOT NULL,
    score      DECIMAL(5,2) NOT NULL,
    max_score  DECIMAL(5,2) NOT NULL DEFAULT 100,
    added_on   TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (student_id) REFERENCES students(id)
        ON DELETE CASCADE
);


4. Run the application:
    python app.py
   The app will start at http://127.0.0.1:5000.    

API Endpoints

*GET 

Returns API status.

Response

  json
{
  "message":"Welcome to Student Marks & Grade Tracker API",
  "status":"Running Successfully"
}

Students Data:

POST /students
Adds a new student.

  json
{
  "name":"venkatesh Namagiri",
  "email":"venkateshnamagiri@gmail.com"
}

Response

  json
{
  "message":"Student Added Successfully"
}

GET /students

Returns all students.

PUT /students/<id>

Updates student details.

Request

  json
{
  "name":"venkateshwaranamagiri",
  "email":"venkateshwaranamagiri@gmail.com"
}

DELETE /students/<id>

Deletes a student and all related marks.

Marks:

POST /students/<id>/marks

Request

  json
{
  "subject":"Maths",
  "score":99,
  "max_score":100
}

Response

  json
{
  "message":"Marks Added Successfully"
}

GET /students/<id>/marks

Returns all marks with:

- Percentage
- Grade

---
DELETE /marks/<id>

Deletes a mark.
