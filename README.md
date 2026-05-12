# Huang Niting IT Product Manager assessment answer
1.	User Roles and Core Scenarios

Role A: Customer  
The primary driver of revenue. An external end-user whose primary objective is to discover, select, and acquire products through the platform.  
Core Scenarios:  
•	Searching for specific items or browsing categories to find products.  
•	Viewing product details (price, description, stock) and adding items to a virtual cart.  
•	Entering shipping details and completing a secure payment.  
•	Receiving order confirmations and tracking the status of their shipment until delivery.

Role B: Operations Staff  
An internal business user responsible for the day-to-day maintenance of the product catalogue and the physical fulfilment of customer orders.  
Core Scenarios:  
•	Creating new product listings, uploading images, and adjusting prices or descriptions.  
•	Updating stock levels to prevent "overselling" (selling items that aren't in the warehouse).  
•	Viewing new "Paid" orders, preparing the physical package, and updating the status to "Shipped" with tracking info.  
 
Role C: Platform Admin  
An internal business user who controls user permissions and settings to keep the platform secure.  
Core Scenarios:  
•	Creating and managing accounts for Operations Staff (e.g., giving a new employee "Merchant" permissions).  
•	Monitoring total sales volume and identifying system errors (e.g., failed payments).  
•	Manually intervening in "abnormal" orders, such as processing a refund or cancelling a fraudulent transaction.<br><br>
  
  
2.	MVP Feature List and Priority  

| Module        | Feature             | Priority | Reason                                                                                                                                                                                                                                                                                                                                |
| ------------- | ------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Customer Side | Login/Registration  | P1       | The feature improves the user experience by allowing customers to save shipping and payment preferences, but is categorized as P1 to ensure development focus remains on the core transaction flow first.                                                                                                                             |
| Customer Side | Product List        | P0       | The feature is essential for the Browse step as customers cannot buy what they cannot see.                                                                                                                                                                                                                                            |
| Customer Side | Product Detail Page | P0       | The feature is essential for the Browse step as customers need to confirm product specs and prices before add to cart.                                                                                                                                                                                                                |
| Customer Side | Product Search      | P1       | The feature significantly improves browse efficiency as the product catalog grows.                                                                                                                                                                                                                                                    |
| Customer Side | Shopping Cart       | P0       | The feature is essential for the Add to Cart step to store intent before checkout.                                                                                                                                                                                                                                                    |
| Customer Side | Submit Order        | P0       | The feature is essential for the Submit Order step to bridge selection and payment, and the feature creates the official order record.                                                                                                                                                                                                |
| Customer Side | Payment             | P0       | The feature is fundamental to the transaction flow; the business cannot collect revenue without it.                                                                                                                                                                                                                                   |
| Customer Side | Order List          | P1       | The feature is important for improving customers experience  and operational efficiency by providing a self-service portal where customers can independently track their order details and status without needing to submit manual inquiries.                                                                                         |
| Customer Side | Cancel Order/Refund | P1       | The feature is an important self-service tool for customers to resolve transaction errors. It reduces the manual support burden on operations staff, which improve both customer experience and operational efficiency.                                                                                                               |
| Admin Side    | Product Management  | P0       | The feature directly enables the 'Browse' steps of the core transaction flow, from Admin Side, by providing the essential data (e.g., pricing, descriptions and images) needed for customer browsing.                                                                                                                                 |
| Admin Side    | SKU                 | P0       | The feature is essential for tracking product availability in real-time, preventing the platform from selling out-of-stock items and ensuring the "Ship" stage can be fulfilled.                                                                                                                                                      |
| Admin Side    | Order Management    | P0       | Essential for staff to see, verify, and move orders through the "Ship" step.                                                                                                                                                                                                                                                          |
| Admin Side    | Shipment Management | P0       | The feature is essential to complete order processing, warehousing, carrier selection, and tracking to ensure successful shipments, and it is the final stage of the core flow ("Ship-Complete").                                                                                                                                     |
| Admin Side    | User Management     | P2       | The feature includes manage user accounts to enhance user experience and data security, which serves as an internal administrative tool rather than a transactional necessity; for an MVP, user permissions can be managed via a single shared credential or manual backend entries until organizational growth for future iteration. |
| Admin Side    | Data Dashboard      | P2       | The feature focuses on long-term business intelligence and strategic growth rather than the immediate functional success of the Browse-to-Complete Order transaction flow.                                                                                                                                                            |


3.	Core Process Design

A: Customer order and payment process  
Process in details:  
•	Customer browses Product List and selects an item.  
•	Customer enters Product Detail Page and adds the item to the Shopping Cart.  
•	Customer clicks Submit Order, creating an order record in the database.  
•	Customer proceeds to Payment and enters payment information.  
•	System receives a "Success" signal from the payment gateway.  
•	Order status updates to Paid; inventory is officially deducted.  
Exception scenarios:  
•	Payment Failure: If the card is declined, the status remains Pending Payment, and the user is prompted to try a different method.  
•	Payment Timeout: If the user doesn't pay within a set time, the order is automatically cancelled, and the locked inventory is released.  
•	Product out-of-stock in shopping carts: If staff removes a product while it's in a user's cart, the checkout process must flag the item as "Unavailable" before the user can submit the order, so customer cannot move to payment stage.  
Status Changes:  
•	Pending payment – Paid (Success)  
•	Pending payment– Order cancelled (Timeout/User action)  






