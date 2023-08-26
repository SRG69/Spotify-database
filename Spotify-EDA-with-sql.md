# 🕵️ Performing EDA with MySQL 🕵️

## Here are some questions For EDA 

### Changing Duration Millisecond Into duration Min
```SQL
ALTER TABLE spotify
ADD COLUMN duration_min FLOAT;

SET SQL_SAFE_UPDATES = 0;

UPDATE spotify
SET duration_min = duration_ms / 60000;

ALTER TABLE	spotify
DROP COLUMN duration_ms;
```

## Basic Overview:
1. How many Duplicates valur are there In dataset ?
   
```SQL
SELECT 
	COUNT(*) - COUNT(DISTINCT track_id) AS total_duplicate_tracks
FROM spotify;
```
![Screenshot 2023-08-26 212036](https://github.com/SRG69/Spotify-database/assets/131379055/994ba0bf-5459-453b-a0a6-abd2cb2fa285)

2. What Are the total Number of tracks In the data set ?

```SQL
SELECT 
	COUNT(*) total_number_of_tracks
FROM 
	spotify;
```
![Screenshot 2023-08-26 212348](https://github.com/SRG69/Spotify-database/assets/131379055/1c564513-ea2d-4b01-9d9a-3ccfe2d01962)

3. What is the average duration of tracks ?
```SQL
SELECT 
	ROUND(AVG(duration_min),2) avg_duration
FROM 
	spotify;
```
![Screenshot 2023-08-26 212612](https://github.com/SRG69/Spotify-database/assets/131379055/9078529f-6d2c-4319-84ee-4ba32c8e85b6)

4. What Is the number of explicit and non-explicit tracks.
```SQL
SELECT 
	COUNT(DISTINCT CASE  WHEN Explicit = 'TRUE' THEN track_id ELSE NULL END) 'explicit_music',
    
	COUNT(DISTINCT CASE  WHEN Explicit = 'FALSE' THEN track_id ELSE NULL END) 'non_explicit_music'  
FROM 
	spotify;
```
![Screenshot 2023-08-26 212934](https://github.com/SRG69/Spotify-database/assets/131379055/0764003e-28b4-4455-a4c9-660695f0c975)

## Artist Insights:
1. Identify the top 5 most popular artists based on the average track popularity.
```SQL
SELECT 
	artists, 
	ROUND(AVG(popularity),2)  average_popularity
FROM 
	spotify
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5;
```
![Screenshot 2023-08-26 213140](https://github.com/SRG69/Spotify-database/assets/131379055/14e4c6e8-b140-48ff-b326-2a5a37cabd11)

2. Who are the top 10 artists who has most contribution of songs in the dataset ?
```SQL
SELECT 
	artists, 
	COUNT(DISTINCT track_id)  No_of_songs 
FROM
	spotify
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10;
```
![Screenshot 2023-08-26 213617](https://github.com/SRG69/Spotify-database/assets/131379055/663a694b-d2d8-496c-be31-9a4065116514)

## Genre Analysis

1. What are the unique genres present in the dataset.
```SQL
SELECT DISTINCT 
    track_genre
FROM 
	spotify;
```
![Screenshot 2023-08-26 214037](https://github.com/SRG69/Spotify-database/assets/131379055/d51aa2f3-e7cf-4716-9ccc-8fb55b293f9f)

2. What are the Top 10 popular Genre ?
```SQL
SELECT 
	track_genre, 
	ROUND(AVG(popularity),2) AS popularity
FROM 
	Spotify
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10;
```
   
![Screenshot 2023-08-26 214337](https://github.com/SRG69/Spotify-database/assets/131379055/26fe489d-9ab3-4da1-a4b0-b108d932e2c4)





