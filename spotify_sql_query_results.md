
# Trend Analysis Questions 
## _Questions to Analyze trend_

1. What is The avg popularity for the top 10 genre ?
2. Who are the Top 5 popular artists?
3. What are the current top 5 songs that are trending?
4. Which categories of emotions in songs are currently popular among listeners?
5. What is the comparative popularity between explicit and non-explicit content?
6. Top 10 artists and there highest no_of tracks
7. What percentage of explicit and non-explicit tracksa are there in the dataset ?
8. avg_durations_song
9. no of popular songs of top 5 artists

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
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

2. Who are the Top 5 performing artists?

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



