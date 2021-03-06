# Polling station data and GIS locations for Pakistan's 2018 elections

This repository hosts [pk_polling_stations_2018.csv](https://github.com/colincookman/pakistan_polling_stations_2018/raw/master/pk_polling_stations_2018.csv), an open dataset in a tidy .csv format of 95,591 polling stations released on July 23 2018 by the Election Commission of Pakistan for the Pakistani general elections for the [national](https://www.ecp.gov.pk/frmGISPublishGE.aspx?type=NA) and [provincial assemblies](https://www.ecp.gov.pk/frmGISPublishGE.aspx?type=PA), including voter registration data and GIS coordinates. Some of these polling stations will be duplicates if they are used for both PA and NA elections. A voter should cast votes for both the national and provincial assembly elections at the same home polling station, so each row is a constituency-polling station.

In the `scrape` folder there is the script that downloaded and scraped the data to produce the file [scraped_ps_data.csv](https://github.com/colincookman/pakistan_polling_stations_2018/raw/master/scrape/scraped_ps_data.csv). The code [01_ps_data_cleanup.R](https://github.com/colincookman/pakistan_polling_stations_2018/blob/master/01_ps_data_cleanup.R) was subsequently used to clean and tidy the initial data scrape to produce the final output.

Please note that *this code is still a work in progress* and data outputs hosted here may be incomplete. For questions, suggestions, or to contribute, please leave an issue here or contact the contributors, Colin Cookman, Luke Sonnet, and Shahan Shahid.

# Data gaps
The biggest gap is that *many* PA constituencies seem to be missing any data whatsoever, due to the ECP not releasing data for those constituencies on their website. We are working to remedy this, but the solution is months in the making unless the ECP fixes their data. Below are the counts of constituencies they released data for:

| Province    | Assembly   | N found constituencies | 
|-------------|------------|------------------------| 
| Balochistan | National   | 7                      | 
| FATA        | National   | 7                      | 
| Islamabad   | National   | 3                      | 
| KPK         | National   | 23                     | 
| Punjab      | National   | 114                    | 
| Sindh       | National   | 44                     | 
| Balochistan | Provincial | 22                     | 
| KPK         | Provincial | 62                     | 
| Punjab      | Provincial | 208                    | 
| Sindh       | Provincial | 71                     | 

Furthermore, within constituencies there are gaps. [validity_checks/ps_sequence_gaps.csv](https://github.com/colincookman/pakistan_polling_stations_2018/raw/master/validity_checks/ps_sequence_gaps.csv) identifies 10384 polling station numbers missing from the available sequence, grouped by constituency. In addition to this, 4,783 polling stations did not report GIS data despite being include in the GIS dataset, and 29 reported erroneous latitude / longitude coordinates located outside of Pakistan.

In 17 cases, male and female voters were listed as being registered despite the absence of a male/female voter booth, and in 13 cases, no booths were reported at all despite reported voter registration figures.

# Plans for expansion
Although we have not yet conducted detailed analysis to confirm co-location in all cases, the unique latitude/longitude coordinates for each polling station should allow for determining the parent/child relationship for all national assembly and provincial assembly constituencies. As a preliminary step, we have identified all unique latitude / longitude coordinates reported within the dataset (37,462), in the file [validity_checks/unique_PS_coords.csv](https://github.com/colincookman/pakistan_polling_stations_2018/raw/master/validity_checks/unique_PS_coords.csv), selecting the first observation in each case where there are duplicates.

The ECP [previously released polling station plans in pdf format](https://www.ecp.gov.pk/frmGenericPage.aspx?PageID=3155), which may offer an opportunity to identify missing polling stations not in the GIS dataset. The pdf polling station plan also includes census block codes associated with each polling station, which are not included in the machine-readable data here. Once joined with [2017 census data](https://github.com/colincookman/pakistan_census), that would allow for more granular data on the percentage of the population registered to vote.

Should the ECP release polling-station level results following the elections on July 25 2018, vote patterns can also be mapped below the constituency level. The use of other geographic data or satellite imagery may offer additional opportunities for analysis.