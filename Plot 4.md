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
head(electric_sub)
with(electric_sub,plot(DateTime,Sub_metering_1,type="l",col="black",xlab="",ylab="Energy sub metering"))
```

##Plot 4
```
par(mfrow=c(2,2))
plot(electric_sub$DateTime,electric_sub$Global_active_power,ylab="Global Active Power (kilowatts)",xlab="",type="l")
with(electric_sub,plot(DateTime,as.numeric(as.character(Voltage)),xlab="datetime",ylab="Volatage",type="l",lwd=2))
with(electric_sub,plot(DateTime,Sub_metering_1,type="l",col="black",xlab="",ylab="Energy sub metering"))
lines(electric_sub$DateTime,electric_sub$Sub_metering_2,col="red")
lines(electric_sub$DateTime,electric_sub$Sub_metering_3,col="blue")
legend('topright',c("Sub_metering_1","Sub_metering_2","Sub_metering_3"),lty=c(1,1,1),col=c("black","red","blue"))
with(electric_sub,plot(DateTime,as.numeric(as.character(Global_reactive_power)),xlab="datetime",ylab="Global_reactive_power",type="l",lwd=1))
```
###Copying plot 4 into Png
```
dev.copy(png,file="Plot4.png")
dev.off()
```
