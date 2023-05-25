# This project consists of 5 tables, namely:

### 1. Customers 
### Transacations
### Products
### Markets
### Date

## Foremost if u want to try to modify any table use this format it can help to undo your actions -
```sql
BEGIN TRANSACTION; -- Start a transaction

-- Your UPDATE statement that made the changes
UPDATE YourTable
SET YourColumn = 'NewValue'
WHERE YourCondition;

-- Rollback the transaction to undo the changes
ROLLBACK;

-- Optional: COMMIT; -- If you want to commit the changes instead of rolling them back

```
# :one: Customers Table Modification

### In the Customers table, there is a column named "customer_type" that initially had the value "E-commerece".

### It has been updated to "E - Commerece" using the following SQL statement:



```sql
select * from customers

UPDATE customers
SET customer_type = REPLACE(customer_type, 'E-', 'E - ')
WHERE customer_type LIKE 'E-%';
```
# :two: Date Table Modification
In the Date table, there is a column named "date_yy_mmm" that initially had the value "17-Jun\r". It has been updated to "17 -Jun" using the following SQL statement:

```sql
UPDATE date
SET date_yy_mmm = CONCAT(
    LEFT(date_yy_mmm, 2), ' - ', SUBSTRING(date_yy_mmm, 4, LEN(date_yy_mmm) - 5)
)
```
##update date
 ## SET date = FORMAT(CONVERT(DATE, date), 'dd MMMM yyyy')
## remaining -------2017-06-01 to 01 june 2017--------------



# :three: Market Table Modification
### In the Date table, there is a column named "zone" that initially had the value "Blank columns". 

### It has been updated to remove blank columns using the following SQL statement:

```sql
--- GOT ALL DATA WHICH HAS NOT ANY BLANK VALUES

select * from markets where zone <> ' '

-- CREATED A FILTERED TABLE FOR FUTURE ANANYLISIS

SELECT markets_code,markets_name,zone
INTO Markets_filtered
FROM markets
where zone <> ' '

--CHECKED NEW FILTERED DATA 

select * from Markets_filtered
```


# :four: Products Table Modification
In the Date table, there is a column named "product_type" that initially had the values like "Distribution\r ". It has been updated to "Distribution" columns like these using the following SQL statement:

```sql
UPDATE products
SET product_type = REPLACE(product_type, '\r', '')
WHERE product_type LIKE '%\r%'
```

# :five: Transactions Table Modification
In the Date table, there is a column named "product_type" that initially had the values like "Distribution\r ". It has been updated to "Distribution" columns like these using the following SQL statement:

```sql
--IF USD THEN 80 MULTIPLY & CREATED NORM_SLAES_ANOUMT


select DISTINCT product_code,customer_code,market_code,order_date,sales_qty,profit_margin_percentage,profit_margin,cost_price,cast(sales_amount as int) as sales_amount_new ,currency,
case when currency = 'USD' then CAST(sales_amount * 80 AS INT) else cast(sales_amount as int)  end as norm_sales_amount 
from transactions

--CREATED A FILTERED TABLE FOR FUTURE ANANYLISIS

SELECT DISTINCT product_code, customer_code, market_code, order_date, sales_qty, profit_margin_percentage,
       profit_margin, cost_price, CAST(sales_amount AS INT) AS sales_amount_new, currency,
       CASE WHEN currency = 'USD' THEN CAST(sales_amount * 80 AS INT) ELSE CAST(sales_amount AS INT) END AS norm_sales_amount
INTO transactions_FILTERED
FROM transactions


```
duplicate colmns



