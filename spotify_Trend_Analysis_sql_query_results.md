
# Trend Analysis Questions 
## _Questions to Analyze trend_

1. What is The avg popularity for the top 10 genre ?
2. Who are the Top 5 popular artists?
3. What are the current top 5 songs that are trending?
4. Which categories of emotions in songs are currently popular among listeners?
5. What is the comparative popularity between explicit and non-explicit content?
6. What is the music duration people prefer ?
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Trend Analysis
1.What is The avg popularity For the top 10 genre ?

```SQL
SELECT DISTINCT
    track_genre,
    ROUND(AVG(popularity),2) avg_popularity
FROM 
    spotify
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10;
```
![Screenshot 2023-08-26 110623](https://github.com/SRG69/Spotify-database/assets/131379055/2ae5ce50-e439-47ef-a4df-755adf78ae7a)

2. Who are the Top 5 popular artists?

```SQL
SELECT DISTINCT
	artists,
    popularity
FROM 
	spotify
ORDER BY 2 DESC
LIMIT 5;
```
![Screenshot 2023-08-26 111304](https://github.com/SRG69/Spotify-database/assets/131379055/cb370d4f-3d2a-411c-a95e-1472b3df3ffa)

3. What are the current top 5 songs that are trending?
```SQL
SELECT DISTINCT
    track_name,
    artists,
    popularity
FROM 
	spotify
ORDER BY 3 DESC
LIMIT 5;
```
![Screenshot 2023-08-26 112222](https://github.com/SRG69/Spotify-database/assets/131379055/98420b65-04b5-4d1e-a938-17c5e314a863)

4. Which categories of emotions in songs are currently popular among listeners?
   _Emotion of a song also known as (valence) is measured between 0.0 to 1.0_
```SQL
SELECT 
    CASE 
	WHEN valence >= 0.8 THEN 'Positive Emotion'
        WHEN valence BETWEEN 0.5 AND 0.7 THEN 'Neutral Emotion'
        ELSE 'Negative Emotion' 
	END AS emotions,
    COUNT(DISTINCT track_id) Total_songs
FROM 
	spotify
GROUP BY 1
ORDER BY 2 DESC;
```
![Screenshot 2023-08-26 113326](https://github.com/SRG69/Spotify-database/assets/131379055/a7d02520-b4fc-42a9-a81e-4700669477e9)

5. What is the comparative popularity between explicit and non-explicit content?
``` SQL
SELECT 
	explicit,
	ROUND(AVG(popularity),2) avg_popularity
FROM 
	spotify
GROUP BY 1
ORDER BY 2 DESC;
```
![Screenshot 2023-08-26 115507](https://github.com/SRG69/Spotify-database/assets/131379055/a6911e42-c7eb-468a-9aad-e64be37fa0f9)

6. What is the music duration people prefer?

	1. sweet spot between 3min and 3.9 min
	2. short between 2 and 2.9
	3. very short < 1.9
	4. long between 4 and 5.9

```SQL
WITH cte AS (
SELECT DISTINCT
	track_genre,
    track_name,
    duration_min,
    
	CASE 
	WHEN duration_min BETWEEN 3 AND 3.9 THEN 'sweet spot' 
        WHEN duration_min BETWEEN 2 AND 2.9 THEN 'short'
        WHEN duration_min < 1.9 THEN 'Very short'
        WHEN duration_min BETWEEN 4 AND 5.9 THEN 'Long'
        ELSE 'Very Long'
	END AS duration,
    
    popularity
FROM 
	spotify
ORDER BY 5 DESC)

 #duration people prefer 
SELECT 
	duration,
	COUNT(duration) 
		-- / 
-- 	 (SELECT COUNT(DISTINCT track_id) FROM spotify) * 100
    AS 'duration_people_prefer'
FROM cte
UP BY 1
ORDER BY 2 DESC;

SELECT 
	ROUND(AVG(duration_min),2) duration_min
FROM 
	spotify
```
![Screenshot 2023-08-26 171947](https://github.com/SRG69/Spotify-database/assets/131379055/5597bab9-5b73-4467-b397-3075620c460b)

![duration](https://github.com/SRG69/Spotify-database/assets/131379055/850579d1-20b9-463f-8654-bdcc8089baac)

