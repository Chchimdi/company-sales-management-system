# Company Sales Management System

This repository contains SQL scripts for a relational database schema designed to manage a company’s sales, employees, clients, branches, and suppliers. The database captures information about employees, their relationships with clients, sales data, and branch information.

## Database Overview

The **Company Sales Management System** database consists of six primary tables:

1. **employee**: Stores details about employees, including their names, birth dates, gender, salary, assigned branch, and supervisor.
2. **branch**: Contains branch details like branch name, manager ID, and the start date for the manager.
3. **client**: Records information about the company’s clients, including client name and the branch they work with.
4. **works_with**: Represents the relationship between employees and clients, including the total sales amount between each employee-client pair.
5. **branch_supplier**: Details the suppliers for each branch, including the type of supplies provided.

Each table is connected through foreign keys to enforce referential integrity, with cascading delete or set-null actions for dependent rows when parent rows are deleted.

## Schema Structure

- **employee**
    - `emp_id` (INT): Primary Key, unique identifier for each employee.
    - `first_name` (VARCHAR(40)): Employee’s first name.
    - `last_name` (VARCHAR(40)): Employee’s last name.
    - `birth_date` (DATE): Employee’s birth date.
    - `sex` (VARCHAR(1)): Employee's gender.
    - `salary` (INT): Employee’s salary.
    - `branch_id` (INT): Foreign Key, references `branch_id` in `branch` table.
    - `super_id` (INT): Foreign Key, self-referencing the `emp_id` of a supervisor.

- **branch**
    - `branch_id` (INT): Primary Key, unique identifier for each branch.
    - `branch_name` (VARCHAR(40)): Name of the branch.
    - `mgr_id` (INT): Foreign Key, references `emp_id` in `employee`, representing the branch manager.
    - `mgr_start_date` (DATE): Start date of the manager.

- **client**
    - `client_id` (INT): Primary Key, unique identifier for each client.
    - `client_name` (VARCHAR(40)): Name of the client.
    - `branch_id` (INT): Foreign Key, references `branch_id` in `branch`.

- **works_with**
    - `emp_id` (INT): Foreign Key, references `emp_id` in `employee`.
    - `client_id` (INT): Foreign Key, references `client_id` in `client`.
    - `total_sales` (INT): Total sales made by the employee to the client.

- **branch_supplier**
    - `branch_id` (INT): Foreign Key, references `branch_id` in `branch`.
    - `supplier_name` (VARCHAR(40)): Name of the supplier.
    - `supply_type` (VARCHAR(40)): Type of supplies provided by the supplier.

## Relationships and Constraints

- **Cascade Deletes**:
  - If an employee or client is deleted, their related entries in `works_with` are automatically removed.
  - If a branch is deleted, associated suppliers in `branch_supplier` are automatically removed.

- **Set Null on Delete**:
  - If a branch or manager is removed, dependent fields (`branch_id`, `mgr_id`) in related tables are set to `NULL` rather than deleted.

## Getting Started

1. Clone this repository.
2. Run the SQL scripts to create the tables and add constraints.
3. Use these tables to manage employee-client relationships, track sales, and maintain branch and supplier data.

---

This database schema is ideal for managing sales data and relationships in a structured and organized format, ensuring data integrity through constraints and foreign keys.

## License

This project is licensed under the MIT License.
