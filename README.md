# weeklyOSM-stats

---

Statistical files for the weeklyOSM, initially static and considering the numbers WN272 (29/09/2015-05/10/2015) to WN768 (03/04/2025-09/04/2025).

> Disclaimer: these datasets are licensed under the GPL 3.0.
> 
> For more information, please refer to <https://www.gnu.org/licenses/gpl-3.0.pt-br.htm>
> 
> How to refer this research: SOUTO, R.D. weeklyOSM-stats. Available at https://github.com/raqueldeziderio/weeklyOSM-stats. GPL 3.0.
> 
> This analysis is under development. To keep contact about this initiative: ivides@ivides.org, a/c: Dr. Raquel Dezidério Souto. Colaborated to this research: Strubbl, derFred and TheFive.
> 
> About the OSM-Wochennotiz (weeklyOSM): [Issue #1, on July 23, 2010](https://blog.openstreetmap.de/blog/2010/07/osm-wochennotiz-nr-1/) [actual domain](https://weeklyosm.eu/).
>

---

# Results with 102 selected softwares (by May 06, 2025)


## [Participation of the selected softwares in its software group](https://github.com/raqueldeziderio/weeklyOSM-stats/tree/main/graphics_software_in_group) [graphics, EN]

## [Participação dos softwares selecionados no grupo de softwares](https://github.com/raqueldeziderio/weeklyOSM-stats/tree/main/graficos_software_no_grupo) [gráficos, PT]

---

# Scope and general objective

The actual weeklyOSM is multilingual and is considering 15 languages. It has the English version as the standard to the AI translation to the other 14 languages, using the [DeepL](https://www.deepl.com/). Initially, it was published in five other languages - Inglês, Espanhol, Turco, Romeno and Japonês, translated from the [Wochennotiz](https://wiki.openstreetmap.org/wiki/Wochennotiz), the German blog, starting in [July 2010](http://blog.openstreetmap.de/blog/2010/07/osm-wochennotiz-nr-1/).

The objective of this analysis is to prospect the most cited categories and softwares, considering the period from 2015 (WN272) to 2025 (WN768), since the adoption of the OpenStreetMap Blog Collector or [OSMBC system](https://github.com/TheFive/osmbc), developed by TheFive.

# But... why calculate it?

These statistics can be a *proxy* for understanding the use of OSM-related software by the OSM mappers community and which categories have received the most attention in various media, such as social networks, blogs, OSMF channels or institutional news sites.


# About the files in this repo

* The files with specific selection according to the application type - editors, navigators, QA analysis and others, are stored in the folder **/selection** and the files generated by PGSQL queries with statistics is in the folder **/statistics** in this project. 

* The softwares were selected according to these websites and the citation in weeklyOSM's articles:


   <https://wiki.openstreetmap.org/wiki/Comparison_of_editors>
   
   
   <https://osm-apps.org/?category=edit> ("Improve the map" category)
   
   
   <https://wiki.openstreetmap.org/wiki/List_of_OSM-based_services>
  

  <https://software.wambachers-osm.website/>

  <https://wiki.openstreetmap.org/wiki/Editor_usage_stats>
  

* The .CSV files has these overall delimiters: comma (,) for records and double quote (") for quote and scape.


## Sequence of steps 

### Initial file

* Considering only EN version - principal version that is translated to the other 14 languages.
768 issues, being:
  
* WN001 a WN271 - without articles (markdown column) - desconsidered, because of the initial weeklyOSM workflow that 
         was different of today.    

* WN272 to WN768 - considered to this analysis

* 35 categories and 32,261 records (articles)
  
### Initial cleaning

* Deleting the WN001 to WN271 - empty articles
   
* Deleting the articles in the following categories, because not corresponding to actual categories or corresponding to 
   unpublished articles:
   
   [Actual Category] (68 records), automatically translated links of this week (1), exerciseEN: (8), Long Term Dates (3),
   -- no category yet -- (5), Not translated (3), unpublished (3,013).

  18,672 records (after the initial cleaning)
        
### Standardizing categories
   
* Standardizing 'Did you know...' and 'Did you know that...'  to the actual category (Did you know that...) (1,142 records)

   UPDATE weekly_issues set category='Did you know that …' WHERE category='Did you know …'
   
   
* Standardizing Licences (en-GB) and Licenses (en-US) to the actual category (Licenses) (138 records)

   UPDATE weekly_issues set category='Licenses' WHERE category='Licences'
  

* Standardizing 'SotM 2016' to 'Events'

  UPDATE weekly_issues set category='Events' WHERE category='SotM 2016'
    
* Standardizing '#switch2OSM' and 'switch2OSM' to 'OSM in action'

  UPDATE weekly_issues set category='OSM in action' WHERE category='switch2OSM' OR category='#switch2OSM'
   
### Dataset Analysis - generation of the statistics
   
For more details, please, refer to the /statistics/README.md in this repo.

After cleaning and standardizing processes:

18,672 records
   
24 categories: About us, Breaking news, Community, Did you know that…, Education, Events, Humanitarian OSM, Imports, Licenses, Local chapter news, Mapping, Mapping campaigns, Maps, Open Data, OpenStreetMap Foundation, OSM in action, OSM in the media, OSM research, Other Geo Things, Picture, Programming, Releases, Software, Upcoming Events

### Final file - selected software articles

5,042 records
24 categories

### Statistics files

Please, see the folder [statistics](https://github.com/raqueldeziderio/weeklyOSM-stats/tree/main/statistics)

### Selected software files

Please, see the folder [selection](https://github.com/raqueldeziderio/weeklyOSM-stats/tree/main/selection)
   
