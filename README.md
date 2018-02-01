# owf-data-co-river-outfitters

This repository contains the [Open Water Foundation (OWF)](http://openwaterfoundation.org) dataset for Colorado River Outfitters.  The goal of this dataset is to establish an inventory of outfitters, in order to indicate the level of recreational use and to potentially connect this information to river data, such as flows.
This is a foundational dataset that provides unique identifiers and other data for river outfitters and the identifiers can be used to link other datasets, such as the [Source Water Route Framework](http://cdss.state.co.us/GIS/Pages/AllGISData.aspx).
OWF has created and is maintaining this dataset to facilitate work on various data analysis and visualization projects in Colorado.  **Note that this work is initially focused on the South Platte Basin and, in particular, those outfitters that operate on Clear Creek and the Cache la Poudre River.  The dataset will continue to be filled in as time and resources permit.** 

The following sections provide a summary of the project repository:

* [Connections to the Colorado Water Plan and the Statewide Water Supply Initiative 2010](#connections-to-the-colorado-water-plan-and-the-statewide-water-supply-initiative-2010)
* [How to Use the Data](#how-to-use-the-data)
* [Repository Contents](#repository-contents)
* [Attribution](#attribution)
* [Data Workflow](#data-workflow)
* [Data Issues](#data-issues)
* [Additional Resources](#additional-resources)
* [Disclaimer](#disclaimer)
* [License](#license)
* [Contributing](#contributing)
* [Maintainers](#maintainers)
* [Contributors](#contributors)

## Connections to the Colorado Water Plan and the Statewide Water Supply Initiative 2010 ##

The [Colorado Water Plan (CWP)](https://www.colorado.gov/cowaterplan), completed in 2015, is "a roadmap that leads to a productive economy, vibrant and sustainable cities, productive agriculture, a strong environment and a robust recreation industry."  The plan lays the groundwork for the measurable outcomes, goals and actions required to ensure that the State's municipal, industrial, agricultural, environmental and recreational needs are preserved.  In the CWP, it is stated that every basin roundtable (of which there are 9, representing the major river basins plus the Denver Metro area), discusses the need to protect recreational opportunities.
Specifically, the South Platte basin's environmental and recreational goal is to "fully recognize the importance of, and support the development of, environmental and recreational projects and multi-purpose projects that support water availability for ecologically and economically important habitats and focus areas" (p.6-50).  One of the measurable outcomes of this goal is to "protect and enhance economic values to local and statewide economies derived from environmental and recreational water uses, such as fishing, boating, waterfowl hunting, wildlife watching, camping and hiking" (p. 6-50).  This can be achieved by "maintaining or improving the amount of river miles or flatwater surface acres available to river and flatwater boaters."
Recreation supports tourism, which is a major economic driver in many parts of the state.  In many headwater counties, recreation and tourism are the largest industries ([SWSI 2010](http://cwcb.state.co.us/water-management/water-supply-planning/pages/swsi2010.aspx), p.2-1).


## How to Use the Data ##

The Colorado River Outfitters dataset intends to provide a complete statewide list of river outfitters assembled from multiple sources.  There are identifiers for each outfitter and the dataset allows cross-referencing the identifiers so that other datasets can be joined.  For example, the [Source Water Route Framework](http://cdss.state.co.us/GIS/Pages/AllGISData.aspx), contains measured, named streams from the National Hydrography Dataset and uses GNIS IDs and names.  GNIS IDs and names can be used to understand the number of outfitters operating on a particular river and sections of river that are utilized.
Other potential uses of this dataset include the following.  Note that this largely requires the use of additional data that are not currently in the dataset.  Data issues are discussed in the Data Issues section.
* Creating a point map of outfitters to indicate where boating activities are concentrated.
* Creating a point map of outfitters in which points are sized or color-coded based on an attribute such as number of clients served or number of boats floated.  This can serve to help understand the current state of rafting/boating use.
* Creating a map of the streams that are commercially floated and highlighting the stream miles that are floated by the various outfitters.  This can serve to help understand the current state of rafting/boating use.  These stretches of river would be key candidates for protection of recreational needs.
* Creating a heat map (also known as a raster plot) of daily, or possibly hourly, flows of the river miles that are commercially floated.  Flows can be color-coded to indicate if they are ideal for floating or if they at least meet some minimum flow.  This can serve to help understand what the ideal (or at least minimum) conditions are for rafting, how frequently those conditions are met, and if they have changed over time.  This could be useful for water supply planning so that conflicts over recreational needs can be avoided.  For example, future water development projects could take into account recreational needs if it is known that river outfitters estimate that "X" amount of water is needed from May to September in Clear Creek.  This could then potentially be tied to the average amount of revenue generated by river outfitters in Clear Creek in an average season to indicate the economic importance of maintaining certain flow conditions.
* Creating a heat map of the rafting season of a particular river in which each day is color-coded as yes/no for being a rafting day; the heat map could contain several years of data.  This can serve to help understand the typical rafting season and to assess any trends over time.

The Excel and csv files can be used as tabular datasets as is, to create filtered lists or to link to other datasets.  Data-processing software such as TSTool can be used to link this dataset to other datasets.

The format and contents of the dataset will change over time.  It is recommended to save a copy of the dataset.


## Repository Contents ##

The repository contains the following:

```text
analysis/                                      TSTool software command files to process data into useful forms.
  Process-xlsx-to-csv.TSTool                   TSTool command file that processes the core dataset from .xlsx to .csv.
  Process-xlsx-to-geojson.TSTool               TSTool command file that processes the core dataset from .xlsx to .geojson.  
data-orig/                                     Folder containing original data files downloaded from agency websites.
  Business-Entities-in-Colorado.csv            The data file containing Business Entity IDs for entities registered with the Colorado Department of State filtered to the list of river outfitters
  Business-Entities-in-Colorado-Original.csv   The data file containing original data download from the Colorado Information Marketplace containing Business Entity IDs for entities registered with the Colorado Department of State.
data/                                          Folder containing data files.        
  Colorado-River-Outfitters.csv                The Excel file contents from the RiverOutfitter worksheet converted to a csv file, useful for automated processing.
  Colorado-River-Outfitters.geojson            Spatial data file of the locations of river outfitters.
  Colorado-River-Outfitters.xlsx               Simple Excel file containing core data.
  RiverOutfitter-Stream-Relate.csv             The Excel file contents from the RiverOutfitter_Stream_Relate worksheet converted to a csv file, useful for automated processing.  **IN INITIAL STAGES**
doc/
  ?                                            Additional documentation for the dataset.
.gitattributes                                 Git configuration file indicate repository configuration, in particular handling of line-ending and binary files.
.gitignore                                     Git configuration file to ignore files that should not be committed to the repository.
README.md                                      Explanation of repository contents, data files and sources and TSTool command files used to process the core data into other products.
```

### Colorado-River-Outfitters.xlsx Contents ###

The core Excel workbook that serves as the master data contains the following data columns within the **RiverOutfitter** worksheet.

* **RiverOutfitterName** - name of the river outfitter as stated on the list of river outfitters with ROL IDs from Colorado Parks and Wildlife
* **ROL_ID** - River Outfitter License ID as assigned by Colorado Parks and Wildlife and current as of July 2017
* **ROL_ID_Flag** - data status of ROL_ID values; see more detail below
* **BusinessEntity_ID** - state-assigned identification number for a business entity, from the Colorado Information Marketplace's [Business Entities in Colorado](https://data.colorado.gov/Business/Business-Entities-in-Colorado/4ykn-tg5h/data) dataset, to link state datasets
* **BusinessEntity_ID_Flag** - data status of BusinessEntity_ID values; see more detail below
* **GNIS_Name_CSV** - [Geographic Names Information System](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) name of the river/creek in which the river outfitter operates, to link federal and state datasets; CSV = comma separated values
* **GNIS_Name_CSV_Flag** - data status of GNIS_Name_CSV values; see more detail below
* **GNIS_ID_CSV** - [Geographic Names Information System](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) identifier of the river/creek in which the river outfitter operates, to link federal and state datasets; CSV = comma separated values
* **GNIS_ID_CSV_Flag** - data status of GNIS_ID_CSV values; see more detail below
* **Business_Address** - business address of the river outfitter or its parent company; from the "Business Entities in Colorado" dataset
* **Business_Municipality** - business municipality in which the river outfitter or its parent company is located; note that this may be different from the local office of the outfitter; from the "Business Entities in Colorado" dataset
* **State** - state in which the river outfitter is located
* **Business_ZipCode** - business zip code in which the river outfitter or its parent company is located; from the "Business Entities in Colorado" dataset
* **Municipality_DOLA_LG_ID** - 5-digit identifier used by Colorado's [Department of Local Affairs (DOLA)](https://dola.colorado.gov/lgis/municipalities.jsf) for the municipality in which the river outfitter or its parent company is located, to link DOLA datasets
* **Municipality_DOLA_LG_ID_Flag** - data status of Municipality_DOLA_LG_ID values; see more detail below
* **Latitude** - latitude of the river outfitter or its parent company's business office in decimal degrees
* **Longitude** - longitude of the river outfitter or its parent company's business office in decimal degrees
* **Lat_Long_Flag** - indication of how latitude and longitude were determined; g1 = coordinates are based on the business address of the river outfitter or its parent company
* **Formation_Date** - year the river outfitter or its parent company began operation or was incorporated; from the "Business Entities in Colorado" dataset
* **Formation_Date_Flag** - data status of Formation_Date values; see more detail below
* **Website** - website URL of the river outfitter; from the Colorado River Outfitters Association website
* **Website_Flag** - data status of Website values; see more detail below
* **CROA_Member** - yes/no indication of whether or not the outfitter is a member of the Colorado River Outfitters Association (CROA); from the CROA website
* **Comments** - any additional information, such as the name of the parent company, if applicable


#### Data Flags ####
For many data columns, a second column of the same name with the word "_Flag" added to the column name is present.  These columns are an indication of data status as it relates to missing data.  The following conventions are used:
* G = Value is a known/good value.  
* g = Value is an estimated (but good) value.  The associated cell is also highlighted in yellow.
* N = Value is not applicable for the municipality and a blank cell is expected.
* I = Incomplete values; cell has been populated but may not yet contain all values or may need to be further verified
* M = Value is known to be missing in original source and therefore a blank cell indicates that a value cannot be provided.
* m = Value is estimated to be missing.  The associated cell is also highlighted in gray.
* z = Value is unable to be confirmed.  A value is possible but cannot be confirmed one way or the other.  The associated cell is also highlighted in orange.
* x = OWF has not made an attempt to populate the cell at this time.  The value is missing because OWF has not attempted to find the value.  The associated cell is also highlighted in black.

*Note that colors are visible only in xlsx files and not csv files.*

Single-character flags may also be followed with a number, as in g1.  These flags are specific to certain columns and are detailed above in the descriptions of the data columns.  

Column names are taken from original sources if possible.  For clarity and attribution, agency abbreviations may be added to the original column name.  Column name length is not restricted, therefore, some data representations such as Esri shapefiles may contain truncated column names.  In such cases, alternative formats such as GeoJSON are recommended.

Descriptions of identifiers are also provided in the **Notes** worksheet within the workbook.  This worksheet also details how the original data were downloaded and where to find those files.


Other worksheets within the workbook contain the following:

* **RiverOutfitter_Stream_Relate** worksheet lists the GNIS names and IDs associated with each outfitter.  This worksheet is organized so that each stream associated with an outfitter is its own record.  Therefore, the same outfitter may be listed in more than one row and be associated with a different stream.  This will allow for the establishment of one-to-many relationships when linking to and processing other datasets.  **This worksheet is in the initial stages.**

* **ChangeLog** worksheet indicates any changes made to the dataset, the date they occurred and who made the changes.

* **Metadata_RiverOutfitter** worksheet serves as the metadata for data columns in the **RiverOutfitter** worksheet.


### Colorado-River-Outfitters.csv Contents ###
This file is the **RiverOutfitter** worksheet saved in csv format.  Warning:  if this file is opened directly in Excel, IDs that contain leading zeroes will not show those zeroes.  Instead, import the file into a blank Excel file by selecting Data/Get External Data/From Text.


### Colorado-River-Outfitters.geojson Contents ###
This file is the **RiverOutfitter** worksheet saved in GeoJSON format.  This file should be viewable as a map in the GitHub repository.  It can also be used in GIS and mapping applications.


### RiverOutfitter-Stream-Relate.csv Contents ###
This file is the **RiverOutfitter_Stream_Relate** worksheet saved in csv format.  Warning:  if this file is opened directly in Excel, IDs that contain leading zeroes will not show those zeroes.  Instead, import the file into a blank Excel file by selecting Data/Get External Data/From Text.


## Attribution ##

The data sources for this dataset are listed below.

* This dataset began as a list of river outfitters who have River Outfitter License IDs as assigned by [Colorado Parks and Wildlife](http://cpw.state.co.us/thingstodo/Pages/RiverOutfitterLicensing.aspx).  The [list](http://cpw.state.co.us/Documents/Boating/ROL-License-Holders.pdf) is in PDF format and is current as of July 2017.  The PDF's contents were copied and pasted into an Excel spreadsheet.  These data are the source for the RiverOutfitterName and ROL_ID data columns.  If the "Additional DBA Names if Applicable:" data column (DBA = doing business as) in the original dataset was filled out, then that column was used for the RiverOutfitterName column.  For example, Rocky Mountain Adventures replaced the parent company name Ignacious Ventures because the "doing business as" name is likely to be more well known and is the basis for outfitter websites.  This means that some river outfitters who have the same parent company also have the same ROL_ID.
* The BusinessEntity_ID is from the Colorado Information Marketplace's [Business Entities in Colorado](https://data.colorado.gov/Business/Business-Entities-in-Colorado/4ykn-tg5h/data) dataset and is a state-assigned identification number.  Because this dataset contains over 1.6 million records, OWF first filtered the dataset based on the words "adventure", "river", "angler", "raft", "guide", "whitewater" and "flyfish".  This reduced the number of records to about 12,600 and this dataset was saved in [CSV](https://github.com/OpenWaterFoundation/owf-data-co-river-outfitters/blob/master/data-orig/Business-Entities-in-Colorado-Original.csv) format.  This file was then reformatted and joined to the river outfitter dataset using a TSTool command file [(Process-original-data.TSTool)](https://github.com/OpenWaterFoundation/owf-data-co-river-outfitters/blob/master/data-orig/Process-original-data.TSTool).  Note that this only joined BusinessEntity_IDs for some outfitters due to misspelling of names or if the outfitter was not in the original dataset due to limitations in filtering data.  This dataset is also the source for the Business_Address, Business_Municipality, State, Business_ZipCode and Formation_Date data columns.  **At this time, the business address of the parent company is listed, rather than a more local physical address of the outfitter.  This may change to local addresses in a future version.** 
* The Colorado Department of Local Affairs (DOLA)'s [Local Government Information System](https://dola.colorado.gov/lgis/municipalities.jsf) uses a local government ID (LG ID) for municipalities.  OWF is using DOLA_LG_ID instead of LG ID to add more description to the identifier.  Municipality_DOLA_LG_IDs come from the [Colorado Municipalities](https://github.com/OpenWaterFoundation/owf-data-co-municipalities) dataset created by OWF.
* Each river outfitter has a business or physical address listed in the dataset, but not latitude/longitude coordinates.  To obtain coordinate data, the dataset was opened in [Google Sheets](https://www.google.com/sheets/about/).  An add-on named Geocode by Awesome Table can take an address and convert it to coordinates, as long as the street address, city, state and zip code are provided.  Note that the coordinates are for business offices and may not necessarily be the same as the local office, especially if the river outfitter is owned by a parent company.  
* The U.S. Geological Survey (USGS)'s [Geographic Names Information System (GNIS)](https://geonames.usgs.gov/apex/f?p=138:1:9185633219989) is the Federal and national standard for geographic nomenclature.  The USGS developed the GNIS in support of the U.S. Board on Geographic Names as the official repository of domestic geographic names data.  Most streams in Colorado have a GNIS Name and GNIS ID.  GNIS names and identifiers are also used within the [Source Water Route Framework](http://cdss.state.co.us/GIS/Pages/AllGISData.aspx), a spatial data layer that contains measured, named streams from the National Hydrography Dataset.  GNIS names were confirmed for each outfitter by viewing the outfitter's website to determine on which streams rafting services are provided.
* The [Colorado River Outfitters Association (CROA)](http://www.croa.org/) is a trade association that represents professional river rafting outfitters.  The website lists the CROA members that operate on specific rivers.  Links to outfitter websites are also provided.  This website is the source of the CROA_Member and Website data columns.


## Data Workflow ##
The general workflow is as follows once the basic dataset is created:
1. Data flags are created for many of the data columns that indicate data status as described above.
2. The data are formatted as a table to allow for data filtering.
3. The dataset is saved in .xlsx format.
4. The xlsx-formatted file is opened in TSTool and a short command file [(Process-xlsx-to-csv.TSTool)](https://github.com/OpenWaterFoundation/owf-data-co-river-outfitters/blob/master/analysis/Process-xlsx-to-csv.TSTool) converts the dataset into CSV format, to be used in additional data-processing steps.
5. The xlsx-formatted file is opened in TSTool and a short command file [(Process-xlsx-to-geojson.TSTool)](https://github.com/OpenWaterFoundation/owf-data-co-river-outfitters/blob/master/analysis/Process-xlsx-to-geojson.TSTool) converts the dataset into GeoJSON format.  This step is optional and applicable for datasets in which a map will be created or if further processing will occur in GIS application such as QGIS.


## Data Issues ##
In its current form, the Colorado River Outfitters dataset can be used to produce a map of river outfitters in Colorado.  To advance the utility of this dataset, the following data would be helpful:
* The stream miles on which an outfitter operates, for example, from mile 50.1 to mile 68.3
* Annual (seasonal) number of boats floated per stream reach/river
* Annual (seasonal) number of clients per stream reach/river
* Annual (seasonal) sales totals per river
* Ideal flows for rafting, according to outfitters
* Minimum flows needed for rafting, according to outfitters
* Total number of rafting days per river per season for each outfitter, possibly with start and end dates

This data would largely need to be provided by the individual river outfitters.  Some of this data is available for outfitters operating on the [Arkansas River](http://cpw.state.co.us/placestogo/parks/ArkansasHeadwatersRecreationArea/Documents/Rationing-Agreement-Coordinator/Use_Reports/Boat/Season_Summary_by_Company.pdf) but it is unknown if these data are overall company totals or totals specific to the Arkansas River.


## Additional Resources ##
* [Colorado River Outfitters Association](http://www.croa.org/)
* [Colorado Rafting Association](http://www.coloradoraftingassociation.com/)
* [American Whitewater](https://www.americanwhitewater.org/)
* [Rafting Colorado](http://www.rafting-colorado.net/)


## Disclaimer ##

OWF has created this initial dataset of Colorado river outfitters.  OWF will attempt to fill data gaps as the dataset is used for analysis and funding allows for more data review.  OWF provides no guarantee as to the accuracy of the data.  **Use this dataset at your own risk.**  OWF welcomes feedback to improve the dataset.

## License ##

The license is being determined.  All the data are public so there are not really any restrictions on use.

## Contributing ##

The Open Water Foundation created this dataset as a general resource with simple analyses.
If you use the dataset and have comments, please contact the maintainers and/or use the GitHub issues to provide feedback.

## Maintainers ##

Kristin Swaim (@kswaim, kristin.swaim@openwaterfoundation.org) is the primary maintainer at the Open Water Foundation.

Steve Malers (@smalers, steve.malers@openwaterfoundation.org) is the secondary contact.

## Contributors ##

None yet, other than OWF staff.
