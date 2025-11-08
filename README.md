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


# -------------------------------
# 📊 YouTube Data Scraper 
# -------------------------------
# This script connects to YouTube’s API using your API key,
# fetches all videos from a channel (like Figma’s),
# and saves their details (title, views, likes, etc.) into a CSV file.

from googleapiclient.discovery import build
import pandas as pd

# -------------------------------
# 🔑 Step 1: Enter your API Key
# -------------------------------
api_key = "AIzaSyCo_S1DXWFyg8UTa2kRbIW6oimfgrFMlho"  # 👈 Paste your YouTube API key inside the quotes

# -------------------------------
# 📺 Step 2: Enter the Channel ID
# -------------------------------
# Example: Figma’s channel ID
channel_id = "UCAB7sJntFKBTAkzE3n_HGzg"

# -------------------------------
# 🧰 Step 3: Create YouTube API client
# -------------------------------
youtube = build('youtube', 'v3', developerKey=api_key)

# -------------------------------
# 🔍 Step 4: Get basic channel info
# -------------------------------
channel_request = youtube.channels().list(
    part='snippet,statistics,contentDetails',
    id=channel_id
)
channel_response = channel_request.execute()

channel_title = channel_response['items'][0]['snippet']['title']
subscribers = channel_response['items'][0]['statistics'].get('subscriberCount', 0)
views = channel_response['items'][0]['statistics'].get('viewCount', 0)
video_count = channel_response['items'][0]['statistics'].get('videoCount', 0)

print(f"📺 Channel: {channel_title}")
print(f"👥 Subscribers: {subscribers}")
print(f"👀 Total Views: {views}")
print(f"🎬 Total Videos: {video_count}")

# -------------------------------
# 🎞 Step 5: Get all videos from the channel
# -------------------------------
video_ids = []
next_page_token = None

while True:
    request = youtube.search().list(
        part='id',
        channelId=channel_id,
        maxResults=50,
        order='date',
        pageToken=next_page_token
    )
    response = request.execute()

    for item in response['items']:
        if item['id']['kind'] == 'youtube#video':
            video_ids.append(item['id']['videoId'])

    next_page_token = response.get('nextPageToken')

    if not next_page_token:
        break

print(f"✅ Total videos fetched: {len(video_ids)}")

# -------------------------------
# 📊 Step 6: Get stats for each video
# -------------------------------
videos_data = []

for video_id in video_ids:
    video_request = youtube.videos().list(
        part='snippet,statistics,contentDetails',
        id=video_id
    )
    video_response = video_request.execute()

    for item in video_response['items']:
        video_title = item['snippet']['title']
        publish_date = item['snippet']['publishedAt']
        views = item['statistics'].get('viewCount', 0)
        likes = item['statistics'].get('likeCount', 0)
        comments = item['statistics'].get('commentCount', 0)
        duration = item['contentDetails']['duration']

        videos_data.append({
            'video_id': video_id,
            'title': video_title,
            'publish_date': publish_date,
            'views': views,
            'likes': likes,
            'comments': comments,
            'duration': duration
        })

# -------------------------------
# 💾 Step 7: Save the data to a CSV file
# -------------------------------
df = pd.DataFrame(videos_data)
df.to_csv('youtube_figma_data.csv', index=False)

print("🎉 Done! Your data has been saved to youtube_figma_data.csv")
  






