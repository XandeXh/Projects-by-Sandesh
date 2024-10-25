# Projects-by-Sandesh
Data / Business Analytics Projects

--Data refining of Invoice table in SQL to include columns required for the project
SELECT 
  i.InvoiceId, 
  i.CustomerId, 
  c.FirstName || ' ' || c.LastName as [Name], 
  ---concatenated first and last names from table c
  --date(i.InvoiceDate) as [Date],  -- removing time from datetime
  strftime ('%Y', i.InvoiceDate) as [Year], 
  --Convert date to just year
  strftime('%m', i.InvoiceDate) AS Month, 
  -- Extract month
  --i.BillingCity as [City],
  ---BillingState
  --i.BillingCountry as Country,
  IFNULL(i.BillingCity, 'Unknown') AS City, 
  IFNULL(i.BillingCountry, 'Unknown') AS Country, 
  --BillingPostalCode
  i.total, 
  CASE --creating quarters
  WHEN CAST(
    strftime('%m', i.InvoiceDate) AS INTEGER
  ) <= 3 THEN 1 -- Q1
  WHEN CAST(
    strftime('%m', i.InvoiceDate) AS INTEGER
  ) > 3 
  AND CAST(
    strftime('%m', i.InvoiceDate) AS INTEGER
  ) <= 6 THEN 2 -- Q2
  WHEN CAST(
    strftime('%m', i.InvoiceDate) AS INTEGER
  ) > 6 
  AND CAST(
    strftime('%m', i.InvoiceDate) AS INTEGER
  ) <= 9 THEN 3 -- Q3
  ELSE 4 -- Q4
  END AS Quarter 
FROM 
  Invoice as i 
  Inner Join Customer as c On i.CustomerId = c.CustomerId


  --Refining the Customers table in SQL to only include relevant fields
SELECT 
  c.CustomerId, 
  -- key for connection
  c.SupportRepId, 
  --key for connection
  --FirstName,
  --LastName,
  c.FirstName || ' ' || c.LastName as [Customer Name], 
  -- concatenated the first and last name for ease
  e.FirstName || ' ' || e.LastName as [Employee Name], 
  --Company,
  --Address,
  --c.City,
  --State,
  --c.Country,
  IFNULL(c.city, 'Unknown') AS City, 
  IFNULL(c.country, 'Unknown') AS Country --PostalCode,
  --Phone
  --Fax
  --Email,
From 
  Customer as c --Table to derive output from
  INNER JOIN Employee as e On c.SupportRepId = e.EmployeeId

  -- Refining the Track table in SQL to include relevant fields
SELECT 
  TrackId, 
  GenreID, 
  Name as [Track Name], 
  --AlbumId, 
  --MediaTypeId,
  --Composer
  --Milliseconds,
  --Bytes,
  UnitPrice as EA 
FROM 
  Track


