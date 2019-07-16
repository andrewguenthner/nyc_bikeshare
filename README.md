# nyc_bikeshare
analysis, visualization, and forecasting of New York City's bikeshare program

The project consists of a set of Tableau dashboards available online at:
https://public.tableau.com/profile/andrew.guenthner#!/vizhome/nyc_bike_book1/TripGrowth

A detailed description of the rationale behind the visualizations is provided in the design doc

In order to process the data, two Jupyter Notebooks are used.  These are built so as to 
allow the user to pick a month, and provided that trip data for that month has been 
downloaded into the data/trips sub-directory, along with data for the same month in the
preceding year, the notebooks will output data that can be used to refresh the visualizations 
in Tableau with the latest data.  

NOTE:  Due to large file size, the data/trips sub-directory is not present in the GitHub repo.
You will need to create this sub-directory within the "data" folder, and then download the 
files from the Citibike web site at https://s3.amazonaws.com/tripdata/index.html.  Each 
monthly data file is more than 300 MB, so plan accordingly. For convenience, a set of daily 
rider data files is provided in the repo.  

Note that the raw data files need to be downloaded from the New York Citibike web site, at:
https://s3.amazonaws.com/tripdata/index.html   (trip data)
https://www.citibikenyc.com/system-data    (daily ridership data, aggregated by quarter)

The trip data typically consists of about 2 million rows of data, so moving large amounts of 
this data around can be cumbersome.  The notebooks should be run first to generate the hourly 
data (process_nyc_bike_data_for_tableau.jypnb) -- this will provide output in a more compact 
form (about 300k rows), and then the commuter estimate can be run (estimate_commuters.jypnb) 
as well, using the output from process_nyc_bike_data_for_tableau.jypnb.  

Note that the notebook expect certain naming conventions to be followed.  If the New York 
Citibike program changes their file naming system, the notebooks will need to be edited. 

To make Tableau work properly, up to eight sets of quarterly data -- every quarter year-to-date 
for the current and previous year, are needed.  In addition, data from the current quarter for 
years further in the past to 2014 is needed to replicate the visualizations exactly.  The Tableau 
union function can be used to join this data.  Cases where the union fails due to minor column 
naming differences have been avoided in this visualization, but if you wish to look at other data,
please be aware that some further munging of columns may be needed.  The hourly trip and esimated 
commuter data can be set up as independent data sets on sheets as needed.  Only the data on commuters 
requires the commuter dataset, but quite a few sheets require hourly data.  

The notebooks list their requierd environments, but generally speaking they need Numpy 1.16 and 
Pandas 0.24.  The commuter estimation notebook also needs scikit-learn 0.21.  
