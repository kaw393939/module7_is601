# Module 7: Mid-Term Project – Python Application Development, Containerization, and DevOps

## Module Overview
This module consists of two parts:
1. **Mid-Term Project**: Students will develop and containerize a Python application, refactor it using Object-Oriented Programming (OOP) principles, test it using `pytest`, and automate testing and Docker builds using **GitHub Actions**. Students will choose one of three project options: **Personal Finance Manager**, **Weather Data Aggregator**, or **Inventory Management System**.
2. **Mid-Term Exam**: The mid-term exam will assess students' understanding of theoretical concepts, including Git, OOP, Docker, and GitHub Actions. The exam will be automatically graded and consist of multiple-choice and short-answer questions.

This module focuses on applying **DevOps** principles through CI/CD automation with GitHub Actions and Docker, emphasizing real-world development workflows.

---

## Why GitHub Actions and DevOps?
GitHub Actions provides an easy way to automate tests and builds by enabling **Continuous Integration (CI)**. It helps catch issues early in the development cycle, ensuring the consistency and reliability of code across environments. Docker ensures applications are portable and run consistently on any platform. This module combines these tools to help students automate workflows and apply modern DevOps practices.

---

### Learning Outcomes
- Utilize Git for version control and collaborative development.
- Write and execute unit tests and integration tests for Python applications using `pytest`.
- Implement object-oriented programming principles in Python.
- Create and manipulate CSV files using Python.
- Apply professional program techniques such as DRY and error handling using LBYL and EAFP.
- Apply containerization techniques to containerize applications using Docker.
- Containerize and manage Python applications using Docker, including Dockerfile creation, environment variables, and volume management.
- Set up GitHub Actions for Continuous Integration (CI), automating the execution of tests and Docker builds.
- Implement DevOps principles to automate testing and deployment pipelines, ensuring software quality and consistency across environments.

---

## Module 7 Learning Pathway

### Mid-Term Exam
The mid-term exam will test students' understanding of the core concepts, including:
- Git for version control.
- Python OOP principles and design patterns.
- Docker and containerization.
- Testing with `pytest`.
- GitHub Actions and Continuous Integration (CI).

The exam will be automatically graded and will consist of multiple-choice, short-answer, and code-based questions. **(Note: This exam will be created later and announced separately.)**

---

### Mid-Term Project

Students will choose **one** of the following project options for their mid-term project. Each project will assess their ability to apply Python, OOP, Docker, and GitHub Actions.

#### Option 1: Personal Finance Manager

**Description**:  
Create a command-line application that allows users to track their personal finances. Users can input income and expenses, categorize transactions, and generate reports in CSV and HTML formats.

**Detailed Requirements**:

1. **Core Functionality**:
   - Users must be able to add, edit, and delete transactions.
   - Each transaction should include the date, description, category (e.g., income or expense), and amount.
   - Users should be able to categorize transactions (e.g., groceries, rent, salary).
   - A summary report should be generated, showing total income, total expenses, and the current balance.

2. **OOP Principles**:
   - Implement classes such as `Transaction`, `FinanceManager`, and `ReportGenerator`.
   - Use a **Factory Method** pattern for creating different types of transactions (e.g., income vs. expense).
   - Use the **Observer Pattern** to notify when the CSV file has been updated with new data.

3. **Testing**:
   - Write unit tests for all key functions, such as adding, editing, deleting transactions, and generating reports.
   - Aim for 80%+ test coverage using `pytest`. Ensure that tests cover both expected functionality and edge cases (e.g., invalid input handling, empty CSV files).

4. **Dockerization**:
   - Create a `Dockerfile` to containerize the application.
   - The application should run inside a Docker container, and users should be able to persist data using Docker volumes for the CSV file.

5. **GitHub Actions**:
   - Set up GitHub Actions to automatically run the tests using `pytest` whenever code is pushed to the repository.
   - Set up a GitHub Action to build the Docker image and ensure that the application can run within a Docker container.

**Example CSV File**:
```csv
Date,Description,Category,Amount
2024-01-01,Salary,Income,5000
2024-01-10,Rent,Expense,-1200
2024-01-15,Grocery,Expense,-300
```

---

#### Option 2: Weather Data Aggregator

**Description**:  
Create a weather data aggregation system that reads weather data from CSV files, filters data based on various conditions, and generates reports in CSV and HTML formats.

**Detailed Requirements**:

1. **Core Functionality**:
   - Users must be able to load weather data from CSV files.
   - The application should allow users to filter data by date, location, and weather condition (e.g., temperature, humidity, weather description).
   - The system should generate a summary report with key statistics, such as average temperature and humidity for a specific date or location.

2. **OOP Principles**:
   - Implement classes such as `WeatherData`, `WeatherAggregator`, and `ReportGenerator`.
   - Use an **Observer Pattern** to notify the system when data is added or updated.

3. **Testing**:
   - Write unit tests for filtering and report generation functionality.
   - Test the edge cases (e.g., missing data, extreme temperatures) and ensure high code coverage (80%+).

4. **Dockerization**:
   - Create a `Dockerfile` that will containerize the weather data aggregator system.
   - Use Docker volumes to persist weather data files and ensure they are correctly handled inside the container.

5. **GitHub Actions**:
   - Set up GitHub Actions to automatically run the tests using `pytest` and build the Docker image when code is committed.

**Example CSV File**:
```csv
Date,Location,Temperature,Humidity,Weather
2024-01-01,New York,30,60,Cloudy
2024-01-02,Los Angeles,75,40,Sunny
2024-01-03,Chicago,20,70,Snow
```

---

#### Option 3: Inventory Management System

**Description**:  
Develop an inventory management system that allows users to add, update, delete, and view inventory items. Generate inventory reports in CSV and HTML formats.

**Detailed Requirements**:

1. **Core Functionality**:
   - Users must be able to add, edit, delete, and view inventory items.
   - Each item should have an ID, name, category, quantity, and price.
   - Generate inventory reports that show total stock value, and flag low-stock items.

2. **OOP Principles**:
   - Implement classes such as `Item`, `InventoryManager`, and `ReportGenerator`.
   - Use the **Command Pattern** to handle user commands such as add, edit, delete, and generate report.

3. **Testing**:
   - Write unit tests for adding, editing, deleting, and viewing items.
   - Ensure comprehensive test coverage for inventory management functions using `pytest` (80%+ coverage).

4. **Dockerization**:
   - Create a `Dockerfile` to containerize the inventory management system.
   - Use Docker volumes to persist the inventory data (stored in a CSV file).

5. **GitHub Actions**:
   - Set up GitHub Actions to automatically run tests and build Docker images upon commits to the repository.

**Example CSV File**:
```csv
ItemID,ItemName,Category,Quantity,Price
1,Laptop,Electronics,15,800
2,Phone,Electronics,30,500
3,Desk,Furniture,10,150
```

---

### Read

**Article**: [Introduction to GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)  
**Purpose**: Learn how to use GitHub Actions to automate testing, builds, and deployments.

**Article**: [Continuous Integration and DevOps Practices](https://www.atlassian.com/continuous-delivery/continuous-integration)  
**Purpose**: Understand how CI/CD practices improve the software development lifecycle.

**Article**: [Using GitHub Actions for Python Projects](https://docs.github.com/en/actions/guides/building-and-testing-python)  
**Purpose**: Learn how to set up GitHub Actions for Python projects to automate testing and Docker builds.

---

### Watch

**Video**: [Introduction to GitHub Actions for CI/CD](https://www.youtube.com/watch?v=mFFXuXjVgkU) (20 minutes)  
**Purpose**: Get an overview of how to use GitHub Actions for automating testing and deployment workflows.

**Video**: [Automating Docker Builds with GitHub Actions](https://www.youtube.com/watch?v=ecK3EnyGD8o) (25 minutes)  
**Purpose**: Learn how to automate Docker builds with GitHub Actions.

---

### Submit

**Activity Title**: Mid-Term Project Submission  
**Grading Type**: Points  
**Submission Instructions**: Submit the following in your GitHub repository:
1. **GitHub Repository Link**: Submit a link to your GitHub repository containing:
   - Your **code**, **Docker

file**, and **GitHub Actions workflows**.
   - A **README.md** file with the reflection, documentation of the project, and instructions for running the application.
   - A link to the deployed container on a cloud service or DockerHub.

---

### Grading Criteria

- **Correctness**: The application meets the functional requirements and correctly implements the features.
- **Testing**: Unit and integration tests are implemented using `pytest`, covering at least 80% of the codebase.
- **OOP Principles**: The project follows proper OOP principles, utilizing appropriate design patterns and structure.
- **Dockerization**: The application runs successfully inside a Docker container, and data persists using Docker volumes.
- **CI/CD**: GitHub Actions workflows are set up to run tests and build Docker images automatically upon commits.
- **Code Quality**: The code is well-organized, follows PEP 8 standards, and includes clear documentation.
- **Reflection**: The README file contains a reflection on the project development process, challenges faced, and lessons learned.

---

### Reflect

**Title**: Mid-Term Project Reflection  
**Grading Type**: Points  
**Instructions**:  
Write a reflection (600-700 words) on your experience developing the mid-term project:
- Discuss the challenges you faced and how you overcame them.
- Reflect on how Docker, GitHub Actions, and OOP principles helped streamline the development process.
- Consider how you would apply these techniques in real-world software development.
```
