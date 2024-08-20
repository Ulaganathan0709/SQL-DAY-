# SQL02 Database Setup and Usage

## Overview

This project sets up a relational database named `SQL02` that models a simple educational platform. The database includes tables for users, students, mentors, topics, tasks, and attendance. The relationships between these entities are managed using primary and foreign keys.

## Database Structure

The database consists of the following tables:

1. **Users**
   - Stores basic user information.
   - Columns: `user_id`, `username`, `email`, `createdAt`
   - Relationships: Linked to both `students` and `mentors`.

2. **Students**
   - Stores additional information specific to students.
   - Columns: `student_id`, `user_id`, `full_name`, `address`, `phone_number`, `qualification`, `work_experience`
   - Relationships: References the `users` table via `user_id`.

3. **Mentors**
   - Stores additional information specific to mentors.
   - Columns: `mentor_id`, `user_id`, `full_name`, `address`, `phone_number`, `qualification`, `work_experience`
   - Relationships: References the `users` table via `user_id`.

4. **Topics**
   - Stores information about educational topics.
   - Columns: `topic_id`, `topic_name`, `description`, `sessions`, `mentor_id`
   - Relationships: References the `mentors` table via `mentor_id`.

5. **Tasks**
   - Stores information about tasks related to topics.
   - Columns: `task_id`, `topic_id`, `task_name`, `description`, `deadline`
   - Relationships: References the `topics` table via `topic_id`.

6. **Attendance**
   - Tracks attendance of users for specific topics.
   - Columns: `attendance_id`, `user_id`, `topic_id`, `session_date`, `status`
   - Relationships: References the `users` and `topics` tables via `user_id` and `topic_id`.

## Setup

To set up the database, follow these steps:

1. **Create the Database and Tables:**

    ```sql
    CREATE DATABASE SQL02;
    USE SQL02;

    -- Users table
    CREATE TABLE users (
        user_id INT PRIMARY KEY,
        username VARCHAR(255),
        email VARCHAR(255),
        createdAt DATETIME
    );

    -- Students table
    CREATE TABLE students (
        student_id INT PRIMARY KEY,
        user_id INT,
        full_name VARCHAR(255),
        address VARCHAR(255),
        phone_number VARCHAR(10),
        qualification TEXT,
        work_experience TEXT,
        FOREIGN KEY (user_id) REFERENCES users(user_id)
    );

    -- Mentors table
    CREATE TABLE mentors (
        mentor_id INT PRIMARY KEY,
        user_id INT,
        full_name VARCHAR(255),
        address VARCHAR(255),
        phone_number VARCHAR(10),
        qualification TEXT,
        work_experience TEXT,
        FOREIGN KEY (user_id) REFERENCES users(user_id)
    );

    -- Topics table
    CREATE TABLE topics (
        topic_id INT PRIMARY KEY,
        topic_name VARCHAR(255),
        description TEXT,
        sessions INT,
        mentor_id INT,
        FOREIGN KEY (mentor_id) REFERENCES mentors(mentor_id)
    );

    -- Tasks table
    CREATE TABLE tasks (
        task_id INT PRIMARY KEY,
        topic_id INT,
        task_name VARCHAR(255),
        description TEXT,
        deadline DATE,
        FOREIGN KEY (topic_id) REFERENCES topics(topic_id)
    );

    -- Attendance table
    CREATE TABLE attendance (
        attendance_id INT PRIMARY KEY,
        user_id INT,
        topic_id INT,
        session_date DATE,
        status VARCHAR(255),
        FOREIGN KEY (user_id) REFERENCES users(user_id),
        FOREIGN KEY (topic_id) REFERENCES topics(topic_id)
    );
    ```

2. **Insert Sample Data:**

    ```sql
    -- Insert data into users table
    INSERT INTO users (user_id, username, email, createdAt) VALUES
    (1, 'john_doe', 'john@example.com', '2024-08-01 10:00:00'),
    (2, 'jane_smith', 'jane@example.com', '2024-08-02 11:00:00'),
    (3, 'mentor_james', 'james@example.com', '2024-08-03 12:00:00');

    -- Insert data into students table
    INSERT INTO students (student_id, user_id, full_name, address, phone_number, qualification, work_experience) VALUES
    (1, 1, 'John Doe', '123 Main St', '1234567890', 'B.Sc. Computer Science', '2 years as Junior Developer'),
    (2, 2, 'Jane Smith', '456 Oak Ave', '0987654321', 'B.A. Information Technology', '1 year as IT Support');

    -- Insert data into mentors table
    INSERT INTO mentors (mentor_id, user_id, full_name, address, phone_number, qualification, work_experience) VALUES
    (1, 3, 'James Mentor', '789 Pine Rd', '1122334455', 'M.Sc. Software Engineering', '5 years as Senior Developer');

    -- Insert data into topics table
    INSERT INTO topics (topic_id, topic_name, description, sessions, mentor_id) VALUES
    (1, 'Introduction to Python', 'Basic Python programming concepts', 10, 1),
    (2, 'Advanced Java', 'Deep dive into Java programming', 12, 1);

    -- Insert data into tasks table
    INSERT INTO tasks (task_id, topic_id, task_name, description, deadline) VALUES
    (1, 1, 'Python Basics Assignment', 'Complete exercises on variables, data types, and control structures.', '2024-08-10'),
    (2, 2, 'Java Collections Assignment', 'Work on Java Collections framework tasks.', '2024-08-12');

    -- Insert data into attendance table
    INSERT INTO attendance (attendance_id, user_id, topic_id, session_date, status) VALUES
    (1, 1, 1, '2024-08-01', 'Present'),
    (2, 2, 1, '2024-08-01', 'Absent'),
    (3, 1, 2, '2024-08-02', 'Present');
    ```

3. **Verify Data:**

    After inserting the data, you can run the following queries to verify the content of each table:

    ```sql
    SELECT * FROM users;
    SELECT * FROM students;
    SELECT * FROM mentors;
    SELECT * FROM topics;
    SELECT * FROM tasks;
    SELECT * FROM attendance;
    ```

## How to Run

- **SQL Environment:** You can run this script in any SQL environment such as MySQL Workbench, DB Fiddle, or any other MySQL-compatible environment.
- **Execution:** Copy and paste the SQL code from this `README.md` into your SQL environment to create the database, tables, and insert the sample data.

## License

This project is open-source and free to use.

