# Real-time-youtube-insights
# 📊 From API to Dashboard — YouTube Analytics Project

## Overview 
This is an end-to-end **data analytics project** I built using real YouTube data.  
It covers the complete workflow — from **data extraction via API** to **data visualization in Power BI**.

---

## 🎯 Project Goal

To analyze the performance of a YouTube channel using live data from the **YouTube Data API v3**.  
For this project, I used **Alex The Analyst’s YouTube channel**, one of my biggest inspirations in data analytics.

---

## 🧠 Workflow Overview

### 1️⃣ Data Collection — YouTube Data API (Google Cloud)
- Created a project in **Google Cloud Console** and enabled the **YouTube Data API v3**.
- Generated an **API key** and used the `googleapiclient.discovery` module to connect.
- Extracted real-time video data including:
  - Video Title  
  - Views  
  - Likes  
  - Comments  
  - Duration  
  - Publish Date  

---
## Dashborad

<img width="1012" height="569" alt="alextheanalyst" src="https://github.com/user-attachments/assets/44cf4cea-1192-4ed9-a25c-7bbccb9db2ee" />
<img width="1003" height="567" alt="alextheanalyst 1" src="https://github.com/user-attachments/assets/687d52ce-6759-495d-8e5b-5ab885db6a71" />

### 2️⃣ Data Processing — Python & Pandas
- Cleaned and structured the raw JSON responses into tabular form.
- Used **pandas** for data wrangling and saved the result as a CSV file.
- Key libraries used:
  ```python

----


## 💻 Python Script (Main Workflow)

Below is the Python code I wrote to collect, clean, and export YouTube channel data.







