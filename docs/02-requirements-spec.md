# 02. Requirements Specification

## 1. User roles

- Manager - accepts devices, creates and assigns orders, manages clients, prints documents, sees prices and statistics.
- Technician - sees only assigned orders, changes statuses, adds comments, logs used parts.

## 2. Functional requirements

FR-1. The system shall authenticate users by username and password.
FR-2. The system shall restrict functions by role; a Technician shall see only orders assigned to them.
FR-3. A Manager shall be able to create an order (client, device model, fault description) and assign it to a Technician.
FR-4. The system shall support the statuses Received, Queued, Diagnostics, Awaiting Parts, Repaired, Released, and record the time of every status change.
FR-5. An authorized user shall be able to add comments to an order.
FR-6. The system shall store client name and contact details, find a client by phone or name, and show the client's repair history.
FR-7. When creating an order, the system shall reuse an existing client found by phone number, otherwise create a new one.
FR-8. The system shall keep a list of parts and services with quantity and price.
FR-9. When a Technician adds a part to an order, the system shall reduce stock by that quantity and reject the operation if stock is insufficient.
FR-10. The system shall store the part price at the time of repair and recalculate the order total.
FR-11. The system shall generate printable documents: Acceptance Receipt and Certificate of Completion.
FR-12. The main page shall show the number of devices under repair and the number of new orders.

## 3. Non-functional requirements

NFR-1. The system shall validate all form input (e.g. phone format, no negative price or quantity) and show an error message instead of failing.
NFR-2. The interface shall be usable without special training and adapt to desktop and smartphone screens.
NFR-3. The client shall work in modern browsers on any operating system.
NFR-4. The code shall follow the MVC pattern.
NFR-5. Search and page loading should complete within 2 seconds under normal load.

## 4. Acceptance criteria

The system is accepted after simulating a working day: create a client, accept a device, change statuses, log parts, print the final document. It must work stably and handle incorrect input without crashing.