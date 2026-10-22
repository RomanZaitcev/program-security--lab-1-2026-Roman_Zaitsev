# 02. Requirements Specification

Prepared in the spirit of ISO/IEC/IEEE 29148:2018. Each requirement has a unique ID, is a single verifiable statement, and has a priority (M = must, S = should).

## 1. Definitions

| Term | Meaning |
|---|---|
| Order | A repair request for one device from one client |
| Manager | User who accepts devices, creates orders and manages clients |
| Technician | User who performs repairs and logs used parts |
| Part | Spare part or consumable stored in inventory |

## 2. User roles

| Role | Rights |
|---|---|
| Manager | Create/edit orders, manage clients, view all orders, prices and statistics, generate documents |
| Technician | View only assigned orders, change status, add comments, log used parts |

## 3. Functional requirements

### 3.1 Authorization and roles
| ID | Requirement | Pri |
|---|---|---|
| FR-1 | The system shall authenticate users by username and password. | M |
| FR-2 | The system shall restrict functions according to the user's role (Manager or Technician). | M |
| FR-3 | A Technician shall see only orders assigned to them. | M |
| FR-4 | The system shall end a session after a period of inactivity. | S |

### 3.2 Order management
| ID | Requirement | Pri |
|---|---|---|
| FR-5 | A Manager shall be able to create an order with client, device model and fault description. | M |
| FR-6 | The system shall support the statuses: Received, Queued, Diagnostics, Awaiting Parts, Repaired, Released. | M |
| FR-7 | An authorized user shall be able to change the status of an order and the system shall record the time of the change. | M |
| FR-8 | An authorized user shall be able to add comments to an order. | M |
| FR-9 | A Manager shall be able to assign an order to a Technician. | M |

### 3.3 Client database
| ID | Requirement | Pri |
|---|---|---|
| FR-10 | The system shall store client name and contact details. | M |
| FR-11 | The system shall find a client by phone number or name. | M |
| FR-12 | The system shall show the complete repair history of a client. | M |
| FR-13 | When creating an order, the system shall reuse an existing client found by phone number, otherwise create a new client. | M |

### 3.4 Inventory
| ID | Requirement | Pri |
|---|---|---|
| FR-14 | The system shall keep a list of parts and services with quantity and price. | M |
| FR-15 | When a Technician adds a part to an order, the system shall reduce the stock by that quantity. | M |
| FR-16 | The system shall reject the operation if the requested quantity exceeds current stock. | M |
| FR-17 | The system shall store the part price at the time of repair and recalculate the order total. | M |

### 3.5 Documents
| ID | Requirement | Pri |
|---|---|---|
| FR-18 | The system shall generate a printable Acceptance Receipt from order data. | M |
| FR-19 | The system shall generate a printable Certificate of Completion listing used parts and the total cost. | M |

### 3.6 Dashboard
| ID | Requirement | Pri |
|---|---|---|
| FR-20 | The main page shall show the number of devices currently under repair and the number of new orders. | S |

## 4. Non-functional requirements

| ID | Category | Requirement | Pri |
|---|---|---|---|
| NFR-1 | Reliability | The system shall validate all form input (e.g. phone format, no negative price or quantity) and show an error message instead of failing. | M |
| NFR-2 | Availability | The system should be available 24/7 during workshop operation. | S |
| NFR-3 | Usability | The interface shall be usable by workshop staff without special training. | M |
| NFR-4 | Portability | The client shall work in modern browsers on any operating system. | M |
| NFR-5 | Responsiveness | The layout shall adapt to desktop and smartphone screens. | M |
| NFR-6 | Maintainability | The code shall follow the MVC pattern. | M |
| NFR-7 | Performance | Search and page loading should complete within 2 seconds under normal load. | S |
| NFR-8 | Security | Security requirements in [06-security.md](06-security.md) shall be satisfied. | M |

## 5. Data input and output

- Input: web forms in the browser.
- Output: tables, order cards and HTML pages prepared for printing.
- Storage: relational database.

## 6. Acceptance criteria

Acceptance is performed by simulating a working day (see [07-testing.md](07-testing.md)): create a client, accept a device, change statuses, log parts, print the final document. The system is accepted when it works stably and handles incorrect input without crashing.

## 7. Traceability

| Subsystem | Requirements |
|---|---|
| Authorization | FR-1..FR-4 |
| Orders | FR-5..FR-9 |
| Clients | FR-10..FR-13 |
| Inventory | FR-14..FR-17 |
| Documents | FR-18..FR-19 |
| Dashboard | FR-20 |
