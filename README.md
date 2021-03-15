# module-9-visualizing-R
# First you need to install these packages
install.packages("lattice")
install.packages("ggplot2")
library(lattice)
library(ggplot2)

# Use the https://vincentarelbundock.github.io/Rdatasets/datasets.html link to get a dataset, below is the Cardiac Data for Domestic dogs which is the one I used
# https://vincentarelbundock.github.io/Rdatasets/csv/boot/dogs.csv
data_from_file <- read.table(file.choose(),header=T,sep=",")[,2:3]

# Plot the data via the built-in boxplot() function
boxplot((lvp*100)~mvo,data_from_file, main="Cardiac Data for Domestic Dogs", xlab="mvo", ylab="Percent lvp", las=1, col=rainbow(6))

# Use the lattice package's bwplot() function to plot the data
bwplot((lvp*100)~mvo, data=data_from_file, horizontal=FALSE, main="lvp Rate", xlab="mvo", ylab="Percent lvp", las=1, par.settings = list(box.rectangle = list(fill=rainbow(6))))

# Plotting data through ggplot2

# Here I needed to take the Time data and get it converted to factors
data_for_gg <- data_from_file
data_for_gg$mvo <- as.factor(data_for_gg$mvo)

# Take the data and plot it as a geom_boxplot()
ggplot(data_for_gg, aes(x=mvo, y=lvp*100, fill=mvo)) + geom_boxplot() + labs(title="Cardiac Data for Domestic Dogs", x="mvo", y="Percent lvp") + theme_classic()
