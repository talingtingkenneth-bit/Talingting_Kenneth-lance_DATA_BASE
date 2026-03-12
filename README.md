# Talingting_Kenneth-lance_DATA_BASE
Project Overview

This is a desktop-based Student Information System built using **Java (Swing GUI)** and a **MySQL Database**. It demonstrates a full understanding of **CRUD** (Create, Read, Update, Delete) operations by allowing users to manage student records in a responsive, visual interface.
Features

* **Create (Add):** Input new student details (First Name, Last Name, Age, Email) and save them directly to the MySQL database.
* **Read (View):** Automatically fetches and displays all student records from the database into a neatly organized Java `JTable`.
* **Update (Edit):** Click on any student in the table to instantly load their data into the text fields, modify their information, and save the updates to the database.
* **Delete (Remove):** Select a student from the table and delete their record from the database with a confirmation prompt.
* **Clear Form:** A utility button to instantly clear all text fields and reset the cursor for quick data entry.

Technologies Used

* **Language:** Java
* **GUI Framework:** Java Swing (JFrame, JButton, JTextField, JTable)
* **IDE:** Apache NetBeans
* **Database:** MySQL
* **Database Driver:** MySQL Connector/J (JDBC)

---

Prerequisites & Setup

To run this application on your local machine, you will need:

1. Java Development Kit (JDK) installed.
2. A MySQL Server running locally (via MySQL Workbench, XAMPP, etc.).
3. The `mysql-connector-j-8.x.x.jar` file attached to your project libraries.

Database Configuration

Before running the application, you must create the database and table. Run the following SQL script in your MySQL Workbench:

```sql
CREATE DATABASE student_information_system;

USE student_information_system;

CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    age INT NOT NULL,
    email VARCHAR(100) NOT NULL
);

```

*(Note: Ensure that the MySQL username and password in the `DBConnection.java` file match your local MySQL server credentials).*

---
How the Code Works

The project is structured into three main parts to keep the code organized:

### 1. The Database Bridge (`DBConnection.java`)

This class uses the **Singleton pattern** to create a single, active connection between the Java application and the MySQL database. It uses `DriverManager.getConnection()` and the JDBC driver to log into the database so the rest of the application can send SQL queries.

### 2. The Blueprint (`Student.java`)

This is the "Model" class. It acts as a blueprint that perfectly matches the columns in the MySQL `students` table. It uses private variables for Encapsulation and provides public "Getters and Setters" to safely access and modify the data.

### 3. The Visual Interface & Logic (`StudentGUI.java`)

This is the core of the application. It extends `javax.swing.JFrame` and handles all user interactions:

* **`loadStudentData()` Method:** Uses a `SELECT * FROM students` query and a `ResultSet` to loop through the database and populate the `DefaultTableModel` of the visual table.
* **Action Listeners:** Every button (Add, Update, Delete, Clear) has an Action Listener. When clicked, these listeners gather data from the `JTextField` components, prepare a `PreparedStatement` with parameterized SQL queries (e.g., `INSERT INTO`, `UPDATE`, `DELETE`) to prevent SQL injection, and execute the update.
* **Mouse Listener:** The `JTable` uses a `mouseClicked` event to detect which row a user selects, extracting the data from that specific row and auto-filling the text fields for easy updating.

---

