List all columns for a quick overview:
```SQL
SELECT *
FROM bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights
LIMIT 5;
```
![image](https://github.com/Kanidbifsbfvhfs/KANI/assets/159033206/f3bde2fd-681a-4da8-aed0-9e9031542999)
Filter data based on a specific country:
```SQL
SELECT *
FROM bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights
WHERE country = 'US'
LIMIT 5;
```

![image](https://github.com/Kanidbifsbfvhfs/KANI/assets/159033206/0d999192-e13d-42e3-94f0-f949e4156a22)
Count the total number of searches:
```SQL
SELECT COUNT(*) AS total_searches
FROM bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights;
```
![image](https://github.com/Kanidbifsbfvhfs/KANI/assets/159033206/666d6ad1-68fa-406d-abe4-e3e15a4e0cda)
Total searches by date:
```SQL
SELECT date, COUNT(*) AS daily_searches
FROM bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights
GROUP BY date
ORDER BY date;
```
![image](https://github.com/Kanidbifsbfvhfs/KANI/assets/159033206/61263193-553a-4b82-a512-41f31495cae7)
Search insights for a specific date range:
```SQL
SELECT *
FROM bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights
WHERE date BETWEEN '2021-1-1' AND '2021-6-1'
LIMIT 5;
```
![image](https://github.com/Kanidbifsbfvhfs/KANI/assets/159033206/cd05dd3a-01cc-47c8-9823-226ec6ad474c)
Average searches per day:
```SQL
SELECT AVG(daily_searches) AS avg_searches_per_day
FROM (
    SELECT date, COUNT(*) AS daily_searches
    FROM bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights
    GROUP BY date
);
```
![image](https://github.com/Kanidbifsbfvhfs/KANI/assets/159033206/6eab3aa2-be3b-45e1-8200-9d428c540bb6)
Filter based on multiple conditions:
```SQL
SELECT *
FROM bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights
WHERE country_region = 'US' AND date = '2021-1-1'  
LIMIT 5;
```
![image](https://github.com/Kanidbifsbfvhfs/KANI/assets/159033206/88848d38-1e69-4c35-8ca5-4dd70e5527f0) 
Find the unique countries in the dataset:
```SQL
SELECT DISTINCT country_region
FROM bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights;
```

![image](https://github.com/Kanidbifsbfvhfs/KANI/assets/159033206/af5301d8-0b15-4786-91af-142e2df18b57)
Basic Join by Country:
```SQL
SELECT *
FROM `bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights` AS wsi
INNER JOIN `bigquery-public-data.covid19_open_data.covid19_open_data` AS coda
ON wsi.country_region = coda.country_code
WHERE wsi.country_region = 'United States';
```

![image](https://github.com/Kanidbifsbfvhfs/KANI/assets/159033206/4505f563-ab65-4983-b05a-2c7474b1d5bb)
Left Join'
```SQL
SELECT 
  wsi.date, 
  wsi.country_region, 
  coda.new_confirmed,
FROM `bigquery-public-data.covid19_vaccination_search_insights.covid19_vaccination_search_insights` AS wsi
LEFT JOIN `bigquery-public-data.covid19_open_data.covid19_open_data` AS coda
ON wsi.date = coda.date AND wsi.country_region = coda.country_name
LIMIT 5;
```

![image](https://github.com/Kanidbifsbfvhfs/KANI/assets/159033206/a63f3774-9dfb-44f0-b077-93265b355b0a)
