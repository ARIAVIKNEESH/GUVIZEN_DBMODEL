# GUVIZEN_DBMODEL

CREATE DATABASE ZenClassPortal;
USE ZenClassPortal;

-- Users Table
CREATE TABLE Users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    role ENUM('candidate', 'mentor') NOT NULL
);

-- Classes Table
CREATE TABLE Classes (
    class_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    timing DATETIME NOT NULL,
    isEnded BOOLEAN NOT NULL DEFAULT FALSE
);

-- Tasks Table
CREATE TABLE Tasks (
    task_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    tag VARCHAR(50) NOT NULL
);

-- Queries Table
CREATE TABLE Queries (
    query_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    description TEXT NOT NULL,
    tag VARCHAR(50),
    date DATE NOT NULL,
    language VARCHAR(50),
    time TIME NOT NULL
);

-- Events Table
CREATE TABLE Events (
    event_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    description TEXT,
    event_type ENUM('Hackathon', 'Placement Session') NOT NULL,
    date DATE NOT NULL,
    time TIME NOT NULL
);

-- Link Table: User_Classes
CREATE TABLE User_Classes (
    user_class_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    class_id INT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES Users(user_id),
    FOREIGN KEY (class_id) REFERENCES Classes(class_id)
);

-- Link Table: User_Tasks
CREATE TABLE User_Tasks (
    user_task_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    task_id INT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES Users(user_id),
    FOREIGN KEY (task_id) REFERENCES Tasks(task_id)
);

-- Link Table: Class_Tasks
CREATE TABLE Class_Tasks (
    class_task_id INT AUTO_INCREMENT PRIMARY KEY,
    class_id INT NOT NULL,
    task_id INT NOT NULL,
    FOREIGN KEY (class_id) REFERENCES Classes(class_id),
    FOREIGN KEY (task_id) REFERENCES Tasks(task_id)
);

-- Link Table: User_Queries
CREATE TABLE User_Queries (
    user_query_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    query_id INT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES Users(user_id),
    FOREIGN KEY (query_id) REFERENCES Queries(query_id)
);

-- Link Table: Event_Participants
CREATE TABLE Event_Participants (
    event_participant_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    event_id INT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES Users(user_id),
    FOREIGN KEY (event_id) REFERENCES Events(event_id)
);


INSERTING VALUES:

-- Insert values into Users table
INSERT INTO Users (name, email, role) VALUES 
('Aria', 'Aria@gmail.com', 'candidate'),
('Akhil', 'akhil@gmail.com', 'mentor');

-- Insert values into Classes table
INSERT INTO Classes (title, timing, isEnded) VALUES 
('JavaScript Basics', '2024-08-16 10:00:00', FALSE),
('React Advanced', '2024-08-17 14:00:00', FALSE);

-- Insert values into Tasks table
INSERT INTO Tasks (title, tag) VALUES 
('Complete Assignment 1', 'JavaScript'),
('Review React Project', 'React');


-- Insert values into Queries table
INSERT INTO Queries (title, description, tag, date, language, time) VALUES 
('Issue with JavaScript Loop', 'I am facing an issue with the for loop in JavaScript.', 'JavaScript', '2024-08-15', 'JavaScript', '10:30:00'),
('React State Management', 'How do I manage state effectively in React?', 'React', '2024-08-15', 'JavaScript', '11:00:00');

-- Insert values into Events table
INSERT INTO Events (title, description, event_type, date, time) VALUES 
('Hackathon 2024', 'Annual coding competition.', 'Hackathon', '2024-09-01', '09:00:00'),
('Placement Preparation Session', 'Guidance for upcoming placement drives.', 'Placement Session', '2024-08-20', '15:00:00');

-- Insert values into User_Classes table
INSERT INTO User_Classes (user_id, class_id) VALUES 
(1, 1),  -- Aria in JavaScript Basics
(2, 2);  -- Akhil in React Advanced

-- Insert values into User_Tasks table
INSERT INTO User_Tasks (user_id, task_id) VALUES 
(1, 1),  -- Aria assigned to Complete Assignment 1
(2, 2);  -- Akhil assigned to Review React Project

-- Insert values into Class_Tasks table
INSERT INTO Class_Tasks (class_id, task_id) VALUES 
(1, 1),  -- JavaScript Basics class linked to Complete Assignment 1
(2, 2);  -- React Advanced class linked to Review React Project

-- Insert values into User_Queries table
INSERT INTO User_Queries (user_id, query_id) VALUES 
(1, 1),  -- Aria asked about Issue with JavaScript Loop
(2, 2);  -- Akhil asked about React State Management

-- Insert values into Event_Participants table
INSERT INTO Event_Participants (user_id, event_id) VALUES 
(1, 1),  -- Aria participating in Hackathon 2024
(2, 2);  -- Akhil participating in Placement Preparation Session
