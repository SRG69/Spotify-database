
# Trend Analysis Questions 
## _Questions to Analyze trend_

1. Top 10 genres have the highest average track popularity?
2. Top 10 performing artists 
3. Top 5 songs currently in trend
4. What type of Emotions are popular ?
5. T0p 10 artists and there highest no_of tracks
6. What percentage of explicit and non-explicit tracksa are there in the dataset ?
7. Popularity of Explicite and Non-explicit content
8. avg_durations_song
9. no of popular songs of top 5 artists

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Trend Analysis
1.Top 10 genres have the highest average track popularity?

```SQL
SELECT DISTINCT
    track_genre,
    ROUND(AVG(popularity),2) avg_popularity
FROM 
    spotify
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10;
![](https://github.com/SRG69/Spotify-database/blob/main/insigt_png/avg_popularity%20track%20genre.png)







