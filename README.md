-- Question 1: Top 5 customers with the highest total bill amount

SELECT CustomerID, SUM(TotalAmount) AS TotalSpent
FROM bills
GROUP BY CustomerID
ORDER BY TotalSpent DESC
LIMIT 5;

-- Question 2: Average time taken to pay bills for each customer
SELECT CustomerID, 
       AVG(DATEDIFF(BillDate, DueDate)) AS AvgPaymentDelay
FROM bills
WHERE Status = 'Paid'
GROUP BY CustomerID;

-- Question 3: Customers with no late payments
SELECT DISTINCT CustomerID
FROM bills
WHERE DATEDIFF(DueDate, BillDate) >= 0;

-- Question 4: Total amount generated
SELECT SUM(LineTotal) AS TotalRevenue
FROM bill_items;

-- Question 5: Item with the highest Line Total
SELECT ItemID, MAX(LineTotal) AS HighestLineTotal
FROM bill_items
GROUP BY ItemID
ORDER BY HighestLineTotal DESC
LIMIT 1;

-- Question 6: Item with the minimum Line Total
SELECT ItemID, MIN(LineTotal) AS LowestLineTotal
FROM bill_items
GROUP BY ItemID
ORDER BY LowestLineTotal ASC
LIMIT 1;

-- Question 7: Most popular payment method
SELECT PaymentMethod, COUNT(*) AS UsageCount
FROM payment
GROUP BY PaymentMethod
ORDER BY UsageCount DESC
LIMIT 1;

-- Question 8: Total revenue by payment method
SELECT PaymentMethod, SUM(Amount) AS TotalRevenue
FROM payment
GROUP BY PaymentMethod;

-- Question 9: Average payment amount
SELECT AVG(Amount) AS AveragePayment
FROM payment;

-- Question 10: Top 3 categories with the highest total revenue
SELECT CategoryID, SUM(TotalAmount) AS TotalRevenue
FROM bills
GROUP BY CategoryID
ORDER BY TotalRevenue DESC
LIMIT 3;

-- Question 11: Customer with the highest number of unpaid bills
SELECT CustomerID, COUNT(*) AS UnpaidBillCount
FROM bills
WHERE Status = 'Unpaid'
GROUP BY CustomerID
ORDER BY UnpaidBillCount DESC
LIMIT 1;
