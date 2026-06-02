# Data Dictionary

Full field definitions for all four tables in the star schema.

---

## fact_sales — 60,000 rows

| Field | Type | Description |
|---|---|---|
| `OrderLineID` | Integer | Unique identifier for each order line |
| `OrderID` | Integer | Parent order identifier (one order can have multiple lines) |
| `OrderDate` | Date | Date the order was placed (DD/MM/YYYY) |
| `CustomerID` | Integer | Foreign key → dim_customers |
| `City` | String | City of the customer |
| `Region` | String | Greek region (περιφέρεια) of the customer |
| `Channel` | String | Sales channel: `Online`, `Κατάστημα` (Store), `B2B` |
| `ProductID` | Integer | Foreign key → dim_products |
| `Units` | Integer | Quantity ordered |
| `UnitPrice` | Currency (€) | Selling price per unit after discount |
| `DiscountPct` | Percentage | Discount applied to the line |
| `Revenue` | Currency (€) | Net revenue: Units × UnitPrice × (1 − Discount) |
| `UnitCost` | Currency (€) | Cost per unit |
| `Cost` | Currency (€) | Total cost: Units × UnitCost |
| `Profit` | Currency (€) | Revenue − Cost |
| `PaymentMethod` | String | Payment used: Google Pay, Apple Pay, Κάρτα, PayPal, Αντικαταβολή, Τραπεζική Μεταφορά |
| `Returned` | Boolean | 1 if the order was returned, 0 otherwise |

---

## dim_date — 1,096 rows (Jan 2024 – Sep 2026)

| Field | Type | Description |
|---|---|---|
| `Date` | Date | Calendar date (primary key) |
| `Year` | Integer | Calendar year |
| `Month` | Integer | Month number (1–12) |
| `MonthName` | String | Greek abbreviated month name (Ιαν, Φεβ, …) |
| `Quarter` | String | Quarter label: Q1, Q2, Q3, Q4 |
| `Weekday` | Integer | Day of week (1 = Monday, 7 = Sunday) |
| `WeekdayName` | String | Greek abbreviated weekday name |
| `IsWeekend` | Boolean | 1 if Saturday or Sunday, 0 otherwise |

---

## dim_customers — 10,000 rows

| Field | Type | Description |
|---|---|---|
| `CustomerID` | Integer | Unique customer identifier (primary key) |
| `FirstName` | String | Customer first name |
| `LastName` | String | Customer last name |
| `Gender` | String | `M` (Male) or `F` (Female) |
| `Age` | Integer | Customer age at time of data extraction |
| `City` | String | City of residence |
| `Region` | String | Greek region of residence |
| `SignupDate` | Date | Date the customer registered |
| `Segment` | String | Customer value tier: `Bronze`, `Silver`, `Gold`, `Platinum` |

**Segment distribution:**

| Segment | Count | % |
|---|---|---|
| Bronze | 4,454 | 44.5% |
| Silver | 3,089 | 30.9% |
| Gold | 1,805 | 18.1% |
| Platinum | 652 | 6.5% |

---

## dim_products — 2,000 rows

| Field | Type | Description |
|---|---|---|
| `ProductID` | Integer | Unique product identifier (primary key) |
| `ProductName` | String | Product name including model suffix |
| `Category` | String | Product category (10 categories) |
| `Brand` | String | Brand name (10 brands) |
| `UnitCost` | Currency (€) | Standard cost price |
| `ListPrice` | Currency (€) | Standard list price before discount |

**Categories:** Screens · Cables · Gaming · Audio · Storage · Networking · Smart Home · Office · Accessories · Power  
**Brands:** Aegis · Helios · Orion · Atlas · Nexus · Spectra · Kronos · Nova · Ion · Aether
