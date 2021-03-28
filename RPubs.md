Untitled
================

## GitHub Documents

This is an R Markdown format used for publishing markdown documents to
GitHub. When you click the **Knit** button all R code chunks are run and
a markdown file (.md) suitable for publishing to GitHub is generated.

## Including Code

You can include R code in the document as follows:

# downloading data

Url\_data \<-
“<https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2FMain_data.csv.bz2>”

File\_data \<- “StormData.csv.bz2” if (\!file.exists(File\_data)) {
download.file(Url\_data, File\_data, mode = “wb”) }

# reading data

Raw\_data \<- read.csv(file = File\_data, header=TRUE, sep=“,”)

# subsetting by date

Main\_data \<- Raw\_data
Main\_data\(BGN_DATE <- strptime(Raw_data\)BGN\_DATE, “%m/%d/%Y
%H:%M:%S”) Main\_data \<- subset(Main\_data, BGN\_DATE \>
“1995-12-31”)

Main\_data \<- subset(Main\_data, select = c(EVTYPE, FATALITIES,
INJURIES, PROPDMG, PROPDMGEXP, CROPDMG, CROPDMGEXP))

\#cleaning event types names
Main\_data\(EVTYPE <- toupper(Main_data\)EVTYPE)

# eliminating zero data

Main\_data \<-
Main\_data\[Main\_data\(FATALITIES !=0 |  Main_data\)INJURIES \!=0 |
Main\_data\(PROPDMG !=0 |  Main_data\)CROPDMG \!=0,
\]

``` 
                   Health_data <- aggregate(cbind(FATALITIES, INJURIES) ~ EVTYPE, data = Main_data, FUN=sum)
```

Health\_data\(PEOPLE_LOSS <- Health_data\)FATALITIES +
Health\_data\(INJURIES Health_data <- Health_data[order(Health_data\)PEOPLE\_LOSS,
decreasing = TRUE), \] Top10\_events\_people \<- Health\_data\[1:10,\]
knitr::kable(Top10\_events\_people, format = “markdown”)

\#creating total damage values library(dplyr) Main\_data \<-
mutate(Main\_data, PROPDMGTOTAL = PROPDMG \* (10 ^ PROPDMGEXP),
CROPDMGTOTAL = CROPDMG \* (10 ^
CROPDMGEXP))

``` 
                Economic_data <- aggregate(cbind(PROPDMGTOTAL, CROPDMGTOTAL) ~ EVTYPE, data = Main_data, FUN=sum)
```

Economic\_data\(ECONOMIC_LOSS <- Economic_data\)PROPDMGTOTAL +
Economic\_data\(CROPDMGTOTAL Economic_data <- Economic_data[order(Economic_data\)ECONOMIC\_LOSS,
decreasing = TRUE), \] Top10\_events\_economy \<-
Economic\_data\[1:10,\] knitr::kable(Top10\_events\_economy, format =
“markdown”)

\#plotting health loss library(ggplot2) g \<- ggplot(data =
Top10\_events\_people, aes(x = reorder(EVTYPE, PEOPLE\_LOSS), y =
PEOPLE\_LOSS)) g \<- g + geom\_bar(stat = “identity”, colour = “black”)
g \<- g + labs(title = “Total people loss in USA by weather events in
1996-2011”) g \<- g + theme(plot.title = element\_text(hjust = 0.5)) g
\<- g + labs(y = “Number of fatalities and injuries”, x = “Event Type”)
g \<- g + coord\_flip() print(g)

\#plotting economic loss g \<- ggplot(data = Top10\_events\_economy,
aes(x = reorder(EVTYPE, ECONOMIC\_LOSS), y = ECONOMIC\_LOSS)) g \<- g +
geom\_bar(stat = “identity”, colour = “black”) g \<- g + labs(title =
“Total economic loss in USA by weather events in 1996-2011”) g \<- g +
theme(plot.title = element\_text(hjust = 0.5)) g \<- g + labs(y = “Size
of property and crop loss”, x = “Event Type”) g \<- g + coord\_flip()
print(g)

## Including Plots

You can also embed plots, for example:

![](RPubs_files/figure-gfm/pressure-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to
prevent printing of the R code that generated the plot.
