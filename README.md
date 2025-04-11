# weeklyOSM-stats

Storage of statistical files for the weeklyOSM , initially static and considering the numbers WN272 (29/09/2015-05/10/2015) to WN768 (03/04/2025-09/04/2025).

All processes with SQL statements - SELECT, DELETE, UPDATE, in the PostgreSQL.

* This analysis is under development. To keep contact about this initiative: ivides@ivides.org, a/c: Dr. Raquel Dezidério Souto

===== Sequence of steps ======

1. Initial file

   Considering only EN version - principal version that is translated to the other 14 languages.
   768 issues, being: 
         WN001 a WN271 - without articles (markdown column)* - desconsidered
         WN272 to WN768 - considered to this analysis
         * Because of the initial weeklyOSM workflow that was different of today.

   43 categories
   32.261 - total dataset
   3.013 - unpublished records
  
2. Initial cleaning

   Deleting the WN001 to WN271 - empty articles
   Deleting the articles in the following categories, because not corresponding to actual categories or corresponding to 
   unpublished articles:
         [Actual Category] (68 records), automatically translated links of this week (1 record), exerciseEN: (2), Future,
         Long Term Dates (3), -- no category yet -- (5), Not translated (3), #switch2OSM (7), switch2OSM (282), unpublished 
         (3,013), SotM 2016 (5).

   delete from weekly_issues where (category='[sentence here]')
        
3. Standardizing categories
   
   Standardizing 'Did you know...' and 'Did you know that...'  to the actual category (Did you know that...) (1,142 records)

   update weekly_issues set category='Did you know that …' where category='Did you know …'
   
   Standardizing Licences (Een-GB) and Licenses (en-US) to the actual category (Licenses) (138 records)

   update weekly_issues set category='Licenses' where category='Licences'
   
4. Analysis dataset
   
   After cleaning and standardizing processes:

   18.755 records
   24 categories as below:

    About us
    Breaking news
    Community
    Did you know that…
    Education
    Events
    Humanitarian OSM
    Imports
    Licenses
    Local chapter news
    Mapping
    Mapping campaigns
    Maps
    Open Data
    OpenStreetMap Foundation
    OSM in action
    OSM in the media
    OSM research
    Other Geo Things
    Picture
    Programming
    Releases
    Software
    Upcoming Events
   
5. Files storage

   The files with specific selection according to the application type - editors, navigators, QA analysis and others are 
   stored in the folders /selection /statistics in this project.
   Delimiter - comma (,)
   Quote and Scape - double quote (")
   
