This project is a **simulation** of something very similar I did at my previous job.  
I cannot share the real code or data (confidential), but here I describe the process and made some diagrams.


## 🔄 How it works

1. **Data comes in many formats** – txt, xlsx, accdb, mdb, csv… all mixed.
2. **Python script**: I run it manually from Ubuntu terminal.  
   It cleans the data, fixes formats (uniform delimiter, remove enters inside a cell, etc.) and saves it as CSV into the right folder. This gets uploaded to GCP.
3. **Scala ETL code**: I also start this manually.  
   Before loading, it checks in PostgreSQL for existing `company_id` and `shipment_id` so we don’t have duplicates.  
   It also checks GCP file metadata to see:
   - if file is already marked as `loaded`
   - if there is a `batch` info to know where to continue
4. If everything is fine, it **transforms and loads** the data into PostgreSQL in 1000-row batches.

## 🛠️ Technologies

- Python (for data conversion)
- Scala (for ETL logic)
- Google Cloud Storage
- PostgreSQL

## 🧠 Challenges I had

- Data came in many different formats, not always nice and clean
- Needed to track which files are already loaded
- Handle schema changes without breaking the load
- Avoid duplicate records

## 🚀 How it could be better

If I had more time, I would:
- Make it **automatic** – for example with GCP Pub/Sub or Cloud Functions so when a new file comes, the pipeline starts without me
- Add better monitoring and logging
- Make a “quarantine” for bad files and flaging them differently, so that the program could only run to rerun those files.
- Have a small table in the database to track all file statuses (`raw`, `validated`, `loaded`, `failed`)

## 📷 Diagram

You can see my process here: [`diagrams/etl_flow.png`](diagrams/etl_flow.png)


## 👩 About me

I’m 24, I studied Computer Science Engineering with big data & business intelligence specialization.  
In my previous job I worked almost 3 years with ETL processes, data cleaning and sometimes frontend.  
I like solving problems with data and I’m learning German now.
