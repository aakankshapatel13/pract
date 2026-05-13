# Power BI Tutorial: Data Import & ETL (Task 7, 8, 9)

This tutorial covers how to Extract, Transform, and Load (ETL) data from multiple sources into Power BI.

---

## Part 1: Importing from Excel (Unstructured/File Source)
1.  **Open Power BI Desktop**.
2.  On the **Home** ribbon, click the **Get Data** icon.
3.  Select **Excel workbook** from the dropdown.
4.  **Browse**: Find your file (e.g., `sales_data.xlsx`) and click **Open**.
5.  **Navigator Pane**: 
    - A list of sheets will appear. Check the box for the sheet you want (e.g., `Sheet1`).
    - You will see a **Preview** of the data on the right.
6.  **Decision**:
    - Click **Load** if the data is perfect.
    - Click **Transform Data** if you need to clean it (e.g., remove empty rows).

---

## Part 2: Importing from SQL Server (Database Source)
1.  Click **Get Data** -> **SQL Server**.
2.  **Server Settings**:
    - **Server**: Type `localhost` or your server's IP address.
    - **Database**: (Optional) Type the name of the database.
    - **Data Connectivity Mode**: 
        - Choose **Import** (standard for most practicals).
3.  **Authentication**:
    - If prompted, choose **Windows Authentication** (Current User) or **Database** (Enter Username/Password).
4.  **Navigator**: Select the tables (e.g., `FactSales`, `DimProduct`) and click **Load**.

---

## Part 3: Importing from Oracle Database
1.  Click **Get Data** -> **More...** -> **Database** -> **Oracle Database**.
2.  **Server**: Enter the Oracle Net Service Name or the connection string (e.g., `localhost:1521/xe`).
3.  **Requirement**: Mention to the examiner: *"To connect to Oracle, the Oracle Data Access Components (ODAC) must be installed on this machine."*

---

## Part 4: Data Transformation (Power Query Editor)
Once you click **Transform Data**, the Power Query window opens. This is where you "Clean" the data:
1.  **Remove Errors/Nulls**: Right-click a column header -> **Remove Errors** or **Remove Empty**.
2.  **Use First Row as Headers**: If your Excel data starts on the second row, click **Use First Row as Headers** on the Home tab.
3.  **Change Data Types**: Click the icon (ABC or 123) next to the column name to change a text column to a number or date.
4.  **Merge Queries**: If you want to join your SQL data with Excel data, click **Merge Queries** and select the common column (e.g., `ProductID`).

---

## Part 5: Loading into the Targeted System
In Power BI, the "Targeted System" is the **In-Memory Data Model**.
1.  In the Power Query Editor, click **Close & Apply** (Top-left corner).
2.  **Wait**: Power BI will now create a connection, pull the rows, and store them in its internal memory.
3.  **Verify**: Look at the **Fields** pane on the far right. You should see all your tables and columns listed there.

---

## Part 6: Creating the Visualization (Task 8 & 10)
1.  Go to the **Report View** (Canvas icon on the left).
2.  Drag a **Column Chart** onto the canvas.
3.  Drag `Category` from your Excel table to the **Axis**.
4.  Drag `SalesAmount` from your SQL table to the **Values**.
5.  Power BI will automatically combine the data from both sources and show you the chart!
