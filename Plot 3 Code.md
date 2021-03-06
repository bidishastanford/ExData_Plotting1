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
###Data cleaning
```
electric$DateTime<-paste(electric$Date, electric$Time)
View(electric)
```
###Lets change the Date Time to yyyy-mm-dd hh:mm:ss
```
electric$DateTime<-strptime(electric$DateTime, "%d/%m/%Y %H:%M:%S")
```
###Subsetting the dates of our interest
```
start<-which(electric$DateTime==strptime("2007-02-01", "%Y-%m-%d"))
end<-which(electric$DateTime==strptime("2007-02-02 23:59:00", "%Y-%m-%d %H:%M:%S"))
electric_sub<-electric[start:end,]
View(electric_sub)
```
###Making the data workable
```
class(electric_sub$Global_active_power)
electric_sub$Global_active_power<-as.numeric(as.character(electric_sub$Global_active_power))
electric_sub$Sub_metering_1<-as.numeric(as.character(electric_sub$Sub_metering_1))
electric_sub$Sub_metering_2<-as.numeric(as.character(electric_sub$Sub_metering_2))
electric_sub$Sub_metering_3<-as.numeric(as.character(electric_sub$Sub_metering_3))
```
###Plotting
```
with(electric_sub,plot(DateTime,Sub_metering_1,type="l",col="black",xlab="",ylab="Energy sub metering"))
with(electric_sub,lines(DateTime,Sub_metering_2,col="red"))
with(electric_sub,lines(DateTime,Sub_metering_3,col="blue"))
legend('topright',c("Sub_metering_1","Sub_metering_2","Sub_metering_3"),lty=c(1,1,1),col=c("black","red","blue"))
```
###Copy the plot to PNG
```
dev.copy(png,file="Plot3.png")
dev.off()
```
