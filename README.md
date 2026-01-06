📊 DATA WAREHOUSE ARCHITECTURE  
TOOLS -SQL SERVER.

🎯 Project Overview
This repository documents the architecture and pipeline logic for processing raw stock and inventory data from local CSV files into a structured, highly refined format suitable for stakeholder consumption and business intelligence. Our multi-layered approach ensures data integrity, full traceability, and adherence to data wrangling ethics through clearly defined transformation stages.

🏛️ Data Architecture Flow
<img width="960" height="507" alt="Screenshot_1" src="https://github.com/user-attachments/assets/0dd81bfb-2d7c-4587-9d77-919a3b98d5b4" />

Our system utilizes a three-tiered structure (Bronze, Silver, Gold) following a Lakehouse design pattern, ensuring raw data immutability and high-quality consumption-ready data.

1. Source Layer (External System)
Attribute	Detail
Data Location-	Local Directory (Host Machine),
File Format	-CSV Files,
Extraction- Technique	File Parsing,
Extraction- Model	Pull,
Extraction Method	-Full (Always extract the complete file),
Scope of Concern	-Extract Only (No manipulation or cleaning)

2. Bronze Layer (Raw Staging)
This layer is the immutable staging area. Data is loaded exactly as it appears in the Source, preserving raw lineage. This is essential for auditing and ethical data handling.

Attribute	Detail
Scope of Concern-	Extract & Load Only,
Extraction Technique-	File Parsing,
Load Processing	-Batch,
Load Method	-Truncate and Insert,
Object Type-	Table,
Transformations	-None (No cleaning, standardization, or derived columns)

3. Silver Layer (Cleansed & Conformed)
The Silver layer is where data quality rules are enforced. Data is cleaned, standardized, and enriched here, making it reliable for internal processes.

Attribute	Detail
Scope of Concern- Transform & Load Only
Load Processing	-Batch
Load Method	-Truncate and Upsert
Object Type-	Table
Transformations-	Data Cleaning, Data Standardization, Data Normalization, Derived Columns, Data Enrichment

4. Gold Layer (Business Consumption)
The Gold layer is optimized for fast reporting, analytics, and business consumption. Data is restructured into dimensional models that align with business logic.

Attribute	Detail
Scope of Concern- Transform & Load Only,
Load Processing-	Batch,
Load Method-	Truncate and Upsert,
Object Type	-Table,
Manipulations	-Aggregation, Star Schema Modeling, Business Logic Implementation

🔖 Data Handling and Naming Conventions
Adhering to strict naming conventions ensures consistency, code readability, and seamless scaling across all environments.

1. Naming Standard
Format: All names (databases, schemas, tables, columns) must be in lowercase with snake_case (e.g., product_inventory).

Technical Prefix: All technical columns created during the ETL process must start with the project prefix dwh_ (e.g., dwh_load_date).

2. Naming Hierarchy (Tables & Schemas)

<img width="508" height="167" alt="naming convention" src="https://github.com/user-attachments/assets/fb713399-d7fe-48e7-8b54-5cd2609ce81f" />
The naming hierarchy is crucial for tracing data lineage back to the source.

Source_Category_Sub-Category_Sub-Sub-Category
Example: source_wigs_frenchcurls_lush

3. Key Conventions

Primary/Foreign Keys: All surrogate keys, foreign keys, and unique identifiers must end with the suffix _key.
<img width="1094" height="556" alt="data_flow" src="https://github.com/user-attachments/assets/42d9be13-88ef-4610-8a03-0c772758d9fc" />

Source Key Example: product_sku_key

Database Key Example: product_inventory_key

🚦 Compliance and Ethical Data Handling
The multi-layered architecture enforces ethical data handling principles:

Immutability (Bronze): The Bronze layer ensures that the raw source file is never modified, providing a definitive audit trail for compliance and data lineage.

Traceability (Silver): The dwh_ technical columns track processing timestamps and source references, allowing a full backtrack from any Gold-layer report to the original Source file.

Transformation Control (Silver/Gold): By restricting cleaning and transformation to the Silver and Gold layers, we ensure that the logic is centralized, documented, and peer-reviewed, mitigating the risk of introducing bias or errors during the wrangling process.


