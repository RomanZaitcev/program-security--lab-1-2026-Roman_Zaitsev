# 04. Business Logic

## 1. Order and client registration (Manager)
1. Read the form data: full name, phone, device model, problem description.
2. Validate the phone format and mandatory fields; on error return a message.
3. Find the client by phone; if not found, create a new client.
4. Create the order with status **Received**, the client ID and the current date and time.

## 2. Status change
1. The user opens an order; the system checks the user may change it (a Technician only for assigned orders).
2. The new status, its time and an optional comment are saved.

## 3. Parts write-off and cost calculation (Technician)
1. Receive the order ID, part code and quantity.
2. If stock is less than the quantity, show an error and cancel.
3. Otherwise reduce stock, save the used part with its current price, and recalculate the order total.

## 4. Document generation (Manager)
1. Receive the order ID and document type: Acceptance Receipt or Certificate of Completion.
2. Read the order and client data; for the Certificate also read the used parts and calculate the total (sum of quantity x price).
3. Fill the HTML template and show it for printing.

## 5. Business rules

1. Stock cannot become negative.
2. The price of a used part is fixed at the moment of use.
3. A Technician cannot see or change orders not assigned to them.
4. Every status change is recorded with its time.