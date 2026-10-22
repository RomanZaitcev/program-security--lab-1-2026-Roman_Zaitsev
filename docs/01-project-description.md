# 01. Project Description

## 1. Purpose

Service Manager is a web application that automates daily work of small service centers and equipment repair workshops. It replaces paper logs and Excel spreadsheets with a single system for orders, clients, repair statuses and spare-parts inventory.

## 2. Problem statement

- Small workshops keep records in notebooks or spreadsheets, so the history of work on a client's device is hard to find.
- Managers cannot see the current repair stage and must ask technicians for updates.
- Spare parts and consumables (screens, toner, thermal paste) are not tracked precisely, which causes losses.
- Receipts and completion reports are filled in manually and take a lot of time.
- Large CRM systems are expensive, hard to configure and contain features a workshop never uses.

## 3. Scope

### In scope
- Authorization with two roles: **Manager** and **Technician**.
- Repair order registration and status tracking.
- Client database with repair history.
- Inventory of spare parts and services, with automatic stock deduction.
- Generation of printable documents: Acceptance Receipt and Certificate of Completion.
- Dashboard with basic statistics.

### Out of scope
- Online payments and accounting.
- Customer self-service portal.
- Native mobile applications (the web interface is responsive instead).
- Integration with external suppliers.

## 4. Stakeholders

| Stakeholder | Interest |
|---|---|
| Workshop owner | Lower losses, control over operations, no subscription fees |
| Manager | Fast order intake, client lookup, printed documents |
| Technician | Clear task queue, easy status and parts logging |
| Developer | Maintainable code, clear requirements |
| Project supervisor | Compliance with course requirements |

## 5. Constraints

- Platform: .NET, C#, MVC pattern.
- Database: SQL Server or SQLite.
- Client: any modern web browser on any OS.
- Source code stored on GitHub.

## 6. Schedule

| Phase | Description | Dates |
|---|---|---|
| 1 | Operational logic, database schema, interface mockups | 22.09.26 - 08.10.26 |
| 2 | Application development | 09.10.26 - 15.11.26 |
| 3 | Testing, refinement, documentation | 16.11.26 - 30.11.26 |
