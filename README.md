# Huang Niting IT Product Manager assessment answer
1.	User Roles and Core Scenarios

Role A: Customer  
The primary driver of revenue. An external end-user whose primary objective is to discover, select, and acquire products through the platform.  
Core Scenarios:  
•	Searching for specific items or browsing categories to find products.  
•	Viewing product details and adding items to a virtual cart.  
•	Entering shipping details and completing a secure payment.  
•	Receiving order confirmations and tracking the status of their shipment until delivery.

Role B: Operations Staff  
An internal business user responsible for the day-to-day activities of the product catalog and the physical fulfilment of customer orders.  
Core Scenarios:  
•	Creating new product listings, uploading images, and adjusting prices or descriptions.  
•	Updating stock levels to prevent overselling.
•	Viewing new paid orders, preparing the physical package, and updating the status to Shipped with tracking information.  
 
Role C: Platform Admin  
An internal business user who controls user permissions and settings to keep the platform secure.  
Core Scenarios:  
•	Creating and managing accounts for Operations Staff.
•	Monitoring total sales volume and identifying system errors.
•	Manually intervening in abnormal orders, such as processing a refund or cancelling a fraudulent transaction.<br><br>
  
  
2.	MVP Feature List and Priority  

| Module        | Feature             | Priority | Reason                                                                                                                                                                                                                                                                                                                                |
| ------------- | ------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Customer Side | Login/Registration  | P1       | The feature improves the user experience by allowing customers to save shipping and payment preferences, but is categorized as P1 to ensure development focus remains on the core transaction flow first.                                                                                                                             |
| Customer Side | Product List        | P0       | The feature is essential for the Browse step as customers cannot buy what they cannot see.                                                                                                                                                                                                                                            |
| Customer Side | Product Detail Page | P0       | The feature is essential for the Browse step as customers need to confirm product details and prices before add to cart.                                                                                                                                                                                                                |
| Customer Side | Product Search      | P1       | The feature significantly improves browse efficiency as the product catalog grows.                                                                                                                                                                                                                                                    |
| Customer Side | Shopping Cart       | P0       | The feature is essential for the Add to Cart step to store intent before checkout.                                                                                                                                                                                                                                                    |
| Customer Side | Submit Order        | P0       | The feature is essential for the Submit Order step to bridge selection and payment, and the feature creates the official order record.                                                                                                                                                                                                |
| Customer Side | Payment             | P0       | The feature is fundamental to the transaction flow; the business cannot collect revenue without it.                                                                                                                                                                                                                                   |
| Customer Side | Order List          | P1       | The feature is important for improving customers experience and operational efficiency by providing a self-service portal where customers can independently track their order details and status without needing to submit manual inquiries.                                                                                         |
| Customer Side | Cancel Order/Refund | P1       | The feature is an important self-service tool for customers to resolve transaction errors. It reduces the manual support burden on operations staff, which improve both customer experience and operational efficiency.                                                                                                               |
| Admin Side    | Product Management  | P0       | The feature directly enables the 'Browse' steps of the core transaction flow, from Admin Side, by providing the essential information needed for customer browsing.                                                                                                                                 |
| Admin Side    | SKU                 | P0       | The feature is essential for tracking product availability in real-time, preventing the platform from selling out-of-stock items and ensuring the Ship stage can be fulfilled.                                                                                                                                                      |
| Admin Side    | Order Management    | P0       | The feature is essential for staff to see, verify, and move orders through the Ship step.                                                                                                                                                                                                                                                          |
| Admin Side    | Shipment Management | P0       | The feature is essential to complete order processing, warehousing, carrier selection, and tracking to ensure successful shipments, and it is the final stage of the core flow (Ship-Complete).                                                                                                                                     |
| Admin Side    | User Management     | P2       | The feature includes manage user accounts to enhance user experience and data security, which serves as an internal administrative tool rather than a transactional necessity |
| Admin Side    | Data Dashboard      | P2       | The feature focuses on long-term business intelligence and strategic growth rather than the immediate functional success of the Browse-to-Complete Order transaction flow.                                                                                                                                                            |


3.	Core Process Design

A: Customer order and payment process  
Process in details:  
•	Customer browses Product List and selects an item.  
•	Customer enters Product Detail Page and adds the item to the Shopping Cart.  
•	Customer clicks Submit Order, creating an order record.  
•	Customer proceeds to Payment and enters payment information.  
•	System receives a "Success" signal from the payment gateway.  
•	Order status updates to Paid; inventory is officially deducted.  
Exception scenarios:  
•	Payment Failure: If the card is declined, the status remains Pending Payment, and the user is prompted to try a different method.  
•	Payment Timeout: If the user doesn't pay within a set time, the order is automatically cancelled, and the locked inventory is released.  
•	Product out-of-stock in shopping carts: If staff removes a product while it's in a user's cart, the checkout process must flag the item as "Unavailable" before the user can submit the order, so customer cannot move to payment stage.  
Status Changes:  
•	Pending payment – Paid (Success)  
•	Pending payment– Order cancelled (exception scenarios)  

B: Order shipment process  
•	Operations staff uses the Order Management feature to filter the system for orders with the status paid.  
•	Staff prepares the physical package. The Inventory Management feature ensures the stock is accurately decreased and reflects the physical count.  
•	Staff uses the Shipment Management feature to enter the tracking number and select the third-party carrier.  
•	The platform updates the status to shipped.  
•	Once the carrier confirms delivery, the status updates to completed.  
Exception Scenarios:  
•	If the staff finds the item is damaged or missing during packing, which causes insufficient inventory, then the order is flagged as abnormal/out of stock and the customer is notified.  
•	If the Shipment Management feature cannot validate the address with the carrier, the process pauses at the Paid status until the customer provides a corrected address.  
Status Changes:  
Paid – Preparing – Shipped -- Completed<br><br>

4.	Simplified PRD

Product Detail Page  
•	Feature background:  
The Product Detail Page is an important stage in the customer journey. It is where a user transitions from just browsing to intent to buy. The page must provide enough information to answer all customer questions and remove doubt from the Add to Cart action.
•	User Goal:  
As Customers, they want to view comprehensive details about a specific so that I can decide whether to add it to shopping cart and proceed to payment.
•	Page field:  

| Name                | Description                                                                                                                                    |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Product name        | The official title of the item                                                                                                                 |
| Images              | Product gallery (main image + thumbnails)                                                                                                      |
| Price               | Current selling price                                                                                                                          |
| Description         | Detailed specifications                                                                                                                        |
| SKU                 | Unique identifier for internal inventory tracking                                                                                              |
| Stock Status        | Indicates if the item is In Stock or Out of Stock.                                                                                         |
| Quantity Selector   | Plus and minus buttons to select numbers of items                                                                                              |
| Add to Cart/Buy now | Action button to make next moves of the purchase                                                                                               |
| Ratings and Reviews | A dedicated section displaying the cumulative star rating and qualitative customer feedback to build trust and assist in the browsing process. |  

•	Business Rules  

(1) Content on the Product Details Page can only be created and modified via the authenticated Product Management module. Access is restricted to staff with access permissions.  

(2) The system must verify the product status before enabling any transaction actions. If the status is anything other than on sale, the "Add to Cart" and "Buy Now" buttons must be disabled, and the status label must display "Product is off sale".  

(3) The page must perform a real-time check of the inventory level for the selected variant. If the stock level is less than or equal to 0, the system must block the purchase flow and display the exception message: "Insufficient inventory".  

(4) The user's selected purchase count is strictly limited by the available inventory levels. The quantity selector component must prevent the user from incrementing the value beyond the current stock count. If a user manually enters a number where intended purchase number is higher than stock, the system must return the error: "Purchase quantity exceeds available inventory".  
 

5.	API Understanding Question

(1)  
•	Product name: Bluetooth Earphones  
•	Product ID: 10001  
•	Status: on sale  
•	Current price: 19900 cents  
•	Original price: 29900 cents  
•	Total stock: 25  
•	Sales count: 132  
•	Images: The main product image via the provided URL.  
•	Product colour options: white and black  
•	White: SKU: 20001; Price: 19900 cents; Stock: 10  
•	Black: SKU: 20002; Price: 20900 cents; Stock: 15  
(2)  
Displayed price: $199.00
(3)  
On the one hand, the Add to Cart and Buy Now buttons must be disabled. On the other hand, a clear "Product Unavailable" or "Off-Sale" banner should appear prominently. If the product will be restocked, the product detail page still need to be remained. If, however, the product would not be restocked, the product detail page should ideally be removed from search results and the Product List module, so customers would not feel confused about the product.  

(4)  
•	The button should be disabled (non-clickable).  
•	The label should change from Add to Cart to Out of Stock. 
•	The purchase button should be replaced with a "Notify Me When Available" button to capture user interest.  

(5)   
•	Price: from $199.00 to $209.00  
•	Inventory: update to 15  

(6)  

| Missing field           | Why it matters                                                                                                                                                                                                                                  |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Product description     | A detailed description is essential for customers to understand the specific features and technical specifications of the earphones before they decide to buy. Description will change if customers click on different versions of the product. |
| Rating/Reviews          | Displaying social proof through star ratings and review counts builds consumer trust and increases the likelihood of a conversion. The field will change if customers click on different versions of the product.                               |
| Estimated Delivery Time | Providing a general delivery timeline on the product page helps manage customer expectations regarding when they will actually receive their order.                                                                                             |

6.	Simple Logic Reading Question

(1)  
This function is a backend validation check used to determine if a specific order request is eligible for submission based on product inventory. It is a standard before a customer can proceed to the payment stage, ensuring that staff can actually fulfill the order being placed.  
(2)  
According to the code logic, the order submission will fail under any of the following three conditions:  
•	Product Status: The product's status is anything other than on sale.
•	Zero Inventory: The specific SKU stock level is zero or less.  
•	Excessive Quantity: The quantity the user is attempting to purchase is greater than the current available stock.  
(3)  
canSubmit: false  
reason: Purchase quantity exceeds available inventory  
(4)  
•	Address Validation: To confirm that the physical location exists and is formatted correctly for mail carriers.  
•	Shipping validation: To ensure the specific items can be legally or physically delivered to that verified location.  
•	Minimum Order Threshold: Ensure the total order value meets any minimum spend requirements required by the platform for processing a transaction.  
•	Coupon and Promotion Validity: Re-validate any applied discount codes or promotional offers to ensure they have not expired and that the order still meets the necessary eligibility criteria (this can be considered after the initial version of platform).  


7.	Order Status Understanding Question  
(1)  
Pending Payment  
(2)  
Paid  
(3)  
Shipped  
(4)  
Cancelled
(5)  
Paid, Shipped, Cancelled  
(6)  
•	Pending Payment – Paid – Shipped – Completed;  
•	Pending Payment – Cancelled;  
•	Pending Payment – Paid – Refunding -- Refunded;  
•	Pending Payment – Paid – Shipped – Refunding – Refunded;  
•	Pending Payment – Paid – Shipped – Completed -- Refunding – Refunded.<br><br>


8.	Bug/Exception Analysis Question

•	Data Caching:  
Cause: The product detail page uses caching to improve performance. The inventory shown to the customer might be a cached snapshot that is several minutes old, while the actual backend database has already reached zero.  
How to investigate: Verifying if the Product Detail Page is serving inventory data from a cache with a long time, which would cause the frontend to display old information.  

•	Concurrent Orders:  
Cause: This occurs when multiple customers are viewing the same product simultaneously. In this scenario, another customer successfully placed an order for that last remaining item in the brief window of time between when the current user loaded the page and when they clicked Submit Order.  
How to investigate: Using Order Management feature to review the application logs to determine if another customer successfully completed an order for the remaining unit during the interval between the user’s page load and their order submission.  

•	Inventory Inconsistency:  
Cause: The product may have multiple versions. The frontend might be incorrectly displaying the total inventory for the parent product, while the specific SKU inventory selected by the user is actually out of stock.  
How to investigate: Utilize the platform's Inventory Management feature—designed for Operations Staff to manage stock—to perform a side-by-side verification between the Total Product Inventory and SKU-specific counts to determine if the frontend is pulling aggregate data while the Order API correctly validates against individual variants.  

•	Shopping Cart Data error:  
Cause: A product may have become invalid or out of stock while sitting in the user's shopping cart. If the system does not dynamically update the cart status, the user only discovers the inventory is gone when the order submission API performs its final mandatory check.  
How to investigate: Look at the user's session logs to see when the item was added to the cart, and compare the adding time with product invalid time.<br><br>


9.	Core Metrics Design

| Metric                | Meaning                                                                                                     | Why it matters                                                                                                                |
| --------------------- | ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Checkout abandon rate | The percentage of users who add items to their cart but do not reach the Submit Order stage.              | High abandonment indicates friction in the checkout process, such as unexpected costs, a complex form, or technical bugs.     |
| Stock-out rate        | The frequency with which customers attempt to buy an item only to receive an "Insufficient inventory" error | This measures the quality of inventory management feature. Frequent stock-outs lead to customer frustration. |
| Average Order Value   | The average amount spent each time a customer completes an order.                                           | It helps understand if your "Add to Cart" and "Browse" stages are encouraging users to buy more.                              |
| Return/Refund rate    | The percentage of completed orders that result in a customer requesting a return or refund.                | A high return rate signals problems with product quality or misleading product detail pages during the Browse stage.        |
| Repeat Purchase Rate  | The percentage of customers who return to place a second order after their first order is marked Complete | This measures long-term platform health. Getting them to return is how the platform becomes more profitable.                  |  

