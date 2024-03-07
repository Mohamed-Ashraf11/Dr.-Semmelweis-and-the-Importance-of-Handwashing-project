# reading and viewing data

yearly = read.csv("yearly_deaths_by_clinic.csv", sep = ",", header =  TRUE)
View(yearly)
monthly = read.csv("monthly_deaths.csv", sep = ",", header = TRUE)
View(monthly)

#adding proportion columns

library(dplyr)
yearly  = yearly %>%
  mutate(proportion_deaths = deaths/births)

monthly = monthly %>%
  mutate(proportion_deaths = deaths / births)

#plotting the data

# for years

library(ggplot2)
ggplot(yearly, aes(x= year , y= proportion_deaths, color = clinic )) + geom_line()

#for months

ggplot(monthly, aes(x= as.Date(date) , y= proportion_deaths, group = 1)) + geom_line(color = "red") + 
  labs( x= "Date", y = "Proportion Deaths") + 
  scale_x_date(date_labels = "%Y-%m", date_breaks = "6 month")

#adding a threshold

handwashing_start = as.Date("1847-06-01")
monthly = monthly %>%
  mutate(handwashing_started = date >= handwashing_start)
monthly

ggplot(monthly, aes(x= as.Date(date) , y= proportion_deaths, group = 1, color = handwashing_started)) + geom_line() + 
  labs( x= "Date", y = "Proportion Deaths") + 
  scale_x_date(date_labels = "%Y-%m", date_breaks = "6 month")

#calculating summary 

monthly_summary = monthly %>%
  group_by(handwashing_started) %>%
  summarise(mean_proportion_deaths = mean(proportion_deaths))
monthly_summary  
