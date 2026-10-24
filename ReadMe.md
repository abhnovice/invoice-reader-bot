 ## Invoice Reader Bot
 ### This is used to batch read invoices generated at SKU-Del. Date-Price level to analyze the possibility of claims

 ### 1. Business Problem
In a supply chain, there could be possibility of claims related to logistics, pricing or a multitude of other reasons and the high volume of invoice processing in demand driven industries makes it imperative to keep a close track on this flow and address discrepancies asap to mitigate or reduce financial damage.

  #### 2. Context and Assumptions

A situation of being able to digitize invoices in a batch and compare it with the real prices.

a. Pricing dataset quality
b. Accuracy of Invoices
c. Access to tech stack
 
 ### 3. Data 
 It is a synthetic dataset taken from kaggle: 
 https://www.kaggle.com/datasets/devp1866/high-quality-ocr-ready-invoice-pdfs?select=Batch+1
 
 ### 4. Supply Chain Logic 
 
The core decision is a deterministic reconciliation, not an LLM judgment:
1. Select the business date. Use the actual delivery date if it is present and trusted. If the invoice only contains an invoice date, mark that as a fallback and confirm that the contract uses invoice date for price selection. The date basis must be configurable and documented.
2. Find the applicable price. Match the normalized SKU, supplier/price list, currency, unit of measure, and any required location against a reference-price record whose validity period includes the selected date:
   effective_from <= selected_date <= effective_to
3. Calculate the expected line amount. For a simple unit-price case:
   expected_line_amount = invoice_quantity × agreed_unit_price
   If the invoice has a different billing unit, pack conversion, discount, tax, or freight treatment, apply a separately defined rule before comparing. Do not silently assume those components are included in the agreed price.
4. Calculate variance.
   unit_price_variance = invoiced_unit_price − agreed_unit_price
   amount_variance = invoiced_line_amount − expected_line_amount
   Positive amount variance means the invoice is higher than the reference calculation; negative variance means it is lower. Currency rounding should be applied consistently at the business-approved precision.
5. Assign a review outcome. Flag a price discrepancy when the absolute variance exceeds a configured tolerance. Treat missing/ambiguous matches, invalid quantities, currency/UOM mismatches, and low-confidence extraction as exceptions rather than as zero variance.
The tolerance should account for permitted rounding and contract terms. Until stakeholders define it, the prototype should expose the tolerance as a configuration value and label results as exploratory. A reviewer should confirm the contract, receipt, tax/discount treatment, and any approved exceptions before raising or rejecting a claim.
 
 ### 5. Approach 
 
Explain how the project works in simple steps. 
 
 ### 6. Project Structure 
 
Briefly explain the important folders and files. 
 
 ### 7. How to Run 
 
```bash 
# Add setup and run commands here
```
### 8. Results
```bash
#Main Outputs, Charts, Findings
```
### 9. Business Value
```bash
#Explanation on how the work helps the business with the stakeholders involved (DILO, WILO, MILO etc)
```
### 10. Limitations
Explain what the project does not cover in bullet points

### 11. What I built and Learnt
5-7 bullet points

### 12. Next Steps
```bash
#### IMPROVEMENT-1

#### IMPROVEMENT-2
```
