Here's a detailed README for your Library Management System project:

---

Library Management System
Project Overview
The Library Management System is a comprehensive project designed to manage the entire catalog of books in a library. It keeps track of book information, costs, statuses, and the total number of books available. The system also manages data related to library branches, employees, customers, and the borrowing and returning of books.

## Table of Contents
1. Database Structure
2. SQL Queries

## Database Structure
The database consists of the following six tables:

### 1. Branch
- **Branch_no**: INT, PRIMARY KEY
- **Manager_Id**: INT
- **Branch_address**: VARCHAR(255)
- **Contact_no**: VARCHAR(20)

### 2. Employee
- **Emp_Id**: INT, PRIMARY KEY
- **Emp_name**: VARCHAR(100)
- **Position**: VARCHAR(100)
- **Salary**: DECIMAL(10, 2)
- **Branch_no**: INT, FOREIGN KEY (references Branch(Branch_no))

### 3. Books
- **ISBN**: INT, PRIMARY KEY
- **Book_title**: VARCHAR(255)
- **Category**: VARCHAR(100)
- **Rental_Price**: DECIMAL(10, 2)
- **Status**: VARCHAR(10) (yes if book is available, no if not available)
- **Author**: VARCHAR(100)
- **Publisher**: VARCHAR(100)

### 4. Customer
- **Customer_Id**: INT, PRIMARY KEY
- **Customer_name**: VARCHAR(100)
- **Customer_address**: VARCHAR(255)
- **Reg_date**: DATE

### 5. IssueStatus
- **Issue_Id**: INT, PRIMARY KEY
- **Issued_cust_id**: INT, FOREIGN KEY (references Customer(Customer_Id))
- **Issued_book_name**: VARCHAR(255)
- **Issue_date**: DATE
- **Isbn_book**: INT, FOREIGN KEY (references Books(ISBN))

### 6. ReturnStatus
- **Return_Id**: INT, PRIMARY KEY
- **Return_cust**: INT, FOREIGN KEY (references Customer(Customer_Id))
- **Return_book_name**: VARCHAR(255)
- **Return_date**: DATE
- **Isbn_book2**: INT, FOREIGN KEY (references Books(ISBN))

## SQL Queries
The following SQL queries are used to manage and retrieve data within the library system:

1. **Retrieve the book title, category, and rental price of all available books:**
   ```sql
   SELECT Book_title, Category, Rental_Price 
   FROM Books 
   WHERE Status = 'yes';
   ```

2. **List the employee names and their respective salaries in descending order of salary:**
   ```sql
   SELECT Emp_name, Salary 
   FROM Employee 
   ORDER BY Salary DESC;
   ```

3. **Retrieve the book titles and the corresponding customers who have issued those books:**
   ```sql
   SELECT Books.Book_title, Customer.Customer_name 
   FROM IssueStatus 
   JOIN Books ON IssueStatus.Isbn_book = Books.ISBN 
   JOIN Customer ON IssueStatus.Issued_cust_id = Customer.Customer_Id;
   ```

4. **Display the total count of books in each category:**
   ```sql
   SELECT Category, COUNT(*) AS Total_Books 
   FROM Books 
   GROUP BY Category;
   ```

5. **Retrieve the employee names and their positions for the employees whose salaries are above Rs.50,000:**
   ```sql
   SELECT Emp_name, Position 
   FROM Employee 
   WHERE Salary > 50000;
   ```

6. **List the customer names who registered before 2022-01-01 and have not issued any books yet:**
   ```sql
   SELECT Customer_name 
   FROM Customer 
   WHERE Reg_date < '2022-01-01' 
   AND Customer_Id NOT IN (SELECT Issued_cust_id FROM IssueStatus);
   ```

7. **Display the branch numbers and the total count of employees in each branch:**
   ```sql
   SELECT Branch_no, COUNT(*) AS Total_Employees 
   FROM Employee 
   GROUP BY Branch_no;
   ```

8. **Display the names of customers who have issued books in the month of June 2023:**
   ```sql
   SELECT Customer.Customer_name 
   FROM IssueStatus 
   JOIN Customer ON IssueStatus.Issued_cust_id = Customer.Customer_Id 
   WHERE IssueStatus.Issue_date BETWEEN '2023-06-01' AND '2023-06-30';
   ```

9. **Retrieve book_title from book table containing history:**
   ```sql
   SELECT Book_title 
   FROM Books 
   WHERE Book_title LIKE '%history%';
   ```

10. **Retrieve the branch numbers along with the count of employees for branches having more than 5 employees:**
    ```sql
    SELECT Branch_no, COUNT(*) AS Total_Employees 
    FROM Employee 
    GROUP BY Branch_no 
    HAVING COUNT(*) > 5;
    ```

11. **Retrieve the names of employees who manage branches and their respective branch addresses:**
    ```sql
    SELECT Emp_name, Branch.Branch_address 
    FROM Employee 
    JOIN Branch ON Employee.Emp_Id = Branch.Manager_Id;
    ```

12. **Display the names of customers who have issued books with a rental price higher than Rs. 25:**
    ```sql
    SELECT DISTINCT Customer.Customer_name 
    FROM IssueStatus 
    JOIN Books ON IssueStatus.Isbn_book = Books.ISBN 
    JOIN Customer ON IssueStatus.Issued_cust_id = Customer.Customer_Id 
    WHERE Books.Rental_Price > 25;
    ```





This README provides a clear and structured overview of your Library Management System project, making it easy for others to understand and use your project.
