# Broadband II

## Project goals

* Integrate socioeconomic data from census.gov to assess the societal problem identified by the stakeholder
* Provide information at the highest resolution possible for characteristic areas (e.g., rural/urban)
* Support Maine's initiative by building upon the [Purdue analysis](https://www.benton.org/source/purdue-university)

## Broadband I+

* Student repo (spring 2022): https://github.com/ds5010/broadband
* Student github-pages site (spring 2022): https://ds5010.github.io/broadband
* Yune repo (summer 2022): https://github.com/ds5110/project-zyune
* The FCC data made the broadband map available in late November -- too late for DS5010 in Fall 2022

## Background

* [Purdue site](https://www.benton.org/source/purdue-university)
* [Digital divide in the US](https://www.benton.org/headlines/digital-divide-us)
  * This page provides a quick overview of the societal problem
  * I got the link to this site in an email from Meghan (Sep 2022)
  * The recommendation for this site originated w/Maggie Drummond-Bahl -- colleague at MCA

## FCC Form 477 data

This data was used by the class in fall 2022 -- we won't be using it.

* [FCC Form 477 data](https://www.fcc.gov/general/broadband-deployment-data-fcc-form-477)
  * Broadband deployment data are available by state from this link
* CSV download for Maine: https://us-fcc.app.box.com/v/ME-Jun2021-v1
  * This file must be downloaded by hand as a zip file (i.e. requires a button click)
* GEOID: The CSV has a BlockCode column with a 15-digit block code (e.g., 230050111004026) 

## FCC broadband map

This dataset became publicly available in fall 2022.

* [FCC National Broadband Map](https://broadbandmap.fcc.gov/home)
  * This has "search by address" page (non-interactive display on mapbox with hex aggregation))))
  * Search by address takes you to page where you can download data
* [Data download page](https://broadbandmap.fcc.gov/data-download/nationwide-data)
  * state-level download by technology -- "fixed broadband" options: cable, copper, fiber, satellite, fixed
  * the download is a zipped CSV
  * Two columns for geospatial info: "block_geoid" (15 digits FIPS combo), h3_res8_id (15-character unique hex id)
  * This page has a link to the data dictionary (pdf)
* [Data Dictionary (PDF)](https://us-fcc.app.box.com/v/bdc-data-downloads-output)
  * block_geoid
    * 15-digit Census Bureau FIPS code for the censusblock in which the Broadband Serviceable Location is located
    * Value is a valid census block from the latest U.S.Census Bureau decennial
  * h3_res8_id
    * 15-character hexadecimal index for the H3 resolution 8 hexagonal cell
    * in which the Broadband Serviceable Location falls.

## Census.gov

This will be our source for socioeconomic and geographic data.

* [Census TIGER/Line shapefiles](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html)
  * FTP site has archives by state and by layer
  * ZIP files -- file sizes in Maine range from 5.7M (county subdivisions) to 108M for tablock20
  * These files should be downloaded locally and .gitignored
* Use FIPS ids to merge data by Census geographies 
* Census blocks for Maine
  * https://www2.census.gov/geo/tiger/TIGER2022/TABBLOCK20/tl_2022_23_tabblock20.zip

## Maine GIS

Possible alternative to Census.gov

* [Maine GeoLibrary](https://www.maine.gov/geolib/) -- maine.gov
  * Entry point for data catalog and services
* [Maine Census Tracts (2010)](https://maine.hub.arcgis.com/datasets/e7a7e490a9bf4bc08c7507f7aabe0f8a) -- arcgis.com

## GEOIDs

* [Understanding GEOIDs](https://www.census.gov/programs-surveys/geography/guidance/geo-identifiers.html) -- census.gov
  * This link is a great reference!
  * FIPS -- Federal Information Processing Service
    * FIPS codes are usually unique within larger geographic entities
    * states -- 2 digits
    * counties -- 5 digits
    * places -- 7 digits
  * GNIS -- Geographic Names Information System codes...
    * do not have a "nesting relationship" as do FIPS codes
    * include airports, beaches, cemeteries, post offices, etc.
    * do not include roads and highways
    * are assigned sequentially based on date of entry
    * do not represent a geographic hierarchy
    * codes can be up to 10 digits in length
  * Census Bureau Codes
    * these census.gov codes are for areas are not covered by FIPS and GNIS
    * these areas include census divisions, census regions, census tracts, block groups, census blocks and urban areas
    * full GEOISs for many levels of geography combine both FIPS and Census Bureau codes
    * for example: census tracts, block groups and census blocks nest within state and county
      * therefore their GEOIDs contain both the state and county FIPS codes, in which they nest.
* GEOID
  * COSUB = County Subdivision (the recommendation from Meghan)
  * STATE -- 2 digits
  * STATE+COUNTY -- 5 digits
  * STATE+COUNTY+COUSUB -- 10 digits
  * STATE+COUNTY+TRACT+BLOCK GROUP -- 2+3+6+1 -- 12 digits
  * STATE+COUNTY+TRACT+BLOCK -- 2+3+6+4 -- 15 digits -- FCC uses this encoding!
* [County subdivisions](https://www2.census.gov/geo/pdfs/reference/GARM/Ch8GARM.pdf) (PDF)
  * CCD names -- Census County Division
  * The purpose of CCDs is to provide a set of subcounty units that
    * (1) have community orientation; 
    * (2) have visible, stable boundaries; 
    * (3) conform to groupings of census tracts or block numbering areas (BNAs); and 
    * (4) have a recognizable name.
* [standard hierarchy](https://www2.census.gov/geo/pdfs/reference/geodiagram.pdf) (PDF)
  * Chart shows relationship between the various geographic entities
