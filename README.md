# Wand-Sales-Graph-DDS

##bonus
install.packages("dygraphs")
library(dygraphs)
library(tidyverse)
Gregor <- read.csv(file = "~/MSDS_6306_Doing-Data-Science/Unit 11/Unit11TimeSeries_Gregorovitch.csv", header = FALSE)
colnames(Gregor) <- c("Date","WandsSold")
Gregor <- Gregor %>% mutate(Date = mdy(Date))
str(Gregor)

Olliv <- read.csv(file = "~/MSDS_6306_Doing-Data-Science/Unit 11/Unit11TimeSeries_Ollivander.csv", header = FALSE)
colnames(Olliv) <- c("Date","WandsSold")
Olliv <- Olliv %>% mutate(Date = mdy(Date))
str(Olliv)

gregorts <- xts(Gregor$WandsSold, order.by = Gregor$Date)
ollivts <- xts(Olliv$WandsSold, order.by = Olliv$Date)
str(combinedts)

combinedts <- merge(gregorts,ollivts)
dygraph(combinedts, main = "Wands Sold Over Time", xlab = "Year", ylab = "Wands Sold") %>% 
  dySeries("ollivts", label = "Ollivander", color = "gold") %>%
  dySeries("gregorts", label = "Gregorovitch", color = "red") %>%
  dyOptions(stackedGraph = TRUE) %>%
  dyRangeSelector() %>%
  dyShading(from = "1995-01-01", to = "1999-12-31", color = "darkgreen") %>%
  dyHighlight()
