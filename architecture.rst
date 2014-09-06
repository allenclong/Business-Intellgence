Business Intelligence Architecture
==================================

This section presents the major technical components that make up an analytical architecture that I believe business users should have at least a high-level understanding of. 

Operational and Source Systems
-------------------------------

Operational and source systems, aka transactional processing systems, are the starting point fo most quantitative data in a company. 
Examples would include the policy system (APS, CLAS), the claims systems (ACE and Claim Center), billing system, and accounting or planning systems.  

ETL: Extract, Transform, Load
-----------------------------
BI often involves analyzing summary data or combining data from multiple operational systems. To facilitate this, data is extracted from the operational systems and loaded into a data warehouse. This process is referred to as *extract, transform, and load (ETL)*.  

Enterprise Information Management
---------------------------------

Enterprise informantion management (EIM, I'm getting sick of acronyms already!) consists of ETL tools, plus data modeling tools, data quality, data profiling, metadata management, and master data management.

Metadata
````````
Metadata is data about the data.  If you didn't already know what metadata is, that definition probably didn't help. Maybe an analogy will.
If the information contained in various books is the data, then the metadata would be the information about the books you would find on the card file or on Amazon: the date it was published, the number of pages, etc.  

Metadata may describe such things as

* When the data was extracted from the source system
* When the data was loaded into the data warehouse
* From which source system an item originated
* From which physical table and field in the source system was it extracted
* Transformation rules and logic
* How something was calculated--for example, *manual premium=(rate* X *payroll/100)*
* The definition, or more specifically, what the item means in a business context.

Master Data Management
```````````````````````
Master data management is the practice of defining and maintaining consistent definitions of business entities (e.g., policy, insured, or agent) and data about them across multiple IT systems.  
Master data management is what ensures the policy key or insured number stored in the warehouse is the same across all the applications.  

The Data Warehouse
------------------
A data warehouse is the collection of data extracted from the various operational systems, loaded into an operational data store or staging area, then transformed to make the data consistent and optimized for analysis and reporting.

Data Marts
``````````
A data mart can be a subset of the data coming from a central data warehouse, or a single subject area populated directly from multiple source systems (e.g., the actuarial data mart).  
Whereas the data warehouse is designed to serve the needs of the enterprise, a data mart is usually designed to serve the needs of a particular business unit, function, process, or application.  
In the past, data marts were frequently built from the operational systems, by passing the - possibly nonexistent - data warehouse.  A data mart built today is much more likely to be a subset of the data warehouse.  

Data Warehouse Tables
---------------------
Within the data warehouse, data is physically stored in individual *tables* within a relational database. 
Most data warehouses have two types of tables: (1) a *fact table* that contains keys into the dimension tables and numeric information to analyze, such as premium, paid losses, case reserves, billing amount, etc. and (2) *dimension tables* that allow analysis of measures from different perspectives, such as policy, agency, claim, claimant.   
Frequently, we will refer to the fact tables as the transaction tables. They aren't transaction tables in the typical data warehousing sense, but the rows of the fact tables tend to correspond to individual transactions.

Dimension tables are also referred to as *lookup tables* or *reference tables*. Typically, lookup tables are used for the smaller dimension tables. So the claim dimension would be less likely to be called a lookup, but the state dimension (which has simple things like the state abbreviation or core state indicator) would often be referred to as the state lookup.

To improve the performance of queries, database designers may choose to create *aggregate* or *summary tables* around the fact table, such as MONTHLY_PREMIUM. We have some of these in the Amerisure warehouse that I believe are used for the web reporting application. The summary tables are not something actuarial has ever bothered with.  



