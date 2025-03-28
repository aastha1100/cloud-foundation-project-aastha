# data-analyst-aastha 

<a href="https://github.com/aastha1100/data-analyst-aastha/blob/main/AWS CF Completion Badge.png" target="_blank" rel="noopener noreferrer">📸 View AWS Cloud Foundation Completion Badge</a>

| Analysis Name          | Short Description                                      | Link                   |  
|------------------------|-------------------------------------------------------|------------------------|  
| 📊 Descriptive Analysis   | Cloud-based DAP for water system analysis             | [View](#descriptive-analysis) |  
| 🔍 Diagnostic Analysis    | Root cause analysis of pipe failures                  | [View](#diagnostic-analysis)  |  
| 🧹 Data Wrangling         | Cleaning and preparing data for analytics             | [View](#data-wrangling)       |
| ✅ Data Quality Control   | Security validation                                   | [View](#data-quality-control)       |  


---

## Descriptive Analysis  
**Project Title:** Data Analytic Platform (DAP) Implementation for Vancouver Water Distribution System  
**Objective:** Design and implement a cloud-based DAP to analyze water distribution pipe age and material composition enabling proactive maintenance prioritization.  

**Background:**  
The City of Vancouver’s Water Distribution Department manages aging infrastructure including 60,000+ water mains. Frequent pipe failures for instance leaks bursts necessitated a data-driven approach to identify high-risk pipes. The DAP aimed to:  
- Calculate pipe age from installation dates.  
- Correlate material types with failure risks.  
- Provide actionable insights for resource allocation.  

**Dataset:**  
- **Water Distribution Mains Dataset**:  
  - Fields: `INSTALLATION_DATE` `MATERIAL_INFO` `PIPE_DIAMETER`.  
  - `INSTALLATION_DATE`: Pipe installation date in DD/MM/YYYY format.  
  - `MATERIAL_INFO`: Material type used for instance cast iron copper ductile iron.  
  - Size: 60,000+ records.  
  - Accuracy: Survey-grade spatial data.  
  - Scope: Excludes residential/commercial connections.  

<img width="769" alt="Screenshot 2025-03-27 at 10 59 44 AM" src="https://github.com/user-attachments/assets/fe80b745-3e06-45b3-853f-f6697c0f13ed" />  

**Methodology:**  
1. **Data Collection & Preparation**:  
   - Load the dataset to python to do initial cleaning and calculate age of pipe. New column added `Pipe_Age`.  
   - Segregate the data using pandas to three datasets `installation_dates` `material_info` `pipe_diameter`.  
   - **Ingestion**: Uploaded raw CSV files (`installation_dates` `material_info` `pipe_diameter`) to dedicated **Amazon S3 buckets**.

<img width="819" alt="Screenshot 2025-03-27 at 8 19 23 PM" src="https://github.com/user-attachments/assets/f1e0d463-f1d4-42a0-a457-c87e15c7cc69" />
  
   - **Segregation**: Organized data by logical categories (e.g. installation dates) for schema-on-read flexibility.  
3. **Descriptive Statistics**:  
   - **Age Calculation**: Used **AWS Athena** SQL queries to compute average pipe age (45 years) and identify 12,083 pipes >70 years old.  
   - **Material Analysis**: Grouped data by `MATERIAL_INFO`; 11,947 aging cast iron pipes were flagged as high-risk.  
4. **Data Visualization**:  
   - **ETL Workflows**: Joined tables in **AWS Glue Visual ETL** to create a unified dataset (`Final-output`).  
   - **Risk Mapping**: Generated summaries (e.g. material-to-age correlations) for prioritization.  

**Tools & Technologies**:  
- **AWS S3** (storage versioning encryption).  
- **AWS Glue** (cataloging ETL jobs Visual ETL joins).  
- **AWS Athena** (SQL queries for material prevalence).  
- **AWS Glue Databrew** (data profiling/cleaning).  
- **AWS Elastic Beanstalk/EC2** (scalable processing).  
- **AWS CloudWatch/CloudTrail** (monitoring/auditing).

**Deliverables**:  
1. **Risk Assessment Report**: Highlighted 11,947 high-risk cast iron pipes needing replacement.  
2. **Cleaned Dataset**: 20,000 records post-cleaning.
   
<img width="580" alt="Screenshot 2025-03-27 at 8 21 12 PM" src="https://github.com/user-attachments/assets/5bba2eec-567d-458f-a7a9-75cfbea37ced" />


4. **Visual Workflows**: ETL pipeline screenshot.

<img width="1142" alt="Screenshot 2025-03-27 at 8 22 33 PM" src="https://github.com/user-attachments/assets/c249fab0-932f-4eac-83d8-c6d276611da9" />


6. **Cost Analysis**: Platform operational cost: **USD 1.32 annually**.
   
<img width="492" alt="Screenshot 2025-03-27 at 8 23 40 PM" src="https://github.com/user-attachments/assets/31660342-b316-4ec6-93c1-b6fa12abc057" />


**Timeline**:  
- **4 weeks** (Data ingestion → Cleaning → Analysis → Reporting).  

---

## Diagnostic Analysis  
**Project Title:** Root Cause Analysis of Cast Iron Pipe Failures  
**Objective:** Diagnose why cast iron pipes contribute disproportionately to failures.  

**Methodology**:  
1. **Correlation Analysis**:  
   - Linked pipe age (`INSTALLATION_DATE`) and material degradation using **AWS Glue ETL jobs**.  
   - Identified 98.8% of pipes >70 years old as cast iron.  
2. **Root Cause Validation**:  
   - Cross-referenced findings with corrosion studies (Rajani & Kleiner,2001).  
   - Validated via **AWS Athena** queries.  

**Tools & Technologies**:  
- **AWS Glue** (material-age mapping).  
- **AWS Athena** (diagnostic SQL queries).  

**Deliverables**:  
- Technical report linking cast iron corrosion to failure rates.  
- Athena query outputs.

---

## Data Wrangling  
**Project Title:** Pipeline Engineering for Water Infrastructure Data  
**Objective:** Clean, transform, and catalog pipe data for analytics.  

**Methodology**:  
1. **Data Profiling**:  
   - Used **AWS Glue Databrew** to detect missing values (e.g. null `INSTALLATION_DATE`).  
2. **Data Cleaning**:  
   - Removed 40,000+ outliers/null records. Standardized date formats.  
3. **Transformation**:  
   - Cataloged data into **AWS Glue** tables (`van_wat_dist_trf_system`).  

**Deliverables**:  
- Cleaned dataset (20,000 records) in S3.  
- Glue DataBrew job profiles.  

## Data Quality Control
**Project Title:** Ensuring Data Integrity for Water Analytics  
**Objective:** Implement security, validation, and governance measures.  

**Methodology**:  
1. **Validation**:  
   - Applied **AWS Glue Data Quality** rules to flag incomplete `MATERIAL_INFO`.  
2. **Security**:  
   - Enabled S3 server-side encryption (SSE) and versioning.

<img width="620" alt="Screenshot 2025-03-27 at 8 29 51 PM" src="https://github.com/user-attachments/assets/4e938fb8-be1e-4008-84fd-bfe2c2261e2e" />

3. **User Roles**:
   - Defining IAM user roles through **Key Management Service (KMS)**.

<img width="622" alt="Screenshot 2025-03-27 at 8 31 23 PM" src="https://github.com/user-attachments/assets/08be184f-3b14-4822-bd13-13def7f3ea60" />


4. **Monitoring**:  
   - Tracked storage metrics with **AWS CloudWatch** (alerts for 3M+ byte thresholds).  

**Deliverables**:  
- Encrypted S3 buckets with versioning.  
- CloudWatch dashboard.

<img width="626" alt="Screenshot 2025-03-27 at 8 32 46 PM" src="https://github.com/user-attachments/assets/b3324ee2-23ff-4268-8315-b26a89f70b88" />

- Key management service.  

### **Final Output**  
- It identified 12,083 pipes over 70 years old. Out of these, 11,947 were cast iron.
- Cast iron’s susceptibility to corrosion is well-documented (Rajani & Kleiner, 2001). This poses a significant risk to Vancouver water system reliability.
- In summary, this project provides a robust framework for infrastructure management. It combines cloud analytics with engineering insights. It addresses immediate risks while paving the way for future innovations.



<img width="788" alt="Screenshot 2025-03-26 at 11 13 37 PM" src="https://github.com/user-attachments/assets/a327b89f-57b6-4a9b-a1cc-8dfc98d11313" />

</div>
