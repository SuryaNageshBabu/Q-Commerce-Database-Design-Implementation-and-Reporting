# Delivery_X Database Design, Implementation and Reporting

![Delivery X logo](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Delivery_X%20logo.png)

A complete end to end project involving design, implementation of a database using Microsoft SQL Server for a quick delivery startup and ad-hoc reports using Power BI.

![techstack1](https://camo.githubusercontent.com/3fb5c666007b264dde797b2d7e258cae7f336848f3408cef902f04c6065cc146/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f6d7973716c2d2532333030662e7376673f7374796c653d666f722d7468652d6261646765266c6f676f3d6d7973716c266c6f676f436f6c6f723d7768697465)
![techstack2](https://camo.githubusercontent.com/ecef4c543198952452b882c5551593f6c6a7f1f4a2b304d61b0d79ce7cbf1bad/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f706f7765725f62692d4632433831313f7374796c653d666f722d7468652d6261646765266c6f676f3d706f7765726269266c6f676f436f6c6f723d626c61636b)
![techstack3](https://camo.githubusercontent.com/a0089bc3cb81a201fafb501952309feba97e5062e0bda984b24d5906670bba12/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4d6963726f736f66745f506f776572506f696e742d4237343732413f7374796c653d666f722d7468652d6261646765266c6f676f3d6d6963726f736f66742d706f776572706f696e74266c6f676f436f6c6f723d7768697465)
![techstack4](https://camo.githubusercontent.com/3accba4a9c3c86c5cd18300b2fc80c4890666662e6ea18361d16d9974a6d8590/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4d6963726f736f66745f457863656c2d3231373334363f7374796c653d666f722d7468652d6261646765266c6f676f3d6d6963726f736f66742d657863656c266c6f676f436f6c6f723d7768697465)
![techstack5](https://camo.githubusercontent.com/b0dd0c2b3bbe007ae4eef1f59c17c24ce53a334ad46bfdb80b5c841eaeccdde3/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f6d61726b646f776e2d2532333030303030302e7376673f7374796c653d666f722d7468652d6261646765266c6f676f3d6d61726b646f776e266c6f676f436f6c6f723d7768697465)


## Overview

Delivery_X is a Q-commerce grocery delivery service startup with stores across 2 different cities in Germany, it is currently experiencing significant growth and facing customer service challenges, including order processing delays, delivery issues, product quality issues and as a result there is an increase in customer complaints & refunds made on the orders. Negative reviews are rising which could harm the startup's growth.

The company's database contains extensive data on order histories, refunds, type of complaints etc. And the Head of Operations at Delivery_X wants to use this data to analyse the performance of the stores (for the period of summer 2022 between April - September) and implement solutions to improve customer satisfaction. Here below I have attached a business knowledge document containing information on all the key metrics and performance indicators used in the project. 

(**Note**: Since Database design, implementation and reporting are the primary focus of this project, there will not be any emphasis on data cleaning, however all the errors and inconsistencies were treated using SQL and Microsoft Excel prior to working with this data).

## 1. Database design

Inorder to have a stuctured approach to the design process, I have adapted *Kimball's 4 step process to design the data models*.

* **Understanding the business process & requirenments gathering**

  Delivery_X is a quick delivery service which delivers groceries in relatively smaller delivery windows in comparison to conventional delivery services. It is currently 
  offers its services in 2 different cities across Germany and both the cities have a Delivery_X store each. The company delivers groceries to its customers who place orders   through Delivery_X's mobile application.

  Considering the nature of the service and based on my previous experience I assume that the delivery, customer satisfaction and store operations to maintain product 
  quality are a few aspects which would be core to its value proposition to the customers.

  Different stakeholders involved directly and indirectly: Head of Operations, Customers, Store Operations manager, Operation associates, Delivery riders & Customer service.   
* **Declare the grain**

  Functionality requirenments: Having concluded on the key stakeholders, based on the requisites from the problem statement I beleive the grain of the data should be the 
  different type of customer complaints at the store level and their timeline

  The company's database (a flat file containing a table with all the attributes relevant to the store, customer and customer complaints) [here](www.comingsoon.com). I have 
  used this as my primary data source and I have further normalized this data to create a data model for better analysis.


  ![Delivery_X ERD diagram](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Delivery_X%20ERD.png)
  

* **Identifying the dimensions**

  After having understood the key business processes at Delivery_X and the requirenments of this project I have decided the key entities to be customer complaints, customers,
  and the store. I will further include another entity 'date' but this will be in the final part when I will be working on the ad-hoc report which I beleive gives me another 
  key dimension to analyse this problem statement.

  
  Dimension 1 : complaints
  
  In order to address the magnitude of effect of certain types of complaint on customer satisfaction, I have included complaints as a seperate dimension and further have 
  added another layer of category 'risk'.

  Dimension 2 : store

  With rapid growth it is quite common for startups like Delivery_X to have multiple stores within a city, therefore I have created a store dimension and have added 
  another category 'store_x' which refers to the name of the particular store. This would help analyse the stores not just by the city but also within a particular city 
  assuming a city might have more than one store. The source data had just the attribute of city for categorisation.

  Dimension 3 : customers

  Customers as a seperate dimension with all the customer related data.

  
* **Identifying the facts**

  The fact/transaction table in this case will be focussed on the different granular aspects of customer complaints like the type of complaints, the store for which the 
  particular complaint was raised, customer that complained, date on which the complaint was recorded, and the compensation amount paid as a refund for the particular 
  complaint to the customer. I have removed a attributes from the original table and also added a few considering the reqirenments.


## 2. Database implementation

Following the conclusions from the previous steps, database and tables are created and the data will further be migrated into these tables from the source. Here below is a schematic representaion of the Delivery_X database.

![Delivery_X database schema](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Delivery_X%20database%20schema.png)

The tables are further normalized into a Star schema. Here above I have aligned the tables according to the *Coolie layout methodology* in which the fact tables(tables containing the transactional data) are placed at the bottom and the lookup tables(dimension tables) are placed on the top for better visual cue, however the tables still follow Star schema.

* **Creating a database Delivery_X and the tables on the SQL Server RDBMS**

![Creating a database Delivery_X and the tables](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Creating%20database%20and%20tables.png)

* **Migrating data into the newly created tables**

![Migrating the data](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Migrating%20the%20data%20into%20the%20tables.png)

![Migrating the data](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Migrating%20the%20data%20into%20the%20tables_02.png)

* **Enforcing data consistency with Attribute, Key & Referential constraints**

![Enforcing data consistency](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Enforcing%20data%20consistency_01.png)

![Enforcing data consistency](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Enforcing%20data%20consistency_02.png)

![Enforcing data consistency](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Enforcing%20data%20consistency_03.png)

* **Defining the fact table, dropping the columns that are not required**

![Drop unn columns](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Drop%20unn%20columns.png)

![Defining the fact table](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Defining%20the%20fact%20table.png)


## 3. Exploratory analysis & Asking the right questions

Considering the pain points and the inputs provided by Delivery_X's head of operations in terms of the requirenments, a preliminary exploratory analysis will be performed addressing aspects aligned with the customer complaints. And the finding will further be reported alongside other key metrics on the dashboard.

***Which type of complaint has been raised by the customers more often and which has costed the company more ?***

  ![Query 1](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Query%201.png)

This is a key insight which should also be included in the dashboard. It gives a clear picture on the most recurring type of complaint, if it is related to product quality which in turn might require changes in SOPs to improve store operations or if it related to delivery, necessary measures can be put in place to address it. 

***Providing insights on how swiftly the high priority complaints were resolved might lead to implemention of measures which can improve the overall customer satisfaction***.

![Query 3](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Query%203.png)

***Compensated amount split by the category of complaints for all stores in Heidelberg***

![Query 4](https://github.com/SuryaNageshBabu/Delivery_X-Database-Design-Implementation-and-Reporting/blob/main/Query%204.png)

This gives a gives a better insight on the most prominant category of complaint for all the stores in Heidelberg. It is a key insight to analyse specifically for this problem statement because there can be a lot of factors which could be responsible for a certain type of complaint to be recurring in a particular store. For Ex: In this case the city of Heidelberg has only one store 'Hei_X' and from the results above it is observed that Delayed orders are amongst the two prominent type of complaints for this store, this can be because of the local of the store Hei_X itself which is not probably located centrally to make deliveries out of the store easier or it could also be due to an issue with the delivery riders working at this store. This opens up a whole new dimension for analysing the scenario further.

***High priority complaints resolved in time vs those not resolved in time for the stores in Darmstadt***

![Query 5](https://github.com/SuryaNageshBabu/Q-Commerce-Database-Design-Implementation-and-Reporting/blob/main/Query%205.png)

Here, we can infer that less than 50% of high priority customer complaints were resolved in time for the stores in Darmstadt. This can be a key insight to the head of operations which can further be flagged to the customer service team that is in charge for the particular store 'Dar_X' in Darmstadt.

**(Note: Not all the queries used for exploring the data are presented here, however I have included detailed list of queries used for exploration as a part of the SQL project series for reference [here](www.comingsoon.com))**

Based on the findings above and based on the requisites of the problem statement, I have included other metrics and indicators in the Power BI dashboard (presented below).


## 4. Reporting/Ad-hoc dashboard design using Power BI

Based on all the findings from the exploratory analysis and also based on the business knowledge I had honed through my previous experience in this sector, I have drafted and designed a dashboard addressing the key granular aspects of customer complaints. I beleive this will provide the end user, head of operations of Delivery_X in this case
to get a detailed insight into the performance of both the stores. 

![Delivery_X Dashboard](https://github.com/SuryaNageshBabu/Q-Commerce-Database-Design-Implementation-and-Reporting/blob/main/Delivery_X%20Performance%20Dahboard%20.gif)

This dashboard was designed to derive numerous different metrics based on the customer complaints. It gives a detailed overview on performance of the stores also on a store level for a few key metrics. Visuals and Metrics presented in the dashboard are based on conclusions derived from the problem statement & also considering the target user that will be using the dashboard, in this case it is the head of operations of Delivery_X. 

A detailed know-how on all the metrics and performace indicators in the dashboard is included in the [business knowledge document](www.comingsoon.com). 

Detailed description of all the different aspects of transformations & analysis performed on Power BI using Power query & the DAX functions used are included here [Q-Commerce-service-Delivery_X-performance-dashboard](https://github.com/SuryaNageshBabu/Q-Commerce-service-Delivery_X-performance-dashboard/blob/main/README.md)


## Get in touch

Feel free to share your feedback. You can reachout to me through [Linkedin](https://www.linkedin.com/in/suryanageshbabu/)
