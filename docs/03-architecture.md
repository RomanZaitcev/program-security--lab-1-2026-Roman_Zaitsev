# 03. Architecture Description

## 1. Stakeholders and concerns

Workshop owner - Cost, reliability, protection of stock.
Manager - Speed of order intake, correct documents.
Technician - Simple status and parts logging.
Developer - Modularity, maintainability.

## 2. Architectural decisions

- **Style:** client-server web application, accessed from any device via browser.
- **Pattern:** Model-View-Controller, to separate data, logic and presentation.
- **Back-end:** .NET, C#.
- **Front-end:** HTML, CSS, JavaScript.
- **Database:** relational (SQL Server or SQLite).

## 3. Data view

Main entities: USER (username, password hash, role), CLIENT (name, phone), ORDER (device, problem, status, dates, total), PART (code, name, quantity, price), ORDER_PART (quantity, price at repair).

## 4. Deployment view

One server runs the .NET application and the database. Users connect through a browser over HTTPS.