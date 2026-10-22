# 04. Business Logic

## 1. Request dispatching
1. Initialize the database connection and load the configuration.
2. Wait for a user request and check for an active session.
3. If there is no session, call authorization. On success determine the role (Manager or Technician) and open the matching dashboard.
4. Route the command to the right subsystem: clients, orders, inventory or documents.

## 2. Order and client registration (Manager)
1. Read data from the form: full name, phone, device model, problem description.
2. Validate: phone format, mandatory fields not empty. On error return a message.
3. Search the client by phone. If not found, create a new client; otherwise take the existing ID.
4. Create the order with status **Received**, client ID and current date/time, and save it.

## 3. Status change
1. User opens an order.
2. The system checks that the user may change this order (Technician only for assigned orders).
3. The new status and time of the change are saved and, optionally, a comment.

## 4. Parts write-off and cost calculation (Technician)
1. Receive order ID, part code and required quantity.
2. Read current stock and price of the part.
3. If stock is less than the requested quantity, show an error and cancel.
4. Otherwise reduce stock, save a record in the used-parts table with the price at the time of repair, and recalculate the order total.

## 5. Document generation (Manager)
1. Receive order ID and document type: Acceptance Receipt or Certificate of Completion.
2. Read the order and client data.
3. For the Certificate, read all used parts of the order and calculate the total as the sum of quantity x price.
4. Fill the HTML template and show it for printing.

## 6. Business rules

| ID | Rule |
|---|---|
| BR-1 | Stock cannot become negative. |
| BR-2 | The price of a used part is fixed at the moment of use. |
| BR-3 | A Technician cannot see or change orders that are not assigned to them. |
| BR-4 | Every status change is recorded with time. |
| BR-5 | An order moves through statuses in the defined sequence. |
