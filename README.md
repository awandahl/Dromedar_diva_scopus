# dromedar_diva_scopus
Dromedar_diva_scopus is an R-script for getting publication data from [DiVA](https://info.diva-portal.org/consortium/), extracting missing identifiers ([DOIs](https://www.wikidata.org/wiki/Property:P356), [ScopusIds (EID)](https://www.wikidata.org/wiki/Property:P1154) and [PMIDs](https://www.wikidata.org/wiki/Property:P698)), looking for these missing identifiers in the [Scopus API](https://dev.elsevier.com/academic_research_scopus.html), and eventually producing csv-files in return for manual upload to the DiVA database. There is no reason why this script can't be used for other purposes as long as the initial csv file is formatted in the same way as the output file from DiVA. Please have a look at the `sample.csv` which you will find in the repository. As for the connection to the Scopus API, I rely on code written by [Christopher Belter](https://github.com/christopherBelter/scopusAPI). Christopher mentions a limit on how many records you can retrieve per week from the Scopus API. I have however overridden that limit by far so I guess this have changed. I have kept the number of records to be fetched at a time to 25 as I find it soothing to watch the retrieval process. The code is ugly and I don't promise it will do you any good. You have the sole responsibility for whatever will happen when you run the code, and also for the accuracy of the output files. If you understand this, please go ahead!

- You obviously need to have a subscription to the Scopus database and have a network connection that belongs to the subscribing institution.
- Install the R libraries `httr, xml and readr` ("Tools" > "Install Packages" in [RStudio](https://rstudio.com/products/rstudio/download/)).
- Put files `dromedar_diva_scopus.R, scopusAPI.R and split_csv.R` in the same directory
- Edit the `"diva_url"` parameter to your liking. The url is initially made by doing a ["create feed"/"utsökning"](https://wiki.epc.ub.uu.se/display/divainfo/CSV-generator) in the DiVA web interface. You should probably change the beginning of the url to your institution, maybe change the years and the number of publications you want. As the sample `"diva_urls"` in `dromedar_diva_scopus.R` are written right now, they will only pick up articles, reviews and conference papers. This can be changed too of course. The default maximum number of publications is 9999, but I have overridden that limit by a factor of seven at one occasion without any problems.
- Insert your [Scopus API key](https://dev.elsevier.com/index.html) at line 9 and 52 in `scopusAPI.R` (replace the text `API_KEY_HERE`).
- Run `dromedar_diva_scopus.R`
- You will see that the program fetches a csv-file from DiVA (according to your settings). Then it will search the Scopus API for the missing identifiers (which may take four rounds and some time), and finally the search results from Scopus are merged with the csv you downloaded from DiVA in the first place.
- In the best of worlds you will find up to four csv-files in the directory. They look like: `File_1_New_ScopusId_20200313_160752_.csv`. The number of files is of course depending on the number of identifiers that are missing in your instance of DiVA. The files contain one column for the PID of your publication and another containing the new identifier. Each file is limited to 250 records, since this is the maximum number that can be safely inserted manually into the DiVA database. In order to prevent confusion I think it is a good habit to move these files out of the directory before you make a new run of the program.
- Good luck and enjoy! I'm happy to answer any questions at aw (at) kth.se
