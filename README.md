🌐 RAI Framework Pilot: ETL Structure

Welcome!
This repository supports the Reflective Agile Intelligence (RAI) Framework pilot project, aligned with UN SDG 4: Quality Education.
Our goal is to build a robust, transparent, and ethically aligned ETL system that empowers reflective learning environments through digital transformation and continuous feedback loops.

🧱 Layered ETL Staging Model

A structured Medallion-inspired architecture that organizes data into progressive stages, ensuring traceability, validation, and auditability across the ETL lifecycle.


| **Zone**                | **Function**                                           | **Industry Equivalent**    |
| ----------------------- | ------------------------------------------------------ | -------------------------- |
| **1. Original.File.***  | Raw, untouched data                                    | 🟤 **Bronze Layer**        |
| **2. Prepared.File.***  | Cleaned and preprocessed datasets                      | ⚪ **Silver Layer**         |
| **3. Load.File.***      | Data ready for ingestion into databases or dashboards  | 🟡 **Gold Layer**          |
| **4. Anomalies.Data.*** | Detected issues, rejected records, and validation logs | 🔴 **Error/Rejected Zone** |



“The project applies a Layered ETL Staging Model, inspired by the Medallion Architecture, using explicitly named folders to reflect each phase of data refinement—enabling traceability, debugging, and governance across the RAI data ecosystem.”


| **RAI Domain**   | **Process**                                  | **PCF Code** | **Description**                                                   |
| ---------------- | -------------------------------------------- | ------------ | ----------------------------------------------------------------- |
| **Reflection**   | Define learning objectives & engagement KPIs | R1.1         | Identify how monthly events contribute to organizational learning |
| **Agility**      | Automate data collection & ETL pipelines     | A1.3         | Streamline ingestion and transformation using Power BI / SSIS     |
| **Intelligence** | Validate and harmonize participation data    | I1.2         | Match attendance and registration using fuzzy logic               |
| **Governance**   | Maintain participant privacy & consent       | G1.4         | Ensure ethical compliance and privacy in all records              |
| **Impact**       | Measure learning outcomes                    | IM1.3        | Track engagement trends and knowledge growth across sessions      |




⚙️ Tools & Technologies

SQL Server / SSIS – Data modeling & ETL pipelines

Power BI / DAX – Visualization, dashboards, and KPI tracking

Python / Pandas – Advanced data transformation and validation

RAI Framework – Reflective Agile Intelligence methodology

GitHub – Version control, collaboration, and documentation

🔁 Continuous Reflection Loop

The RAI Data Warehouse supports iterative learning and continuous improvement through reflection cycles:

Compare planned vs. actual participation across events.

Identify data quality gaps and process inefficiencies.

Document findings in RAI-PCF reflective logs.

Adjust communication and engagement strategies based on evidence.

Each feedback cycle strengthens agility, trust, and intelligence within the learning ecosystem.

📈 Expected Outcomes

A fully functional RAI-aligned Data Warehouse built using the Medallion Architecture.

Enhanced data transparency, integrity, and traceability across reflective learning environments.

Dynamic Power BI dashboards supporting reflective, agile, and intelligent decision-making.

Scalable ETL blueprint adaptable to education, governance, and quality-management domains.

🧭 Ethical Governance & UN Alignment

Aligned with UN SDG 4 (Quality Education) and UN SDG 16 (Peace, Justice & Strong Institutions).

Respects data privacy, inclusivity, and accountability principles.

Encourages digital literacy and transparent learning analytics as part of sustainable transformation.

Pilot Case Study Step by Step :
🎓 Project 1: RAI RU ETL – Unified Table Model

Welcome everyone to the first project in this course!
This introductory project will help you understand the end-to-end process of organizing, cleaning, and preparing a unified dataset for loading into a relational database.
We’ll use real data related to the Reflective Agile Intelligence (RAI) RU Project, focusing on integrating registration, attendance, photos, and membership records into one structured table.

🧱 Step 1. Organize Your ETL Workspace

Before doing any cleaning or transformation, create four folders to follow the RAI ETL model:

Folder	Purpose	Notes
1.Original.File	Store raw files exactly as received.	Never modify these.
2.Prepared.File	Perform cleaning, merging, and validation.	Work only on copies.
3.Load.File	Final version ready for database ingestion.	Must be verified and clean.
4.Anomalies.Data	Store rejected or problematic rows.	Document the issue and cause.

💡 Tip: Always protect the 1.Original.File copy. If something breaks, you can easily restart.

🗃️ Step 2. Understand Your Unified Dataset

The dataset you are working with is a single merged table that consolidates multiple data sources.

🧩 Table: RAI_RU_Integrated.csv

Each row now represents one participant’s full event journey—from registration to attendance to certification status.

Category	Columns	Description
Registration Data	registration_id, full_name, email, event_code, registration_timestamp, source_file	Registration records from event forms
Attendance Data	attendance_id, display_name, join_time, leave_time, platform, Section, Member, Member Type, WebexAttendance.Report	Attendance logs across Webex, Zoom, Teams, or Google Meet
Photo Metadata	photo_id, file_path, attendee_label, consent_flag, photo_timestamp, load_date, source_file	Session photo and consent records
Membership Data	member_id, member_name, member_type, certification_status, member_email, source_file	Member profiles and certification progress
🧹 Step 3. Clean the Data (in 2.Prepared.File)

Now, open the unified dataset in Excel or Power BI (or Python/Pandas if you prefer scripting).

🔍 3.1 Verify Column Names and Formats

Check that headers match exactly the expected schema above.

Confirm all date/time fields are recognized as datetime types.

Standardize platform entries → only Webex, Zoom, Teams, Google Meet.

Normalize case:

email, member_email → lowercase

full_name, display_name, member_name → proper title case

🧩 3.2 Key Consistency

Each registration_id, attendance_id, member_id, photo_id must be unique.

Check for duplicated rows or missing event codes (event_code).

Where event_code mismatches across subcomponents, flag them to 4.Anomalies.Data/anomalies_event_mismatch.csv.

🧮 3.3 Derived Columns

Attendance Duration:
attendance_minutes = DATEDIFF(minute, join_time, leave_time)

Consent Category:
If consent_flag = 0, mask the file_path value (replace with “null”).

🔒 3.4 Privacy and Data Ethics

Do not remove non-consented rows; simply mask sensitive fields.

Ensure photo paths are not publicly exposed unless consent is confirmed.

Maintain compliance with RAI Governance Code G1.4.

🧰 Step 4. Create the Load Table (in 3.Load.File)

Once cleaned, save the file as:

RAI_RU_Load_YYYYMMDD.csv

and prepare to load into SQL Server, Power BI, or your analytics tool.

Recommended SQL Table Schema
CREATE TABLE dbo.RAI_RU_Participants (
  registration_id INT,
  full_name NVARCHAR(200),
  email NVARCHAR(200),
  event_code VARCHAR(50),
  registration_timestamp DATETIME2,
  attendance_id INT,
  display_name NVARCHAR(200),
  join_time DATETIME2,
  leave_time DATETIME2,
  platform VARCHAR(50),
  section NVARCHAR(100),
  member NVARCHAR(100),
  member_type VARCHAR(100),
  webex_attendance_report NVARCHAR(100),
  photo_id INT,
  file_path NVARCHAR(400),
  attendee_label NVARCHAR(100),
  consent_flag BIT,
  photo_timestamp DATETIME2,
  load_date DATETIME2,
  member_id INT,
  member_name NVARCHAR(200),
  certification_status VARCHAR(100),
  member_email NVARCHAR(200),
  attendance_minutes INT
);

🚨 Step 5. Handle Anomalies (in 4.Anomalies.Data)

When validation fails, separate those records for review:

File Name	Purpose
anomalies_event_mismatch.csv	Event codes don’t align across sources
anomalies_duplicates.csv	Duplicate participant or registration IDs
anomalies_time_issues.csv	Negative or unrealistic attendance durations
anomalies_consent.csv	Missing or revoked consent details
🔁 Step 6. Save and Reflect

Once all stages are complete:

Keep the original file safe.

Keep a clean prepared version as your ETL input.

Keep load-ready and anomaly files properly dated.

Document your data cleaning observations in a short reflective log:

What patterns did you find?

How did you resolve inconsistencies?

What could be automated in the next cycle?

🌱 Outcome

By the end of this project, you’ll have:

✅ A single, unified table ready for SQL or Power BI.
✅ A transparent ETL structure aligned with RAI Medallion Logic (Bronze → Silver → Gold → Anomalies).
✅ Documented data governance, consent, and reflection records.

📬 Authors

Narges Aminimoghaddam & Jafar Abolfathi
Creators of the Reflective Agile Intelligence (RAI) Framework
🌐 https://raiframework.org
 (Website's Update Coming Soon)
