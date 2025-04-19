Statistics for the weeklyOSM issues from WN272 (29/09/2015-05/10/2015) to WN768 (03/04/2025-09/04/2025)
(this work is under development)

## Description of files

* article_per_category....csv  (number of articles per weeklyOSM's category)

        SELECT category, COUNT(*) AS articles_per_category, MIN(blog) as min_wn, MAX(blog) as max_wn
        FROM weekly_issues
        GROUP BY category ORDER BY category

* categories_actual_data...csv   (list of the actual weeklyOSM's categories)

        SELECT distinct category from weekly_issues
        ORDER BY category ASC;

* software_groups...csv   (list of software groups as defined by this analysis)

* software_groups_stats...csv  (number of weeklyOSM articles per software group)

        SELECT public.software_groups.desc_sg, public.weekly_issues_selection.sg_id, 
        COUNT(weekly_issues_selection.id_select) 
        FROM public.weekly_issues_selection, public.software_groups
        WHERE public.weekly_issues_selection.sg_id=public.software_groups.sg_id
        GROUP BY weekly_issues_selection.sg_id, public.software_groups.desc_sg
        ORDER BY COUNT(weekly_issues_selection.id_select) DESC

* software_index_group....csv  (index as a result of division between the number of articles with a specific software (e.g. JOSM) and the total of records of its software group (e.g. editors))  

        SELECT public.software_stats.name, public.software_groups_stats.desc_sg, 
        public.software_groups_stats.sg_id, 
        public.software_stats.sg_stats_id,
        public.software_stats.ndoc, 
        public.software_groups_stats.count,
        (public.software_stats.ndoc::float/public.software_groups_stats.count)*100 AS index_group
        FROM public.software_stats, 
        public.software_groups_stats
        WHERE public.software_stats.sg_id = public.software_groups_stats.sg_id
        ORDER BY public.software_stats.name ASC

* software_stats....csv  (number of weeklyOSM's articles citing a specific software (e.g. JOSM))

File created with results of various SQL queries, for each software considered by this analysis. For example, for 'Panoramax':

        SELECT * from weekly_issues where (markdown like '%Panoramax%') or (markdown like '%panoramax%') order by blog, category

* top_categories...csv  (categories most cited in weeklyOSM's articles)

        SELECT category, count(*) from weekly_issues
        GROUP BY category
        ORDER BY count(*) DESC;
        

* Top_sites_category_programming...csv  (most frequent sites for each weeklyOSM's 'Programming' category where:
ndoc = number of articles and nentry = number of occurrences (because can be bigger with multiple instances in a single text)).

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

* Top_sites_category_software...csv  (most frequent sites for each weeklyOSM's 'Software' category where:
ndoc = number of articles and nentry = number of occurrences (because can be bigger with multiple instances in a single text)).

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

* weekly_issues_selection....csv  (dataset considering only the articles with softwares chosen to this analysis)





