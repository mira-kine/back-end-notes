# Lecture 3.23.2022

## Aggregating

- You can set COUNT(\*) AS total_number_of_cities
- GROUP BY country.country_id
- ORDER BY total_number_of_cities DESC,
  country.country;

- ARRAY_AGG means that you can get all the titles back as an array, and THEN group them
- for ex:

```sql
SELECT
    ARRAY_AGG(title),
    rating,
    rental_rate,
    MIN(title) -- will start from A
    MAX(title)
FROM
    film
GROUP BY
    rating, rental_rate
ORDER BY
    rating DESC;

```

- unnesting make things individual rows
