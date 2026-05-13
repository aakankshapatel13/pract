# Guide: Advanced Excel for Data Analysis (Task 10)

This guide covers the 4 essential "Advanced Excel" features for your BI practical.

---

## 1. Pivot Tables (The most important tool)
**Purpose**: To summarize large amounts of data quickly (e.g., total sales per region).
- **How to**: 
    1. Select your entire data table.
    2. Go to **Insert** -> **PivotTable**.
    3. Drag `Category` to **Rows** and `SalesAmount` to **Values**.
    4. *Result*: A summary table showing totals for each category.

---

## 2. VLOOKUP / XLOOKUP (Data Retrieval)
**Purpose**: To find data in one table based on a value in another.
- **Formula**: `=VLOOKUP(lookup_value, table_array, col_index, [range_lookup])`
- **Example**: `=VLOOKUP(A2, Products!A:B, 2, FALSE)`
    - This looks for the Product ID in cell A2 and returns the Product Name from the second column of the "Products" sheet.

---

## 3. Conditional Formatting (Visual Analysis)
**Purpose**: To highlight cells that meet certain criteria (e.g., highlighting low marks in red).
- **How to**:
    1. Select the `Marks` column.
    2. Go to **Home** -> **Conditional Formatting** -> **Highlight Cells Rules** -> **Less Than...**
    3. Enter `40` and choose "Light Red Fill".
    4. *Result*: All failing marks are instantly visible.

---

## 4. Charts & Slicers (Dynamic Visualization)
**Purpose**: To create an interactive dashboard.
- **How to**:
    1. Select your Pivot Table.
    2. Go to **Insert** -> **PivotChart** (Choose a Column or Pie chart).
    3. With the chart selected, go to **Insert** -> **Slicer**.
    4. Select `Year` or `Region`.
    5. *Result*: You now have buttons that you can click to filter your chart instantly.

---

## 5. Goal Seek (What-If Analysis)
**Purpose**: To find what input value is needed to reach a specific goal.
- **How to**:
    1. Go to **Data** -> **What-If Analysis** -> **Goal Seek**.
    2. "Set cell": Your Total Profit cell.
    3. "To value": 100,000.
    4. "By changing cell": Your Sales Quantity cell.
