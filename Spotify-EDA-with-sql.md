# Performing EDA with MySQL And Ms Power BI 

## Here are some questions For EDA 

# Changing Duration Millisecond Into duration Min
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


