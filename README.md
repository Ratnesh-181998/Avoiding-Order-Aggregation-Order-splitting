Avoiding Order Aggregation/Order-splitting :  

Business Requirement: 

Currently the buyer visits the marketplace to select the product of interest in order to add it to the cart 
and initiate the procurement process. The product selected can be procured directly from marketplace if 
it falls under a specified limit. Any procurement that breach this limit has to be done under the bidding 
process. To avoid this buyer goes with multiple direct purchases. The bid of more value requires an 
approval from the higher authority, to bypass this multiple bids with smaller quantity is placed. 
Avoiding order aggregation is the method using which the buyer is splitting a larger order to multiple 
small orders. GeM wants to identify and alert the buyers who are avoiding order aggregation. Orders 
splitting can be for done in the following ways: 

<img width="1352" height="1373" alt="image" src="https://github.com/user-attachments/assets/84887288-d645-4a8a-a4cc-8de7a3fdbf3f" />


• Splitting an order of potential bid into multiple direct procurement; this is the case where the 
requirement of solution to detect such cases.  
• Splitting an order of potentially high bid into similar smaller bids; not in the scope of this 
solution. 
The splitting of the bid into multiple direct procurement can be done to avoid the long processing period 
involved in a bidding process or to procure the same product/services for different consignees. The act 
of splitting the order because of the above reason might save some time but eliminates the competition 
(in case of purchase under 25K) and best price discovery possible in bidding. The splitting of a bid into 
multiple bids with smaller value is done to bypass the requirement of permission from superior financial 
authority. This can allow a buyer to procure a product above the authorized limit and bypass his 
superiors. 
Requirement as per RFP: Detect and Report patterns to identify large orders break down into several 
smaller portions and buying repeatedly to avoid tendering. 

<img width="2247" height="1216" alt="image" src="https://github.com/user-attachments/assets/9f9e4af0-5d31-4721-bcc1-d49487c562b3" />

Proposed solution: 

Similar to Buyer Seller Collusion, idea is to let data define the rules of order aggregation. Different levels 
of data like inter-purchase interval (time between two purchases in the same category), % of 
transactions that are non-competitive (either non-L1 or higher priced than historical transactions), # of 
unique sellers being transacted with, etc. will be used together to set thresholds based on data to define 
buyer behavior that considered as avoiding order aggregation. 
The monthly report of suspected buyers shared to GeM SPV and by taking corrective action against 
suspected buyers leads to increase order aggregation, competitive price for the products and reduce the 
chances of seller buyer collusion.

Data: 

To build this solution, data is extracted from following database table  
• ffm_order 
• ffm_orderitem 
• ffm_buyer 
• ffm_consignee  
And the required data is as below  
• order_id 
• category_id 
• product_id 
• product_name 
• quantity 
• unit_price 
• order_amount 
• buyer_id 
• seller_id 
• order_placed 
• buying_mode 
• buyer_organizationName 
• buyer_departmentName 
• consignee_id 

Model Methodology:  

The required data is extracted from database; The data is processed and categories such as custom and 
BOQ gets excluded, Buyer behavior and categorical behavioral is achieved from data processing.  
Similar to collusion there are two methods in which we can find out collusion. Initially using Machine 
learning module created to identify the suspected transactions. But later by discussing with GeM the 
rule based approach was defined and finalized to get outcome which provides better expected result.    
1. Rule Based model (Suggested by GeM) 
2. Machine learning model (Unsupervised model)

Steps In Model:  

1. Extract data from database 
2. Data pre-processing 
3. Get Buyer behavior 
4. Get Category Behavior 
5. Get buyer-category behavior  
6. Data processing and aggregation; and apply rule based approach. 
7. Create final report

<img width="1410" height="1007" alt="image" src="https://github.com/user-attachments/assets/12978a3b-c9dd-441d-bbec-b566548801ff" />

Business Value: 

1. Improved Transparency and Efficiency in Public Procurement: The solution aligns with GeM's 
objective of enhancing transparency and efficiency in public procurement by identifying malicious 
activities.  
2. Promotes Bid process: Solution helps buyer to create bids by prohibiting splitting of transactions 
through direct purchase. Bidding encourages suppliers to compete, which can lead to innovation 
and lower prices to ensure fairness on portal by allowing all interested parties to participate. 

Solution Consumption: 

Currently, this solution is consumed through BI dashboards which is accessible GeM team. Dashboard is 
updated at monthly level having a report of suspected buyers along with transaction, category and seller 
details. Below is the screenshot of dashboard:

<img width="1368" height="459" alt="image" src="https://github.com/user-attachments/assets/0386af81-9ba3-476a-96fe-3c73add4ca99" />


Integration & API: Developed and integrated using FlaskAPI.

Input: 

<img width="1244" height="634" alt="image" src="https://github.com/user-attachments/assets/ba1e407f-5244-408e-8d35-b329049e998b" />

Output: 

<img width="1304" height="320" alt="image" src="https://github.com/user-attachments/assets/ef76d5ad-b1af-4d2a-b1f2-2b81db5f4acc" />



