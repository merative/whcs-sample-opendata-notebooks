
The COVID-19 Processed Literature Notebook is provided as-is. It is intended to be an example notebook that users such as data scientists can use or build upon to perform analysis against the raw data files produced by the Annotator for Clinical Data enrichment process. Two things are provided to support running this notebook:

1. A master index file in CSV format
2. A set of raw data files from the Annotator for Clinical Data enrichment process in zip file format

The CSV file can be downloaded from [here](https://whcs-dev-covid19-data.s3.us-east.cloud-object-storage.appdomain.cloud/iml_04162020.csv.zip).

The data files can be downloaded from these locations: [file1](https://whcs-dev-covid19-data.s3.us-east.cloud-object-storage.appdomain.cloud/iml_04162020_1.zip) [file2](https://whcs-dev-covid19-data.s3.us-east.cloud-object-storage.appdomain.cloud/iml_04162020_2.zip) [file3](https://whcs-dev-covid19-data.s3.us-east.cloud-object-storage.appdomain.cloud/iml_04162020_3.zip)

This notebook shows how to load the master index and begin using it to navigate into the raw data files for analysis and discovery.  The CSV file can be quite large, so typically the user will want to load only specific columns.  If loading only specific columns is still too large, the user may consider breaking the master index into multiple sub-master index files to work with individually and then perform aggregation of those results.  The separating of the master index should be done based on "docId" field value where one docId does not span across sub-master index files.  The raw data files can be unzipped into their own directories but those directories should be under one common root directory.  By doing this, the root directory can be used/set, as specified below, and will support the master index file or any subset of the master index file.

To use the notebook, the steps needed are as follows:
- Download the notebook, CSV file and zip file(s) from the load location
- Unzip zip files into desired location
- Open notebook and modify the CSV_path and raw_files_path variables in the 3rd cell to point to the location where you placed the CSV and the unzipped files
- Begin using the notebook

The notebook begins by loading the master index file into a dataframe.  It then prompts the user to select an attribute name from a ranked list of the top attribute names in the data set (the ranking is done based on counts).  Once the user selects a name, they are presented with a ranked list of preferred names (again based on counts) that support the previously selected attribute name.  Once the user selects the preferred name, they are shown the total number of documents that exist in the raw data set that have an association between that attribute name and that preferred name.  The user is then asked how many of those documents they would like to include in the analysis.  The user can enter any number up to the shown total.  Please be aware that any number above 500 could result in long response times.  Once the number of documents is input, the analysis is run.  When analysis is complete a wordcloud is presented showing a ranking of the surface forms that exist for the selected attribute name+preferred name combination.

Note: The files included represents a large, but subsetted version of the complete enrichment set.  This is because of the prohibitively large size of the complete set.  