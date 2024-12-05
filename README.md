<h3 align="center">Ｒｅｓｔａｕｒａｎｔ Ｏｒｄｅｒ Ａｎａｌｙｓｉｓ</h3>

<p align="center">
  <img src="https://github.com/user-attachments/assets/bb849249-3682-4095-88a2-cef169bbef22" alt="Restaurant Order Analysis Chart">
</p>

<div align="center">
  <a href="https://git.io/typing-svg">
    <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&pause=600&color=142D81&background=C6FF4100&center=true&vCenter=true&random=true&width=435&lines=A+Guide+Project+at+Maven+Analytics;using+SQL%2BTABLEAU" alt="Typing SVG">
  </a>
</div>

<div align="center">
  <a href="https://github.com/astutir" target="_blank">
    <img src="https://img.shields.io/badge/Follow-GitHub-%23181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub Badge">
  </a>
  <a href="https://www.linkedin.com/in/a-rahmawati/" target="_blank">
    <img src="https://img.shields.io/badge/Connect-LinkedIn-%230A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn Badge">
  </a>
  <a href="https://github.com/Data-Portofolio/Restaurant-Order-Analysis-" target="_blank">
    <img src="https://img.shields.io/github/stars/Data-Portofolio/Restaurant-Order-Analysis-?style=for-the-badge&logo=github&label=Stars&logoColor=white&color=yellow" alt="Star Badge">
  </a>
</div>




## Business Undestanding
### **Background**  
The Taste of the World Cafe debuted a new menu at the start of the year. So, the Data Analyst has been asked to dig into the customer data to see which menu items are doing well/not well and what the top customers seem to like best.  

### **Role**  
Data Analyst for the Taste of the World Cafe  

### **Objectives**  
- Explore the menu items table to get an idea of what's on the new menu.  
- Explore the order details table to get an idea of the data that's been collected.  
- Use both tables to understand how customers are reacting to the new menu.  

### **Data Source**  
Data Playground at Maven Analytics
(https://mavenanalytics.io/data-playground?order=date_added%2Cdesc&pageSize=10&search=resta)

## Data Understanding
### Dataset Information
Dataset Restaurant Order ini memiliki 2 table yang meliputi `menu_items` dan.

#### 1. `menu_items` : 4 features with 32 records

| **Features**      | **Distinct** | **Details**                                                                                                          |
|-------------------|--------------|----------------------------------------------------------------------------------------------------------------------|
| **`menu_item_id`**| 32           | 131 - 132                                                                               |
| **`item_name`**   | 32           | Mac & Cheese, Meat Lasagna, Orange Chicken, Spaghetti & Meatballs, Steak Burrito, Pork Ramen, Steak Tacos, dll.      |
| **`category`**    | 4            | American, Mexican, Asian, Italian                                                                                   |
| **`price`**       | 14            | $5 - $19.95|

#### 2. `orders_details` : 5 features with 12234 records

| **Features**      | **Distinct** | **Details**                                                                                                          |
|-------------------|--------------|----------------------------------------------------------------------------------------------------------------------|
| **`orders_details_id`**| 12234           | 1-12234                                                                              |
| **`order_id`**   | 5370           | 1-5370      |
| **`order_date`**    | 90            | 2023-01-01 to 2023-03-31                                                                                 |
| **`order_time`**       | 5010            | 10:50:46 to 23:05:24|
| **`item_id`**       | 32            | 101-132|

### Dataset Checking

#### 1. Check Duplicat
  
```sql
  SELECT 
    od.orders_details_id,
    od.order_id,
    od.order_date,  -- Diperbaiki dari rder_date
    od.order_time,
    od.item_id, 
    COUNT(*) AS duplicate_count
FROM orders_details od
GROUP BY od.orders_details_id, od.order_id, od.order_date, od.order_time, od.item_id
HAVING COUNT(*) > 1;
```

> [!NOTE]
> Tidak ada Duplikat.


#### 2. Check Missing Value

```sql
  SELECT 
    SUM(CASE WHEN od.orders_details_id IS NULL THEN 1 ELSE 0 END) AS orders_details_id_missing,
    SUM(CASE WHEN od.order_id IS NULL THEN 1 ELSE 0 END) AS order_id_missing,
    SUM(CASE WHEN od.order_date IS NULL THEN 1 ELSE 0 END) AS order_date_missing,
    SUM(CASE WHEN od.order_time IS NULL THEN 1 ELSE 0 END) AS order_time_missing,
    SUM(CASE WHEN od.item_id IS NULL THEN 1 ELSE 0 END) AS item_id_missing
FROM orders_details od;
```

![image](https://github.com/user-attachments/assets/a4f8d9cd-65f7-4d27-a942-84835bcf6426)

> [!NOTE]
> Terdapat missing value pada item_id sebanyak 137 rows.


## Business Insight

1. The most favored food by customers in this restaurant is **Asian category**, with around **3,470 orders**. The Italian, Mexican, and American categories have similar order counts, around ~2,700+.

   ![image](https://github.com/user-attachments/assets/f62242a0-0869-400e-b189-f5c8c3672f7f)


3. The **Top 5 Best-Selling** food items in this restaurant are Hamburger (American), Edamame (Asian), Korean Beef Bowl (Asian), Cheeseburger (American), and French Fries (American).
   
   

      ![image](https://github.com/user-attachments/assets/db3221e8-8635-4aa7-a984-78ba09d019c1)

4.  The **Top 5 Worst-Selling** food items in this restaurant are Chicken Tacos (Mexican), Potstickers (Asian), Cheese Lasagna (Italian), Steak Tacos (Mexican), and Cheese Quesadillas (Mexican).
   
      ![image](https://github.com/user-attachments/assets/d1f1a04c-a2d3-4677-ab1d-9a580aa3a2e9)
5.  The highest revenue is generated by **Korean Beef Bowl (Asian)** with a total of **$10,554.60**. Item lain dengan pendapatan tinggi memiliki perbedaan yang hanya sedikit.
   
    ![image](https://github.com/user-attachments/assets/f55948ab-cd6a-4998-a464-cf1c0bf7af29)

6.  The item with the **lowest revenue** is **Chicken Tacos**, generating **$1,469.85**, which is also the least ordered by customers.
    ![image](https://github.com/user-attachments/assets/e663bb50-f1a2-499a-9e59-34d232874bd4)

7.  Based on **the seasonality analysis**, consumer behavior can be observed. Customers at this restaurant particularly enjoy placing orders during **lunchtime**. As shown in the chart below, the peak order time occurs around **12 PM**. Additionally, the second peak happens around **5 PM**, just **before dinner**. However, customers are less inclined to order around **3 PM**.
   
    ![image](https://github.com/user-attachments/assets/00c58a50-d1bf-45cd-bbcc-06be0ccf1027)

8. From a **weekday perspective**, customers at this restaurant prefer visiting on **Mondays** and **Fridays**, with peak times during **lunch at 12 PM** and just before **dinner at 5 PM**. However, the day with the **highest customer turnout** is **Wednesday**.

    
    https://github.com/user-attachments/assets/db9d1c6d-ae42-4f46-adc8-599d76616142


9. When analyzing orders by **month**, the highest number of orders occurred in **January**, while the lowest were observed in **February**. Upon a more detailed examination by **hour**, peak times consistently occur around **12 PM** during lunch and **5 PM** just before dinner throughout all months. When analyzing by **weekdays**, the peak days show some variation; however, **Mondays** and **weekends** are generally favored by customers.
    
    https://github.com/user-attachments/assets/10a8984a-b488-41f8-8e3b-ce0e489f389b
   
  -----------------------------------------------------------------------------------------------------
   
  
  ![image](https://github.com/user-attachments/assets/d0ed1366-664e-48db-b18c-f0cda86261bc)
      
  ------------------

   ![image](https://github.com/user-attachments/assets/cc43d6f2-7b56-477e-9794-7317993d1af3)

11. Here is the chart showing the **order IDs** with the highest total number of items purchased.
    

    https://github.com/user-attachments/assets/947d7ea3-21ab-490f-b514-2669a6bbb2ec

<p align="right">(<a href="#top">back to top</a>)</p>

<p align="center">
    :copyright: 2024 | A-Rahmawati </p>
</h3>



    
