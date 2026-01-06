---
layout: project
type: project
image_svg: svg/lms/lms-thumbnail.svg
title: "Library Management System (LMS)"
date: 2025-01-25
published: true
labels:
  - C++
  - SQL
  - Database Management
  - Command Line Interface
summary: "A robust C++ and SQL-based system designed to automate library operations, including book inventory, user management, and fine calculations."
---

<div class="text-center p-4">
  <img width="400px" src="../img/lms/lms-visual-report.png" class="img-thumbnail">
  <img width="400px" src="../img/lms/lms-book-searching.png" class="img-thumbnail">
  <img width="400px" src="../img/lms/lms-payment.png" class="img-thumbnail">
  <img width="400px" src="../img/lms/lms-profile.png" class="img-thumbnail">
</div>

## Project Overview

The **Library Management System (LMS)** is a professional-grade software solution designed to modernize traditional library operations. Despite advances in digital systems, many institutions still rely on manual book tracking and inefficient borrowing workflows. This project addresses those challenges by providing a centralized digital platform that automates core library functions, improving operational efficiency, data accuracy, and user accountability.

## System Roles and Access Control

The system implements **Role-Based Access Control (RBAC)** and supports three distinct user roles:

- **Patrons:** Search books, borrow and return items, and manage personal profiles.
- **Staff:** Handle daily lending operations, inventory updates, and loan records.
- **Admins:** Manage system configurations, including fine rates, borrowing limits, and user privileges.

This role separation ensures secure access control and clear operational responsibilities.

## Development Responsibilities

For this project, I was responsible for **full-stack system development**, including the following components:

### Database Schema Design
Designed and implemented an SQL database consisting of five core entities:
- `User`
- `Book`
- `Loan`
- `Fine`
- `RolePrivilege`

The schema enforces referential integrity and supports scalable transaction handling.

### Core Logic Implementation
Developed the application layer in **C++**, incorporating:
- Automated fine calculations for overdue items
- Real-time book availability tracking
- Secure user authentication and role validation

### Command Line Interface (CLI)
Built a user-friendly **CLI** featuring:
- Arrow-key navigation
- Color-coded outputs
- Structured menus for efficient system interaction

### Data Reporting
Integrated reporting features that generate:
- Annual borrowing statistics
- Tabular summaries
- Graph-based visualizations for administrative review

## Technical Implementation Snippet

The system extensively applies **Object-Oriented Programming (OOP)** principles. For example, the `dbConnection` class centralizes all SQL database interactions, using pass-by-reference and constant parameters to improve efficiency and maintain data immutability.

Below is a representative snippet demonstrating how query results are fetched into a vector of maps for flexible data manipulation:

```cpp
std::vector<std::map<std::string, std::string>> 
dbConnection::fetchResults(const std::string& query) {
    try {
        std::unique_ptr<sql::PreparedStatement> pstmt(con->prepareStatement(query));
        std::unique_ptr<sql::ResultSet> res(pstmt->executeQuery());

        std::vector<std::map<std::string, std::string>> result;

        while (res->next()) {
            std::map<std::string, std::string> row;
            sql::ResultSetMetaData* meta = res->getMetaData();

            for (int i = 1; i <= meta->getColumnCount(); ++i) {
                row[meta->getColumnName(i)] = res->getString(i);
            }

            result.push_back(row);
        }

        return result;
    } catch (const sql::SQLException& e) {
        throw std::runtime_error("SQL Error: " + std::string(e.what()));
    }
}
```

<div class="text-center p-4"> <a href="https://github.com/ThomsonTea/Library-Management-System" class="btn btn-outline-primary"> View Project on GitHub </a> </div>