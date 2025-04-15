Statistics for the weeklyOSM issues from WN272 (29/09/2015-05/10/2015) to WN768 (03/04/2025-09/04/2025)


* article_per_category....csv

SELECT category, COUNT(*) AS articles_per_category, MIN(blog) as min_wn, MAX(blog) as max_wn
        FROM weekly_issues
        GROUP BY category ORDER BY category

* categories_actual_data...csv

SELECT distinct category from weekly_issues
        ORDER BY category ASC;

* top_categories...csv

SELECT category, count(*) from weekly_issues
        GROUP BY category
        ORDER BY count(*) DESC;

* Most frequent words in the table weekly_issues, column markdown, according to category.

ndoc .. the number of rows 

nentry .. the number of occurrences (can be bigger with multiple instances in a single text).

1 - top_sites_category_software...csv

SELECT word, ndoc, nentry
FROM   ts_stat($$SELECT to_tsvector('english', markdown) FROM weekly_issues WHERE category='Software'$$) 
WHERE (word LIKE '%.org%') 
or (word LIKE '%.de%') 
and (word NOT LIKE 'blog.openstreetmap.de/wp-uploads/2016/12/de.svg)')
and (word NOT LIKE '%blog.openstreetmap.de/wp-uploads/2016/12/ru.svg)%')
and (word NOT LIKE '%blog.openstreetmap.de/wp-uploads/2016/12/fr.svg)%')
and (word NOT LIKE '%blog.openstreetmap.de/wp-uploads/2016/12/ja.svg)%')
ORDER  BY nentry DESC
LIMIT  100;

2 - top_sites_category_programming...csv

SELECT word, ndoc, nentry
FROM   ts_stat($$SELECT to_tsvector('english', markdown) FROM weekly_issues WHERE category='Programming'$$) 
WHERE ((word LIKE '%.org%') or (word LIKE '%.de%') 
and  (word NOT LIKE '%blog.openstreetmap.de/wp-uploads/2016/12/de.svg)%')
and (word NOT LIKE '%blog.openstreetmap.de/wp-uploads//2016/12/de.svg)%')
and (word NOT LIKE '%blog.openstreetmap.de/wp-uploads/2016/12/ru.svg)%')
and (word NOT LIKE '%blog.openstreetmap.de/wp-uploads/2016/12/fr.svg)%')
and (word NOT LIKE '%blog.openstreetmap.de/wp-uploads/2016/12/ja.svg)%')
and (word NOT LIKE '%blog.openstreetmap.de/wp-uploads/2016/12/es.svg)%')
and (word NOT LIKE '%www.openstreetmap.org/user/%')) and nentry > 1
ORDER  BY nentry DESC
LIMIT 100;



