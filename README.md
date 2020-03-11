# dromedar_diva_scopus
Dromedar_diva_scopus is an R-script for getting publication data from DiVA (https://info.diva-portal.org/consortium/), extracting missing identifiers (DOIs, ScopusIds and PMIDs), looking for these missing identifiers in Scopus, and eventually getting csv-files in return (limited to 250 rows) for manual upload to the DiVA database. There is no reason why this script couldn't be used for other purposes as long as the initial csv file is formatted in the same way as the output file from DiVA. Please look at the sample.csv which you will find in the repository. The code is ugly and I don't promise it will do you any good. You have the sole responsibility for whatever will happen when you run the code, and also for the faultlessness of the output files. If you understand this, please go ahead!

- You obviously need to have a subscription to the Scopus database and have a network connection that belongs to the subscribing institution.
- Install the R libraries httr, xml and readr
- Put files dromedar_diva_scopus.R, scopusAPI.R and split_csv.R in the same directory
- Edit the "diva_url" parameter to your liking. This url is initially made by doing a "create feed"/"utsökning" in the DiVA web interface. You should probably change the beginning of the url to your institution, change the years and the number of publications you want. As the sample "diva_urls" in dromedar_diva_scopus.R are written right now, they will only pick up articles, reviews and conference papers. This can be changed too of course. You can retrieve a maximum of 9999 publications which in many cases means that you have to limit your search, e.g. to one year at a time.
- Insert your Scopus API key at line 9 and 52 in scopusAPI.R (replace the text API_KEY_HERE). You can get your API key here: https://dev.elsevier.com/
- Run dromedar_diva_scopus.R
- You will see that the program fetches a csv-file from DiVA (according to your settings). Then it will search the Scopus API for the missing identifiers (which may take four rounds and some time), and finally the search results from Scopus are merged with the csv you downloaded from DiVA in the first place.
- In the best of worlds you will find up to four csv-files in the directory. They look like: file2_20200310_165056_.csv The number of files is of course depending on the number of identifiers that are missing in your DiVA. The files contain one column for the PID of your publication and another containing the new identifier. Each file is limited to 250 records, since this is the maximum number that can be safely inserted manually into the DiVA database. In order to prevent confusion I think it is a good habit to move these files out of the directory before you make a new run of the program.
- Good luck and enjoy! I'm happy to answer any questions at aw (at) kth.se
