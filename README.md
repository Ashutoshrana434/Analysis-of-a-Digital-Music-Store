
# Unlocking Business Insights: A SQL-Powered Analysis of a Digital Music Store

### **1. Title**

Music Store Sales Analysis
##Database Schema
<img width="984" height="886" alt="Music_Database Schema" src="https://github.com/user-attachments/assets/f45c642f-49cc-416d-bc1e-3b13a221bfe2" />
### **2. Executive Summary**

This project involves a comprehensive analysis of a digital music store's database using SQL to extract actionable business insights. By querying data across multiple tables, including customer information, invoices, tracks, and artists, this analysis answers critical questions about sales performance, customer behavior, and genre popularity across different countries. Key findings include identifying the most profitable cities for promotional events, pinpointing the highest-value customers for loyalty programs, determining the most popular music genres in various regions for targeted marketing, and recognizing top-selling artists. The project showcases the power of SQL in transforming raw data into strategic business intelligence.

### **3. Business Problem**

The management of the digital music store aims to make data-driven decisions to boost sales, enhance customer engagement, and optimize marketing spend. To achieve this, they need to answer several key business questions:

  * Which countries and cities generate the most revenue?
  * Who are our most valuable customers?
  * Which artists and music genres are the most popular among our customers?
  * How does music taste vary by geographical location?
  * Where should we focus our next marketing campaign or host a promotional music festival?
  * Which artists should we invite for a promotional collaboration?

This SQL analysis directly addresses these questions by delving into the sales and customer data.

### **4. Methodology**

The analysis was conducted entirely using SQL, leveraging a relational database schema that connects customers, invoices, tracks, albums, artists, and genres. The approach involved writing a series of queries that ranged from simple to complex to uncover patterns and trends.

The core methodologies included:

  * **Data Aggregation:** Using functions like `COUNT()`, `SUM()`, and `AVG()` with `GROUP BY` clauses to summarize data. This was used to find the total number of invoices per country, the total sales per city, and the number of songs per artist.
    ```sql
    -- Example: Finding the city with the highest total sales
    SELECT billing_city, SUM(total) AS total_invoices
    FROM invoice
    GROUP BY billing_city
    ORDER BY total_invoices DESC;
    ```
  * **Table Joins:** Combining multiple tables (`customer`, `invoice`, `invoice_line`, `track`, `album`, `artist`, `genre`) using `JOIN` clauses to create comprehensive views for analysis. This was fundamental for nearly every query, such as linking customers to their favorite genres.
  * **Subqueries and Common Table Expressions (CTEs):** Employing multi-step logic to answer complex questions. For instance, a subquery was used to find all tracks with a length longer than the overall average, and a CTE was used to first identify the best-selling artist before calculating how much each customer spent on them.
    ```sql
    -- Example: Using a CTE to find the most popular genre per country
    WITH popular_genre AS (
        SELECT COUNT(il.quantity) AS purchases, c.country, g.name, g.genre_id,
        ROW_NUMBER() OVER(PARTITION BY c.country ORDER BY COUNT(il.quantity) DESC) AS RowNo
        FROM invoice_line il
        JOIN invoice i ON i.invoice_id = il.invoice_id
        -- ... additional joins
    )
    SELECT * FROM popular_genre WHERE RowNo <= 1;
    ```
  * **Window Functions:** Using advanced functions like `ROW_NUMBER()` with `PARTITION BY` to rank data within specific categories. This was crucial for determining the top-spending customer and the most popular genre *for each country*.

### **5. Skills**

  * **SQL:** Proficient in writing simple to advanced queries.
  * **Data Analysis:** Interpreting business questions and translating them into data queries.
  * **Relational Database Management:** Understanding and navigating database schemas, including primary and foreign key relationships.
  * **Advanced SQL Techniques:**
      * Common Table Expressions (CTEs)
      * Window Functions (`ROW_NUMBER`, `PARTITION BY`)
      * Subqueries
      * Complex Joins
  * **Business Intelligence:** Extracting actionable insights from data to support strategic decision-making.
