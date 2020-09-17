Week 1 Assignment: Plotting Electric Power Consumption
================

Instructions
------------

This assignment uses data from the UC Irvine Machine Learning Repository, a popular repository for machine learning datasets. In particular, we will be using the “Individual household electric power consumption Data Set” which I have made available on the course web site:

>Dataset: [Electric power consumption](https://d396qusza40orc.cloudfront.net/exdata%2Fdata%2Fhousehold_power_consumption.zip) [20Mb]
>Description:Measurements of electric power consumption in one household with a one-minute sampling rate over a period of almost 4 years. Different electrical quantities and some sub-metering values are available.

The following descriptions of the 9 variables in the dataset are taken from the UCI web site 1. Date: Date in format dd/mm/yyyy 2. Time: time in format hh:mm:ss 3. Global_active_power: household global minute-averaged active power (in kilowatt) 4. Global_reactive_power: household global minute-averaged reactive power (in kilowatt) 5. Voltage: minute-averaged voltage (in volt) 6. Global_intensity: household global minute-averaged current intensity (in ampere) 7. Sub_metering_1: energy sub-metering No. 1 (in watt-hour of active energy). It corresponds to the kitchen, containing mainly a dishwasher, an oven and a microwave (hot plates are not electric but gas powered). 8. Sub_metering_2: energy sub-metering No. 2 (in watt-hour of active energy). It corresponds to the laundry room, containing a washing-machine, a tumble-drier, a refrigerator and a light. 9. Sub_metering_3: energy sub-metering No. 3 (in watt-hour of active energy). It corresponds to an electric water-heater and an air-conditioner.

Loading the data
-----------------

>When loading the dataset into R, please consider the following:
-   The dataset has 2,075,259 rows and 9 columns. First calculate a rough estimate of how much memory the dataset will require in memory before reading into R. Make sure your computer has enough memory (most modern computers should be fine).
-   We will only be using data from the dates 2007-02-01 and 2007-02-02. One alternative is to read the data from just those dates rather than reading in the entire dataset and subsetting to those dates.
-   You may find it useful to convert the Date and Time variables to Date/Time classes in R using the strptime() and as.Date() functions.
-   Note that in this dataset missing values are coded as ?.

```R
download.file('https://d396qusza40orc.cloudfront.net/exdata%2Fdata%2Fhousehold_power_consumption.zip', destfile = './hw1_data.zip', method = 'curl', quiet = T)
unzip(zipfile = 'hw1_data.zip')
```

```R
rawData <- read.table('household_power_consumption.txt', header = T, stringsAsFactors = F, na.strings = "?", sep = ';', quote = "", skip = 66636, nrows = 2880)
tail(rawData, 10)
```

```R
##      X31.1.2007 X23.59.00 X0.326 X0.126 X242.800 X1.400 X0.000 X0.000.1
## 2871   2/2/2007  23:50:00  3.624  0.104   241.11   15.0      0        0
## 2872   2/2/2007  23:51:00  3.628  0.104   241.26   15.0      0        0
## 2873   2/2/2007  23:52:00  3.626  0.104   241.07   15.0      0        0
## 2874   2/2/2007  23:53:00  3.700  0.208   240.72   15.4      0        0
## 2875   2/2/2007  23:54:00  3.696  0.226   240.71   15.2      0        1
## 2876   2/2/2007  23:55:00  3.696  0.226   240.90   15.2      0        1
## 2877   2/2/2007  23:56:00  3.698  0.226   241.02   15.2      0        2
## 2878   2/2/2007  23:57:00  3.684  0.224   240.48   15.2      0        1
## 2879   2/2/2007  23:58:00  3.658  0.220   239.61   15.2      0        1
## 2880   2/2/2007  23:59:00  3.680  0.224   240.37   15.2      0        2
##      X0.000.2
## 2871       18
## 2872       18
## 2873       18
## 2874       18
## 2875       17
## 2876       18
## 2877       18
## 2878       18
## 2879       17
## 2880       18
```

```R
colnames(rawData) <- c('Date', 'Time', 'GlobalActivePower', 'GlobalReactivePower', 'Voltage', 'GlobalIntensity', 'SubMetering1', 'SubMetering2', 'SubMetering3')
rawData$DateTime <- strptime(paste(rawData$Date, rawData$Time), format = '%d/%m/%Y %H:%M:%S')
```

Making Plots
-------------

>Our overall goal here is simply to examine how household energy usage varies over a 2-day period in February, 2007. Your task is to reconstruct the plots that can be found [here](https://github.com/rdpeng/ExData_Plotting1), all of which were constructed using the base plotting system.

>For each plot you should:
-   Construct the plot and save it to a PNG file with a width of 480 pixels and a height of 480 pixels.
-   Name each of the plot files as plot1.png, plot2.png, etc.
-   Create a separate R code file (plot1.R, plot2.R, etc.) that constructs the corresponding plot, i.e. code in plot1.R constructs the plot1.png plot. Your code file should include code for reading the data so that the plot can be fully reproduced. You should also include the code that creates the PNG file.
-   Add the PNG file and R code file to your git repository

# Plot 1
```R
#png('plot1.png', width = 480, height = 480)
hist(rawData$GlobalActivePower, col = 'red',
     main = 'Global Active Power',
     xlab = 'Global Active Power (kilowatts)')
```
![Alt text](https://github.com/rdpeng/ExData_Plotting1/blob/master/figure/unnamed-chunk-2.png?raw=true "Plot1")

```R
#dev.off()
```

# Plot 2
```R
#png('plot2.png', width = 480, height = 480)
plot(x = rawData$DateTime, y = rawData$GlobalActivePower, 
     type = 'l', xlab = NA, ylab = 'Global Active Power (kilowatts)')
```
![Alt text](https://github.com/rdpeng/ExData_Plotting1/raw/master/figure/unnamed-chunk-3.png "Plot2")

```R
#dev.off()
```

# Plot 3
```R
#png('plot3.png', width = 480, height = 480)
plot(x = rawData$DateTime, y = rawData$SubMetering1, type = 'l',
     xlab = NA, ylab = 'Energy sub metering')
lines(x = rawData$DateTime, y = rawData$SubMetering2, col = 'red')
lines(x = rawData$DateTime, y = rawData$SubMetering3, col = 'blue')
legend('topright', 
       legend = c('Sub_metering_1', 'Sub_metering_2', 'Sub_metering_3'),
       col = c('black', 'red', 'blue'),
       lwd = 1)
```
![Alt text](https://github.com/rdpeng/ExData_Plotting1/raw/master/figure/unnamed-chunk-4.png "Plot3")

```R
#dev.off()
```

# Plot 4
```R
#png('plot4.png', width = 480, height = 480)
par(mfrow = c(2, 2)) 
  #plots from left to right, top to bottom (since you used mfrow vs mfcol)

#plot 4a = plot 1
plot(x = rawData$DateTime, y = rawData$GlobalActivePower, 
     type = 'l', xlab = NA, ylab = 'Global Active Power')

#plot 4b
plot(x = rawData$DateTime, y = rawData$Voltage, 
     type = 'l', xlab = 'datetime', ylab = 'Voltage')

#plot 4c = plot 3
plot(x = rawData$DateTime, y = rawData$SubMetering1, type = 'l',
     xlab = NA, ylab = 'Energy sub metering')
lines(x = rawData$DateTime, y = rawData$SubMetering2, col = 'red')
lines(x = rawData$DateTime, y = rawData$SubMetering3, col = 'blue')
legend('topright', 
       legend = c('Sub_metering_1', 'Sub_metering_2', 'Sub_metering_3'),
       col = c('black', 'red', 'blue'),
       lwd = 1, bty = 'n')

#plot 4d
plot(x = rawData$DateTime, y = rawData$GlobalReactivePower, type = 'l',
     xlab = 'datetime', ylab = 'Global_reactive_power')
```
![Alt text](https://github.com/rdpeng/ExData_Plotting1/raw/master/figure/unnamed-chunk-5.png "Plot3") 

```R
#dev.off()
``` 