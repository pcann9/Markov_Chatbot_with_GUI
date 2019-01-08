# Chatbot Data Prep in R
```R
#import packages
library(jsonlite)

# import data
f <- file('comments.json')
data <- stream_in(f)
data_backup <- data


### text cleaning ###

# keep columns that you want
cols_to_keep <- c('text')
data <- subset(data, select = cols_to_keep) 

# lower case
data$text <- tolower(data$text)

# filter out "http|https|www." links
data$text <- gsub('(http|https|www\\.)[^([:blank:]|\\"|<|\n\r)]+\\w', " ", data$text)

# url that starts with domain name "reddit.com" 
data$text <- gsub('[[:alnum:]_-]+(\\.com)[^([:blank:]|\\"|<|\n\r)]*', " ", data$text)

# remove control characters
data$text <- gsub('[[:cntrl:]]', ' ', data$text)

# replace excessive spaces and tabs with juts one space
data$text <- gsub('\\s+', ' ', data$text)

# contains any characters
data$has_char <- grepl('[[:alpha:]]', data$text)
data <- data[data$has_char == TRUE, ]

# keep the cols that you want
data <- subset(data, select = cols_to_keep) 

# export data
write.csv(x = data, file = "clean_data.txt", row.names = FALSE, col.names = FALSE, quote = FALSE, sep = '\n', fileEncoding = "UTF-8")
```
