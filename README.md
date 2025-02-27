# 🎵 Spotify Data Pipeline with SQL
# Project Overview
This project builds a data pipeline to extract track metadata from the Spotify API, store it in a MySQL database, and analyze it using SQL queries. It provides insights into popular tracks, artists, and other key metrics.

# Features
✔️ Extract track details using the Spotify API                                                                                                                                                                    
✔️ Transform raw data (convert duration, clean fields)                                                                                                                                                            
✔️ Load (ETL) into a MySQL database                                                                                                                                                                            
✔️ Analyze trends using SQL queries                                                                                                                                                                                

# Tech Stack
Python (for API integration & data handling)                                                                                                                                                                    
Spotify API (to fetch track details)                                                                                                                                                                        
MySQL (to store and query track data)                                                                                                                                                                        
pandas (for data manipulation)                                                                                                                                                                                

![image](https://github.com/user-attachments/assets/b9cb9b38-f26d-41fe-a5e3-edd9a61e9f4c)


# 1. Create Table
```python
# Create Table Query
create_table_query = """
CREATE TABLE IF NOT EXISTS spotify_tracks (
    id INT AUTO_INCREMENT PRIMARY KEY,
    track_name VARCHAR(100),
    artist VARCHAR(50),
    album VARCHAR(30),
    popularity INT,
    duration_minutes FLOAT
);
"""
```
# 2. Function to extract metadata
```python
def fetch_spotify_track(url):
    track_id = re.search(r'track/([a-zA-Z0-9]+)', url).group(1)  # Extract track ID
    track = sp.track(track_id)  # Fetch track details
    
    track_data = {
        'Track Name': track['name'],
        'Artist': track['artists'][0]['name'],
        'Album': track['album']['name'],
        'Popularity': track['popularity'],
        'Duration (minutes)': track['duration_ms'] / 60000  # Convert ms to minutes
    }
    return track_data
```
# 3. SQL Analysis
```sql
SELECT * FROM spotify_tracks;
```
![image](https://github.com/user-attachments/assets/a4c91f40-f6b0-41e3-a682-00381ca89703)


to find the artist that occurs the most 
```sql
SELECT artist,COUNT(*) as count from spotify_tracks GROUP BY artist ORDER BY count desc;
```
![image](https://github.com/user-attachments/assets/6d9f732e-cd19-49c2-907b-4c7257048698)

most popular track
```sql
SELECT track_name,popularity from spotify_tracks order by popularity desc limit 1;
```
![image](https://github.com/user-attachments/assets/3c994474-a096-4a63-83c3-f59b620df7f9)

