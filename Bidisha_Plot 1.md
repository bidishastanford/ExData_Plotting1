### Setting the directory
```require(foreign)
getwd()
setwd("/Users/Liza/Box/Coursera")
```
###Loading the data
```
electric<-read.table("household_power_consumption.txt",header=T, sep=";")
```
###Checking the data
```
head(electric)
View(electric)
names(electric)
```
####Data cleaning
```
electric$DateTime<-paste(electric$Date, electric$Time)
View(electric)
```
###Lets change the Date Time to yyyy-mm-dd hh:mm:ss
```
electric$DateTime<-strptime(electric$DateTime, "%d/%m/%Y %H:%M:%S")
```
####Subsetting the dates of our interest
```
start<-which(electric$DateTime==strptime("2007-02-01", "%Y-%m-%d"))
end<-which(electric$DateTime==strptime("2007-02-02 23:59:00", "%Y-%m-%d %H:%M:%S"))
electric_sub<-electric[start:end,]
View(electric_sub)
```
####Making the data workable
```
class(electric_sub$Global_active_power)
electric_sub$Global_active_power<-as.numeric(as.character(electric_sub$Global_active_power))
```
###Plot 1
```{r}
hist(electric_sub$Global_active_power,col="red",xlab="Global Active Power (kilowatts)",main="Global Active Power")
```
###Copy the plot onto PNG
```
dev.copy(png,file="Plot1.png")
dev.off()
```
