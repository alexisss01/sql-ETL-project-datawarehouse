# SQL ETL Sales Data Warehouse (CRM & ERP Integration)

## Executive Summary

This project delivers an end-to-end **SQL-based ETL pipeline** that integrates CRM and ERP source data into a **business-ready sales data mart**. The solution is designed to mirror a real-world analytics environment, where fragmented operational data is transformed into reliable, standardised, and analytics-ready datasets.

The implementation follows a **Medallion Architecture (Bronze / Silver / Gold)** using SQL Server, with a **star schema** in the Gold layer to support BI reporting, ad-hoc analysis, and downstream analytics use cases.


---

## Business Context

In many organisations, sales and customer insights depend on data sourced from multiple operational systems, commonly CRM and ERP platforms. While these systems are essential for daily operations, they are typically **not designed for analytics consumption**.

Common challenges observed in such environments include:

* Duplicate customer and product records across systems
* Inconsistent identifiers and naming conventions
* Missing or invalid attributes (e.g. dates, prices, locations)
* No single source of truth for sales reporting

Without a unified data warehouse, analysts and stakeholders face significant friction producing accurate, consistent, and scalable insights.

---

## Problem Statement

The absence of a structured data warehouse makes it difficult to:

* Produce reliable sales metrics
* Perform consistent customer and product analysis
* Scale BI dashboards and ad-hoc reporting
* Maintain confidence in analytical outputs

This project addresses these issues by designing and implementing a **layered ETL pipeline** that consolidates CRM and ERP data into a centralised, analytics-ready sales data mart.

---

## High-Level Architecture

The solution is implemented using a Medallion Architecture:

* **Bronze Layer** – Raw ingestion of CRM and ERP data with no transformations
* **Silver Layer** – Cleansed and standardised datasets with data quality rules applied
* **Gold Layer** – Business-ready views optimised for analytics consumption

This layered approach improves:

* Data reliability
* Traceability and lineage
* Maintainability and extensibility

<img width="1231" height="301" alt="High Level Architecture" src="https://github.com/user-attachments/assets/cab57861-b23d-43e6-be2d-3317100faec0" />


---

## Data Flow & Lineage

Data flows from source systems (CRM and ERP) into the Bronze layer as raw tables. Each dataset is then processed through the Silver layer, where cleansing, standardisation, and enrichment logic is applied. Finally, curated Gold views are created for analytics consumption.

This design ensures:

* Clear end-to-end data lineage
* Separation of raw data from business logic
* Easier debugging and auditing

---

## Data Integration

CRM and ERP systems contain complementary information:

* **CRM**: Sales transactions, customer master data, product master data
* **ERP**: Additional customer attributes, geographic information, and product categories

These datasets are integrated in the Silver layer using consistent business keys before being modelled into fact and dimension structures in the Gold layer.

---

## Sales Data Mart (Gold Layer)

The Gold layer is modelled as a **star schema** optimised for analytics and BI reporting.

### Fact Table

* **fact_sales**

  * Order number
  * Order, shipping, and due dates
  * Quantity and price
  * Sales amount (calculated)

**Business Metric:**

* `Sales Amount = Quantity × Price`

### Dimension Tables

* **dim_customers** – Consolidated customer attributes (CRM + ERP)
* **dim_products** – Consolidated product and category attributes

This model supports performant slicing and dicing across customers, products, and time.

---

## ETL Design Decisions

Key design decisions made in this project include:

* **Batch processing** to simplify orchestration and ensure repeatable loads
* **Full load with truncate & insert** to prioritise data consistency over incremental complexity
* **Stored procedures** to encapsulate transformation logic and improve maintainability
* **Gold layer implemented as views** to support flexible BI, ad-hoc SQL, and analytics workloads

These choices reflect common trade-offs made in small-to-medium scale analytics platforms.

---

## Data Quality & Transformations

Transformations applied in the Silver layer include:

* Data cleansing (handling missing and invalid values)
* Standardisation and normalisation
* De-duplication
* Derived columns and enrichment

The goal is to ensure downstream consumers interact only with **trusted, analytics-ready data**.

---

## Skills Demonstrated

This project demonstrates practical capability across:

* SQL-based ETL development
* Data warehouse design (Medallion Architecture)
* Data cleansing and standardisation
* Star schema data modelling
* Cross-system data integration (CRM & ERP)
* Analytics-ready data delivery

---

## Potential Enhancements

Given additional time and scope, the following enhancements would further productionise the solution:

* Incremental loading and Change Data Capture (CDC)
* Automated data quality validation

---

## Summary

This project showcases a **realistic, end-to-end SQL ETL workflow** designed to bridge the gap between operational systems and analytics consumption.
