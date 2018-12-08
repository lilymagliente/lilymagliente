# lilymagliente
######### Load libraries / packages
library(rvest)
library(data.table)
library(dplyr)
library(caret)

######### Set working directory
setwd("~/Fall 2018/STAT184")

######### Webscrape data tables of each National Basketball Association team from ESPN 

######### CELTICS 
celtics_roster_url <-"http://www.espn.com/nba/team/roster/_/name/bos/boston-celtics"

Celtics <- celtics_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Celtics_roster<-Celtics[[2]][-1,] #look at all tables, pull the third table, then remove the first row
header<-Celtics_roster[1,] #want this part, the header
Celtics_roster<-data.table(Celtics_roster[-1,]) #dropping the names 
setnames(Celtics_roster,names(Celtics_roster),as.character(unlist(header[1,])))
Celtics_roster<-Celtics_roster[,1:8]
Celtics_roster <- mutate(Celtics_roster, Team = rep.int("Celtics",16)) #was 17 before

celtics_stats_url <- "http://www.espn.com/nba/team/stats/_/name/bos/boston-celtics"
Celtics <- celtics_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Celtics_game_stats<-Celtics[[1]][-1,] 
header<-Celtics_game_stats[1,] 
Celtics_game_stats<-data.table(Celtics_game_stats[-1,])  
setnames(Celtics_game_stats,names(Celtics_game_stats),as.character(unlist(header[1,])))
Celtics_game_stats <- mutate(Celtics_game_stats, Team = rep.int("Celtics",16)) #was 15
Celtics_game_stats<- Celtics_game_stats[-nrow(Celtics_game_stats),]

Celtics_shooting_stats<-Celtics[[2]][-1,] 
header<-Celtics_shooting_stats[1,] 
Celtics_shooting_stats<-data.table(Celtics_shooting_stats[-1,])  
setnames(Celtics_shooting_stats,names(Celtics_shooting_stats),as.character(unlist(header[1,])))
Celtics_shooting_stats <- mutate(Celtics_shooting_stats, Team = rep.int("Celtics",16))
Celtics_shooting_stats <-Celtics_shooting_stats[-nrow(Celtics_shooting_stats),]


######### Hawks
Hawks_roster_url <- "http://www.espn.com/nba/team/roster/_/name/atl/atlanta-hawks"

Hawks <- Hawks_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Hawks_roster<-Hawks[[2]][-1,] #look at all tables, pull the third table, then remove the first row
header<-Hawks_roster[1,] #want this part, the header
Hawks_roster<-data.table(Hawks_roster[-1,]) #dropping the names 
setnames(Hawks_roster,names(Hawks_roster),as.character(unlist(header[1,])))
Hawks_roster<-Hawks_roster[,1:8]
Hawks_roster <- mutate(Hawks_roster, Team = rep.int("Hawks",17))

Hawks_stats_url <- "http://www.espn.com/nba/team/stats/_/name/atl/atlanta-hawks"

Hawks <- Hawks_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Hawks_game_stats<-Hawks[[1]][-1,] 
header<-Hawks_game_stats[1,] 
Hawks_game_stats<-data.table(Hawks_game_stats[-1,])  
setnames(Hawks_game_stats,names(Hawks_game_stats),as.character(unlist(header[1,])))
Hawks_game_stats <- mutate(Hawks_game_stats, Team = rep.int("Hawks",18))
Hawks_game_stats<- Hawks_game_stats[-nrow(Hawks_game_stats),]


Hawks_shooting_stats<-Hawks[[2]][-1,] 
header<-Hawks_shooting_stats[1,] 
Hawks_shooting_stats<-data.table(Hawks_shooting_stats[-1,])  
setnames(Hawks_shooting_stats,names(Hawks_shooting_stats),as.character(unlist(header[1,])))
Hawks_shooting_stats <- mutate(Hawks_shooting_stats, Team = rep.int("Hawks",18))
Hawks_shooting_stats<-Hawks_shooting_stats[-nrow(Hawks_shooting_stats),]


######### NETS
Nets_roster_url <- "http://www.espn.com/nba/team/roster/_/name/bkn/brooklyn-nets"

Nets <- Nets_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Nets_roster<-Nets[[2]][-1,]
header<-Nets_roster[1,] 
Nets_roster<-data.table(Nets_roster[-1,]) 
setnames(Nets_roster,names(Nets_roster),as.character(unlist(header[1,])))
Nets_roster<-Nets_roster[,1:8]
Nets_roster <- mutate(Nets_roster, Team = rep.int("Nets",17))

Nets_stats_url <-"http://www.espn.com/nba/team/stats/_/name/bkn/brooklyn-nets"

Nets <- Nets_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Nets_game_stats<-Nets[[1]][-1,] 
header<-Nets_game_stats[1,] 
Nets_game_stats<-data.table(Nets_game_stats[-1,])  
setnames(Nets_game_stats,names(Nets_game_stats),as.character(unlist(header[1,])))
Nets_game_stats <- mutate(Nets_game_stats, Team = rep.int("Nets",17))
Nets_game_stats<- Nets_game_stats[-nrow(Nets_game_stats),]

Nets_shooting_stats<-Nets[[2]][-1,] 
header<-Nets_shooting_stats[1,] 
Nets_shooting_stats<-data.table(Nets_shooting_stats[-1,])  
setnames(Nets_shooting_stats,names(Nets_shooting_stats),as.character(unlist(header[1,])))
Nets_shooting_stats <- mutate(Nets_shooting_stats, Team = rep.int("Nets",17))
Nets_shooting_stats<-Nets_shooting_stats[-nrow(Nets_shooting_stats),]

######### Hornets
Hornets_roster_url <- "http://www.espn.com/nba/team/roster/_/name/cha/charlotte-hornets"

Hornets <- Hornets_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Hornets_roster<-Hornets[[2]][-1,]
header<-Hornets_roster[1,] 
Hornets_roster<-data.table(Hornets_roster[-1,]) 
setnames(Hornets_roster,names(Hornets_roster),as.character(unlist(header[1,])))
Hornets_roster<-Hornets_roster[,1:8]
Hornets_roster <- mutate(Hornets_roster, Team = rep.int("Hornets",16))

Hornets_stats_url <-"http://www.espn.com/nba/team/stats/_/name/cha/charlotte-hornets"

Hornets <- Hornets_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Hornets_game_stats<-Hornets[[1]][-1,] 
header<-Hornets_game_stats[1,] 
Hornets_game_stats<-data.table(Hornets_game_stats[-1,])  
setnames(Hornets_game_stats,names(Hornets_game_stats),as.character(unlist(header[1,])))
Hornets_game_stats <- mutate(Hornets_game_stats, Team = rep.int("Hornets",15))
Hornets_game_stats<- Hornets_game_stats[-nrow(Hornets_game_stats),]

Hornets_shooting_stats<-Hornets[[2]][-1,] 
header<-Hornets_shooting_stats[1,] 
Hornets_shooting_stats<-data.table(Hornets_shooting_stats[-1,])  
setnames(Hornets_shooting_stats,names(Hornets_shooting_stats),as.character(unlist(header[1,])))
Hornets_shooting_stats <- mutate(Hornets_shooting_stats, Team = rep.int("Hornets",15))
Hornets_shooting_stats<-Hornets_shooting_stats[-nrow(Hornets_shooting_stats),]

######### BULLS

Bulls_roster_url <- "http://www.espn.com/nba/team/roster/_/name/chi/chicago-bulls"

Bulls <- Bulls_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Bulls_roster<-Bulls[[2]][-1,]
header<-Bulls_roster[1,] 
Bulls_roster<-data.table(Bulls_roster[-1,]) 
setnames(Bulls_roster,names(Bulls_roster),as.character(unlist(header[1,])))
Bulls_roster<-Bulls_roster[,1:8]
Bulls_roster <- mutate(Bulls_roster, Team = rep.int("Bulls",17))

Bulls_stats_url <-"http://www.espn.com/nba/team/stats/_/name/chi/chicago-bulls"

Bulls <- Bulls_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Bulls_game_stats<-Bulls[[1]][-1,] 
header<-Bulls_game_stats[1,] 
Bulls_game_stats<-data.table(Bulls_game_stats[-1,])  
setnames(Bulls_game_stats,names(Bulls_game_stats),as.character(unlist(header[1,])))
Bulls_game_stats <- mutate(Bulls_game_stats, Team = rep.int("Bulls",16))
Bulls_game_stats<- Bulls_game_stats[-nrow(Bulls_game_stats),]

Bulls_shooting_stats<-Bulls[[2]][-1,] 
header<-Bulls_shooting_stats[1,] 
Bulls_shooting_stats<-data.table(Bulls_shooting_stats[-1,])  
setnames(Bulls_shooting_stats,names(Bulls_shooting_stats),as.character(unlist(header[1,])))
Bulls_shooting_stats <- mutate(Bulls_shooting_stats, Team = rep.int("Bulls",16))
Bulls_shooting_stats<-Bulls_shooting_stats[-nrow(Bulls_shooting_stats),]


######### Cavaliers
Cavaliers_roster_url <- "http://www.espn.com/nba/team/roster/_/name/cle/cleveland-cavaliers"

Cavaliers <- Cavaliers_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Cavaliers_roster<-Cavaliers[[2]][-1,]
header<-Cavaliers_roster[1,] 
Cavaliers_roster<-data.table(Cavaliers_roster[-1,]) 
setnames(Cavaliers_roster,names(Cavaliers_roster),as.character(unlist(header[1,])))
Cavaliers_roster<-Cavaliers_roster[,1:8]
Cavaliers_roster <- mutate(Cavaliers_roster, Team = rep.int("Cavaliers",16))

Cavaliers_stats_url <-"http://www.espn.com/nba/team/stats/_/name/cle/cleveland-cavaliers"

Cavaliers <- Cavaliers_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Cavaliers_game_stats<-Cavaliers[[1]][-1,] 
header<-Cavaliers_game_stats[1,] 
Cavaliers_game_stats<-data.table(Cavaliers_game_stats[-1,])  
setnames(Cavaliers_game_stats,names(Cavaliers_game_stats),as.character(unlist(header[1,])))
Cavaliers_game_stats <- mutate(Cavaliers_game_stats, Team = rep.int("Cavaliers",20))
Cavaliers_game_stats<- Cavaliers_game_stats[-nrow(Cavaliers_game_stats),]

Cavaliers_shooting_stats<-Cavaliers[[2]][-1,] 
header<-Cavaliers_shooting_stats[1,] 
Cavaliers_shooting_stats<-data.table(Cavaliers_shooting_stats[-1,])  
setnames(Cavaliers_shooting_stats,names(Cavaliers_shooting_stats),as.character(unlist(header[1,])))
Cavaliers_shooting_stats <- mutate(Cavaliers_shooting_stats, Team = rep.int("Cavaliers",20))
Cavaliers_shooting_stats<-Cavaliers_shooting_stats[-nrow(Cavaliers_shooting_stats),]

######### Mavericks
Mavericks_roster_url <- "http://www.espn.com/nba/team/roster/_/name/dal/dallas-mavericks"

Mavericks <- Mavericks_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Mavericks_roster<-Mavericks[[2]][-1,]
header<-Mavericks_roster[1,] 
Mavericks_roster<-data.table(Mavericks_roster[-1,]) 
setnames(Mavericks_roster,names(Mavericks_roster),as.character(unlist(header[1,])))
Mavericks_roster<-Mavericks_roster[,1:8]
Mavericks_roster <- mutate(Mavericks_roster, Team = rep.int("Mavericks",17))

Mavericks_stats_url <-"http://www.espn.com/nba/team/stats/_/name/dal/dallas-mavericks"

Mavericks <- Mavericks_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Mavericks_game_stats<-Mavericks[[1]][-1,] 
header<-Mavericks_game_stats[1,] 
Mavericks_game_stats<-data.table(Mavericks_game_stats[-1,])  
setnames(Mavericks_game_stats,names(Mavericks_game_stats),as.character(unlist(header[1,])))
Mavericks_game_stats <- mutate(Mavericks_game_stats, Team = rep.int("Mavericks",16))
Mavericks_game_stats<- Mavericks_game_stats[-nrow(Mavericks_game_stats),]

Mavericks_shooting_stats<-Mavericks[[2]][-1,] 
header<-Mavericks_shooting_stats[1,] 
Mavericks_shooting_stats<-data.table(Mavericks_shooting_stats[-1,])  
setnames(Mavericks_shooting_stats,names(Mavericks_shooting_stats),as.character(unlist(header[1,])))
Mavericks_shooting_stats <- mutate(Mavericks_shooting_stats, Team = rep.int("Mavericks",16))
Mavericks_shooting_stats<-Mavericks_shooting_stats[-nrow(Mavericks_shooting_stats),]



######### NUGGETS
Nuggets_roster_url <- "http://www.espn.com/nba/team/roster/_/name/den/denver-nuggets"

Nuggets <- Nuggets_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Nuggets_roster<-Nuggets[[2]][-1,]
header<-Nuggets_roster[1,] 
Nuggets_roster<-data.table(Nuggets_roster[-1,]) 
setnames(Nuggets_roster,names(Nuggets_roster),as.character(unlist(header[1,])))
Nuggets_roster<-Nuggets_roster[,1:8]
Nuggets_roster <- mutate(Nuggets_roster, Team = rep.int("Nuggets",18))

Nuggets_stats_url <-"http://www.espn.com/nba/team/stats/_/name/den"

Nuggets <- Nuggets_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Nuggets_game_stats<-Nuggets[[1]][-1,] 
header<-Nuggets_game_stats[1,] 
Nuggets_game_stats<-data.table(Nuggets_game_stats[-1,])  
setnames(Nuggets_game_stats,names(Nuggets_game_stats),as.character(unlist(header[1,])))
Nuggets_game_stats <- mutate(Nuggets_game_stats, Team = rep.int("Nuggets",15))
Nuggets_game_stats<- Nuggets_game_stats[-nrow(Nuggets_game_stats),]

Nuggets_shooting_stats<-Nuggets[[2]][-1,] 
header<-Nuggets_shooting_stats[1,] 
Nuggets_shooting_stats<-data.table(Nuggets_shooting_stats[-1,])  
setnames(Nuggets_shooting_stats,names(Nuggets_shooting_stats),as.character(unlist(header[1,])))
Nuggets_shooting_stats <- mutate(Nuggets_shooting_stats, Team = rep.int("Nuggets",15))
Nuggets_shooting_stats<-Nuggets_shooting_stats[-nrow(Nuggets_shooting_stats),]

######### Pistons
Pistons_roster_url <- "http://www.espn.com/nba/team/roster/_/name/det/detroit-pistons"

Pistons <- Pistons_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Pistons_roster<-Pistons[[2]][-1,]
header<-Pistons_roster[1,] 
Pistons_roster<-data.table(Pistons_roster[-1,]) 
setnames(Pistons_roster,names(Pistons_roster),as.character(unlist(header[1,])))
Pistons_roster<-Pistons_roster[,1:8]
Pistons_roster <- mutate(Pistons_roster, Team = rep.int("Pistons",17))

Pistons_stats_url <-"http://www.espn.com/nba/team/stats/_/name/det/detroit-pistons"

Pistons <- Pistons_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Pistons_game_stats<-Pistons[[1]][-1,] 
header<-Pistons_game_stats[1,] 
Pistons_game_stats<-data.table(Pistons_game_stats[-1,])  
setnames(Pistons_game_stats,names(Pistons_game_stats),as.character(unlist(header[1,])))
Pistons_game_stats <- mutate(Pistons_game_stats, Team = rep.int("Pistons",17))
Pistons_game_stats<- Pistons_game_stats[-nrow(Pistons_game_stats),]

Pistons_shooting_stats<-Pistons[[2]][-1,] 
header<-Pistons_shooting_stats[1,] 
Pistons_shooting_stats<-data.table(Pistons_shooting_stats[-1,])  
setnames(Pistons_shooting_stats,names(Pistons_shooting_stats),as.character(unlist(header[1,])))
Pistons_shooting_stats <- mutate(Pistons_shooting_stats, Team = rep.int("Pistons",17))
Pistons_shooting_stats<-Pistons_shooting_stats[-nrow(Pistons_shooting_stats),]


######### WARRIORS
Warriors_roster_url <- "http://www.espn.com/nba/team/roster/_/name/gs/golden-state-warriors"

Warriors <- Warriors_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Warriors_roster<-Warriors[[2]][-1,]
header<-Warriors_roster[1,] 
Warriors_roster<-data.table(Warriors_roster[-1,]) 
setnames(Warriors_roster,names(Warriors_roster),as.character(unlist(header[1,])))
Warriors_roster<-Warriors_roster[,1:8]
Warriors_roster <- mutate(Warriors_roster, Team = rep.int("Warriors",16))

Warriors_stats_url <-"http://www.espn.com/nba/team/stats/_/name/gs/golden-state-warriors"

Warriors <- Warriors_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Warriors_game_stats<-Warriors[[1]][-1,] 
header<-Warriors_game_stats[1,] 
Warriors_game_stats<-data.table(Warriors_game_stats[-1,])  
setnames(Warriors_game_stats,names(Warriors_game_stats),as.character(unlist(header[1,])))
Warriors_game_stats <- mutate(Warriors_game_stats, Team = rep.int("Warriors",16))
Warriors_game_stats<- Warriors_game_stats[-nrow(Warriors_game_stats),]

Warriors_shooting_stats<-Warriors[[2]][-1,] 
header<-Warriors_shooting_stats[1,] 
Warriors_shooting_stats<-data.table(Warriors_shooting_stats[-1,])  
setnames(Warriors_shooting_stats,names(Warriors_shooting_stats),as.character(unlist(header[1,])))
Warriors_shooting_stats <- mutate(Warriors_shooting_stats, Team = rep.int("Warriors",16))
Warriors_shooting_stats<-Warriors_shooting_stats[-nrow(Warriors_shooting_stats),]


######### ROCKETS
Rockets_roster_url <- "http://www.espn.com/nba/team/roster/_/name/hou/houston-rockets"

Rockets <- Rockets_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Rockets_roster<-Rockets[[2]][-1,]
header<-Rockets_roster[1,] 
Rockets_roster<-data.table(Rockets_roster[-1,]) 
setnames(Rockets_roster,names(Rockets_roster),as.character(unlist(header[1,])))
Rockets_roster<-Rockets_roster[,1:8]
Rockets_roster <- mutate(Rockets_roster, Team = rep.int("Rockets",16))

Rockets_stats_url <-"http://www.espn.com/nba/team/stats/_/name/hou/houston-rockets"

Rockets <- Rockets_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Rockets_game_stats<-Rockets[[1]][-1,] 
header<-Rockets_game_stats[1,] 
Rockets_game_stats<-data.table(Rockets_game_stats[-1,])  
setnames(Rockets_game_stats,names(Rockets_game_stats),as.character(unlist(header[1,])))
Rockets_game_stats <- mutate(Rockets_game_stats, Team = rep.int("Rockets",17))
Rockets_game_stats<- Rockets_game_stats[-nrow(Rockets_game_stats),]

Rockets_shooting_stats<-Rockets[[2]][-1,] 
header<-Rockets_shooting_stats[1,] 
Rockets_shooting_stats<-data.table(Rockets_shooting_stats[-1,])  
setnames(Rockets_shooting_stats,names(Rockets_shooting_stats),as.character(unlist(header[1,])))
Rockets_shooting_stats <- mutate(Rockets_shooting_stats, Team = rep.int("Rockets",17))
Rockets_shooting_stats<-Rockets_shooting_stats[-nrow(Rockets_shooting_stats),]


######### PACERS
Pacers_roster_url <- "http://www.espn.com/nba/team/roster/_/name/ind/indiana-pacers"

Pacers <- Pacers_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Pacers_roster<-Pacers[[2]][-1,]
header<-Pacers_roster[1,] 
Pacers_roster<-data.table(Pacers_roster[-1,]) 
setnames(Pacers_roster,names(Pacers_roster),as.character(unlist(header[1,])))
Pacers_roster<-Pacers_roster[,1:8]
Pacers_roster <- mutate(Pacers_roster, Team = rep.int("Pacers",16))

Pacers_stats_url <-"http://www.espn.com/nba/team/stats/_/name/ind"

Pacers <- Pacers_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Pacers_game_stats<-Pacers[[1]][-1,] 
header<-Pacers_game_stats[1,] 
Pacers_game_stats<-data.table(Pacers_game_stats[-1,])  
setnames(Pacers_game_stats,names(Pacers_game_stats),as.character(unlist(header[1,])))
Pacers_game_stats <- mutate(Pacers_game_stats, Team = rep.int("Pacers",17))
Pacers_game_stats<- Pacers_game_stats[-nrow(Pacers_game_stats),]

Pacers_shooting_stats<-Pacers[[2]][-1,] 
header<-Pacers_shooting_stats[1,] 
Pacers_shooting_stats<-data.table(Pacers_shooting_stats[-1,])  
setnames(Pacers_shooting_stats,names(Pacers_shooting_stats),as.character(unlist(header[1,])))
Pacers_shooting_stats <- mutate(Pacers_shooting_stats, Team = rep.int("Pacers",17))
Pacers_shooting_stats<-Pacers_shooting_stats[-nrow(Pacers_shooting_stats),]


######### CLIPPERS
Clippers_roster_url <- "http://www.espn.com/nba/team/roster/_/name/lac/la-clippers"

Clippers <- Clippers_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Clippers_roster<-Clippers[[2]][-1,]
header<-Clippers_roster[1,] 
Clippers_roster<-data.table(Clippers_roster[-1,]) 
setnames(Clippers_roster,names(Clippers_roster),as.character(unlist(header[1,])))
Clippers_roster<-Clippers_roster[,1:8]
Clippers_roster <- mutate(Clippers_roster, Team = rep.int("Clippers",17))

Clippers_stats_url <-"http://www.espn.com/nba/team/stats/_/name/lac/la-clippers"

Clippers <- Clippers_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Clippers_game_stats<-Clippers[[1]][-1,] 
header<-Clippers_game_stats[1,] 
Clippers_game_stats<-data.table(Clippers_game_stats[-1,])  
setnames(Clippers_game_stats,names(Clippers_game_stats),as.character(unlist(header[1,])))
Clippers_game_stats <- mutate(Clippers_game_stats, Team = rep.int("Clippers",16))
Clippers_game_stats<- Clippers_game_stats[-nrow(Clippers_game_stats),]

Clippers_shooting_stats<-Clippers[[2]][-1,] 
header<-Clippers_shooting_stats[1,] 
Clippers_shooting_stats<-data.table(Clippers_shooting_stats[-1,])  
setnames(Clippers_shooting_stats,names(Clippers_shooting_stats),as.character(unlist(header[1,])))
Clippers_shooting_stats <- mutate(Clippers_shooting_stats, Team = rep.int("Clippers",16))
Clippers_shooting_stats<-Clippers_shooting_stats[-nrow(Clippers_shooting_stats),]


######### LAKERS
Lakers_roster_url <- "http://www.espn.com/nba/team/roster/_/name/lal/los-angeles-lakers"

Lakers <- Lakers_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Lakers_roster<-Lakers[[2]][-1,]
header<-Lakers_roster[1,] 
Lakers_roster<-data.table(Lakers_roster[-1,]) 
setnames(Lakers_roster,names(Lakers_roster),as.character(unlist(header[1,])))
Lakers_roster<-Lakers_roster[,1:8]
Lakers_roster <- mutate(Lakers_roster, Team = rep.int("Lakers",17))

Lakers_stats_url <-"http://www.espn.com/nba/team/stats/_/name/lal"

Lakers <- Lakers_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Lakers_game_stats<-Lakers[[1]][-1,] 
header<-Lakers_game_stats[1,] 
Lakers_game_stats<-data.table(Lakers_game_stats[-1,])  
setnames(Lakers_game_stats,names(Lakers_game_stats),as.character(unlist(header[1,])))
Lakers_game_stats <- mutate(Lakers_game_stats, Team = rep.int("Lakers",16))
Lakers_game_stats<- Lakers_game_stats[-nrow(Lakers_game_stats),]

Lakers_shooting_stats<-Lakers[[2]][-1,] 
header<-Lakers_shooting_stats[1,] 
Lakers_shooting_stats<-data.table(Lakers_shooting_stats[-1,])  
setnames(Lakers_shooting_stats,names(Lakers_shooting_stats),as.character(unlist(header[1,])))
Lakers_shooting_stats <- mutate(Lakers_shooting_stats, Team = rep.int("Lakers",16))
Lakers_shooting_stats<-Lakers_shooting_stats[-nrow(Lakers_shooting_stats),]


######### GRIZZLIES
Grizzlies_roster_url <- "http://www.espn.com/nba/team/roster/_/name/mem/memphis-grizzlies"

Grizzlies <- Grizzlies_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Grizzlies_roster<-Grizzlies[[2]][-1,]
header<-Grizzlies_roster[1,] 
Grizzlies_roster<-data.table(Grizzlies_roster[-1,]) 
setnames(Grizzlies_roster,names(Grizzlies_roster),as.character(unlist(header[1,])))
Grizzlies_roster<-Grizzlies_roster[,1:8]
Grizzlies_roster <- mutate(Grizzlies_roster, Team = rep.int("Grizzlies",17))

Grizzlies_stats_url <-"http://www.espn.com/nba/team/stats/_/name/mem/memphis-grizzlies"

Grizzlies <- Grizzlies_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Grizzlies_game_stats<-Grizzlies[[1]][-1,] 
header<-Grizzlies_game_stats[1,] 
Grizzlies_game_stats<-data.table(Grizzlies_game_stats[-1,])  
setnames(Grizzlies_game_stats,names(Grizzlies_game_stats),as.character(unlist(header[1,])))
Grizzlies_game_stats <- mutate(Grizzlies_game_stats, Team = rep.int("Grizzlies",17))
Grizzlies_game_stats<- Grizzlies_game_stats[-nrow(Grizzlies_game_stats),]

Grizzlies_shooting_stats<-Grizzlies[[2]][-1,] 
header<-Grizzlies_shooting_stats[1,] 
Grizzlies_shooting_stats<-data.table(Grizzlies_shooting_stats[-1,])  
setnames(Grizzlies_shooting_stats,names(Grizzlies_shooting_stats),as.character(unlist(header[1,])))
Grizzlies_shooting_stats <- mutate(Grizzlies_shooting_stats, Team = rep.int("Grizzlies",17))
Grizzlies_shooting_stats<-Grizzlies_shooting_stats[-nrow(Grizzlies_shooting_stats),]


######### HEAT
Heat_roster_url <- "http://www.espn.com/nba/team/roster/_/name/mia/miami-heat"

Heat <- Heat_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Heat_roster<-Heat[[2]][-1,]
header<-Heat_roster[1,] 
Heat_roster<-data.table(Heat_roster[-1,]) 
setnames(Heat_roster,names(Heat_roster),as.character(unlist(header[1,])))
Heat_roster<-Heat_roster[,1:8]
Heat_roster <- mutate(Heat_roster, Team = rep.int("Heat",16))

Heat_stats_url <-"http://www.espn.com/nba/team/stats/_/name/mia"

Heat <- Heat_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Heat_game_stats<-Heat[[1]][-1,] 
header<-Heat_game_stats[1,] 
Heat_game_stats<-data.table(Heat_game_stats[-1,])  
setnames(Heat_game_stats,names(Heat_game_stats),as.character(unlist(header[1,])))
Heat_game_stats <- mutate(Heat_game_stats, Team = rep.int("Heat",15))
Heat_game_stats<- Heat_game_stats[-nrow(Heat_game_stats),]

Heat_shooting_stats<-Heat[[2]][-1,] 
header<-Heat_shooting_stats[1,] 
Heat_shooting_stats<-data.table(Heat_shooting_stats[-1,])  
setnames(Heat_shooting_stats,names(Heat_shooting_stats),as.character(unlist(header[1,])))
Heat_shooting_stats <- mutate(Heat_shooting_stats, Team = rep.int("Heat",15))
Heat_shooting_stats<-Heat_shooting_stats[-nrow(Heat_shooting_stats),]


######### BUCKS
Bucks_roster_url <- "http://www.espn.com/nba/team/roster/_/name/mil/milwaukee-bucks"

Bucks <- Bucks_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Bucks_roster<-Bucks[[2]][-1,]
header<-Bucks_roster[1,] 
Bucks_roster<-data.table(Bucks_roster[-1,]) 
setnames(Bucks_roster,names(Bucks_roster),as.character(unlist(header[1,])))
Bucks_roster<-Bucks_roster[,1:8]
Bucks_roster <- mutate(Bucks_roster, Team = rep.int("Bucks",17))

Bucks_stats_url <-"http://www.espn.com/nba/team/stats/_/name/mil/milwaukee-bucks"

Bucks <- Bucks_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Bucks_game_stats<-Bucks[[1]][-1,] 
header<-Bucks_game_stats[1,] 
Bucks_game_stats<-data.table(Bucks_game_stats[-1,])  
setnames(Bucks_game_stats,names(Bucks_game_stats),as.character(unlist(header[1,])))
Bucks_game_stats <- mutate(Bucks_game_stats, Team = rep.int("Bucks",17))
Bucks_game_stats<- Bucks_game_stats[-nrow(Bucks_game_stats),]

Bucks_shooting_stats<-Bucks[[2]][-1,] 

header<-Bucks_shooting_stats[1,] 
Bucks_shooting_stats<-data.table(Bucks_shooting_stats[-1,])  
setnames(Bucks_shooting_stats,names(Bucks_shooting_stats),as.character(unlist(header[1,])))
Bucks_shooting_stats <- mutate(Bucks_shooting_stats, Team = rep.int("Bucks",17))
Bucks_shooting_stats<-Bucks_shooting_stats[-nrow(Bucks_shooting_stats),]


######### Timberwolves
Timberwolves_roster_url <- "http://www.espn.com/nba/team/roster/_/name/min/minnesota-timberwolves"

Timberwolves <- Timberwolves_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Timberwolves_roster<-Timberwolves[[2]][-1,]
header<-Timberwolves_roster[1,] 
Timberwolves_roster<-data.table(Timberwolves_roster[-1,]) 
setnames(Timberwolves_roster,names(Timberwolves_roster),as.character(unlist(header[1,])))
Timberwolves_roster<-Timberwolves_roster[,1:8]
Timberwolves_roster <- mutate(Timberwolves_roster, Team = rep.int("Timberwolves",17))

Timberwolves_stats_url <-"http://www.espn.com/nba/team/stats/_/name/min"

Timberwolves <- Timberwolves_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Timberwolves_game_stats<-Timberwolves[[1]][-1,] 
header<-Timberwolves_game_stats[1,] 
Timberwolves_game_stats<-data.table(Timberwolves_game_stats[-1,])  
setnames(Timberwolves_game_stats,names(Timberwolves_game_stats),as.character(unlist(header[1,])))
Timberwolves_game_stats <- mutate(Timberwolves_game_stats, Team = rep.int("Timberwolves",18))
Timberwolves_game_stats<- Timberwolves_game_stats[-nrow(Timberwolves_game_stats),]

Timberwolves_shooting_stats<-Timberwolves[[2]][-1,] 
header<-Timberwolves_shooting_stats[1,] 
Timberwolves_shooting_stats<-data.table(Timberwolves_shooting_stats[-1,])  
setnames(Timberwolves_shooting_stats,names(Timberwolves_shooting_stats),as.character(unlist(header[1,])))
Timberwolves_shooting_stats <- mutate(Timberwolves_shooting_stats, Team = rep.int("Timberwolves",18))
Timberwolves_shooting_stats<-Timberwolves_shooting_stats[-nrow(Timberwolves_shooting_stats),]


######### PELICANS
Pelicans_roster_url <- "http://www.espn.com/nba/team/roster/_/name/no/new-orleans-pelicans"

Pelicans <- Pelicans_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Pelicans_roster<-Pelicans[[2]][-1,]
header<-Pelicans_roster[1,] 
Pelicans_roster<-data.table(Pelicans_roster[-1,]) 
setnames(Pelicans_roster,names(Pelicans_roster),as.character(unlist(header[1,])))
Pelicans_roster<-Pelicans_roster[,1:8]
Pelicans_roster <- mutate(Pelicans_roster, Team = rep.int("Pelicans",17))

Pelicans_stats_url <-"http://www.espn.com/nba/team/stats/_/name/no/new-orleans-pelicans"

Pelicans <- Pelicans_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Pelicans_game_stats<-Pelicans[[1]][-1,] 
header<-Pelicans_game_stats[1,] 
Pelicans_game_stats<-data.table(Pelicans_game_stats[-1,])  
setnames(Pelicans_game_stats,names(Pelicans_game_stats),as.character(unlist(header[1,])))
Pelicans_game_stats <- mutate(Pelicans_game_stats, Team = rep.int("Pelicans",17))
Pelicans_game_stats<- Pelicans_game_stats[-nrow(Pelicans_game_stats),]

Pelicans_shooting_stats<-Pelicans[[2]][-1,] 
header<-Pelicans_shooting_stats[1,] 
Pelicans_shooting_stats<-data.table(Pelicans_shooting_stats[-1,])  
setnames(Pelicans_shooting_stats,names(Pelicans_shooting_stats),as.character(unlist(header[1,])))
Pelicans_shooting_stats <- mutate(Pelicans_shooting_stats, Team = rep.int("Pelicans",17))
Pelicans_shooting_stats<-Pelicans_shooting_stats[-nrow(Pelicans_shooting_stats),]

######### KNICKS
Knicks_roster_url <- "http://www.espn.com/nba/team/roster/_/name/ny/new-york-knicks"

Knicks <- Knicks_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Knicks_roster<-Knicks[[2]][-1,]
header<-Knicks_roster[1,] 
Knicks_roster<-data.table(Knicks_roster[-1,]) 
setnames(Knicks_roster,names(Knicks_roster),as.character(unlist(header[1,])))
Knicks_roster<-Knicks_roster[,1:8]
Knicks_roster <- mutate(Knicks_roster, Team = rep.int("Knicks",17))

Knicks_stats_url <-"http://www.espn.com/nba/team/stats/_/name/ny"

Knicks <- Knicks_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Knicks_game_stats<-Knicks[[1]][-1,] 
header<-Knicks_game_stats[1,] 
Knicks_game_stats<-data.table(Knicks_game_stats[-1,])  
setnames(Knicks_game_stats,names(Knicks_game_stats),as.character(unlist(header[1,])))
Knicks_game_stats <- mutate(Knicks_game_stats, Team = rep.int("Knicks",16))
Knicks_game_stats<- Knicks_game_stats[-nrow(Knicks_game_stats),]

Knicks_shooting_stats<-Knicks[[2]][-1,] 
header<-Knicks_shooting_stats[1,] 
Knicks_shooting_stats<-data.table(Knicks_shooting_stats[-1,])  
setnames(Knicks_shooting_stats,names(Knicks_shooting_stats),as.character(unlist(header[1,])))
Knicks_shooting_stats <- mutate(Knicks_shooting_stats, Team = rep.int("Knicks",16))
Knicks_shooting_stats<-Knicks_shooting_stats[-nrow(Knicks_shooting_stats),]

######### THUNDER
Thunder_roster_url <- "http://www.espn.com/nba/team/roster/_/name/okc/oklahoma-city-thunder"

Thunder <- Thunder_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Thunder_roster<-Thunder[[2]][-1,]
header<-Thunder_roster[1,] 
Thunder_roster<-data.table(Thunder_roster[-1,]) 
setnames(Thunder_roster,names(Thunder_roster),as.character(unlist(header[1,])))
Thunder_roster<-Thunder_roster[,1:8]
Thunder_roster <- mutate(Thunder_roster, Team = rep.int("Thunder",16))

Thunder_stats_url <-"http://www.espn.com/nba/team/stats/_/name/okc/oklahoma-city-thunder"

Thunder <- Thunder_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Thunder_game_stats<-Thunder[[1]][-1,] 
header<-Thunder_game_stats[1,] 
Thunder_game_stats<-data.table(Thunder_game_stats[-1,])  
setnames(Thunder_game_stats,names(Thunder_game_stats),as.character(unlist(header[1,])))
Thunder_game_stats <- mutate(Thunder_game_stats, Team = rep.int("Thunder",16))
Thunder_game_stats<- Thunder_game_stats[-nrow(Thunder_game_stats),]

Thunder_shooting_stats<-Thunder[[2]][-1,] 
header<-Thunder_shooting_stats[1,] 
Thunder_shooting_stats<-data.table(Thunder_shooting_stats[-1,])  
setnames(Thunder_shooting_stats,names(Thunder_shooting_stats),as.character(unlist(header[1,])))
Thunder_shooting_stats <- mutate(Thunder_shooting_stats, Team = rep.int("Thunder",16))
Thunder_shooting_stats<-Thunder_shooting_stats[-nrow(Thunder_shooting_stats),]

######### MAGIC
Magic_roster_url <- "http://www.espn.com/nba/team/roster/_/name/orl/orlando-magic"

Magic <- Magic_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Magic_roster<-Magic[[2]][-1,]
header<-Magic_roster[1,] 
Magic_roster<-data.table(Magic_roster[-1,]) 
setnames(Magic_roster,names(Magic_roster),as.character(unlist(header[1,])))
Magic_roster<-Magic_roster[,1:8]
Magic_roster <- mutate(Magic_roster, Team = rep.int("Magic",17))

Magic_stats_url <-"http://www.espn.com/nba/team/stats/_/name/orl"

Magic <- Magic_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Magic_game_stats<-Magic[[1]][-1,] 
header<-Magic_game_stats[1,] 
Magic_game_stats<-data.table(Magic_game_stats[-1,])  
setnames(Magic_game_stats,names(Magic_game_stats),as.character(unlist(header[1,])))
Magic_game_stats <- mutate(Magic_game_stats, Team = rep.int("Magic",15))
Magic_game_stats<- Magic_game_stats[-nrow(Magic_game_stats),]

Magic_shooting_stats<-Magic[[2]][-1,] 
header<-Magic_shooting_stats[1,] 
Magic_shooting_stats<-data.table(Magic_shooting_stats[-1,])  
setnames(Magic_shooting_stats,names(Magic_shooting_stats),as.character(unlist(header[1,])))
Magic_shooting_stats <- mutate(Magic_shooting_stats, Team = rep.int("Magic",15))
Magic_shooting_stats<-Magic_shooting_stats[-nrow(Magic_shooting_stats),]


######### 76ers
Seventysixers_roster_url <- "http://www.espn.com/nba/team/roster/_/name/phi/philadelphia-76ers"

Seventysixers <- Seventysixers_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Seventysixers_roster<-Seventysixers[[2]][-1,]
header<-Seventysixers_roster[1,] 
Seventysixers_roster<-data.table(Seventysixers_roster[-1,]) 
setnames(Seventysixers_roster,names(Seventysixers_roster),as.character(unlist(header[1,])))
Seventysixers_roster<-Seventysixers_roster[,1:8]
Seventysixers_roster <- mutate(Seventysixers_roster, Team = rep.int("Seventysixers",16))

Seventysixers_stats_url <-"http://www.espn.com/nba/team/stats/_/name/phi/philadelphia-76ers"

Seventysixers <- Seventysixers_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Seventysixers_game_stats<-Seventysixers[[1]][-1,] 
header<-Seventysixers_game_stats[1,] 
Seventysixers_game_stats<-data.table(Seventysixers_game_stats[-1,])  
setnames(Seventysixers_game_stats,names(Seventysixers_game_stats),as.character(unlist(header[1,])))
Seventysixers_game_stats <- mutate(Seventysixers_game_stats, Team = rep.int("Seventysixers",17))
Seventysixers_game_stats<- Seventysixers_game_stats[-nrow(Seventysixers_game_stats),]

Seventysixers_shooting_stats<-Seventysixers[[2]][-1,] 
header<-Seventysixers_shooting_stats[1,] 
Seventysixers_shooting_stats<-data.table(Seventysixers_shooting_stats[-1,])  
setnames(Seventysixers_shooting_stats,names(Seventysixers_shooting_stats),as.character(unlist(header[1,])))
Seventysixers_shooting_stats <- mutate(Seventysixers_shooting_stats, Team = rep.int("Seventysixers",17))
Seventysixers_shooting_stats<-Seventysixers_shooting_stats[-nrow(Seventysixers_shooting_stats),]


######### SUNS
Suns_roster_url <- "http://www.espn.com/nba/team/roster/_/name/phx/phoenix-suns"

Suns <- Suns_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Suns_roster<-Suns[[2]][-1,]
header<-Suns_roster[1,] 
Suns_roster<-data.table(Suns_roster[-1,]) 
setnames(Suns_roster,names(Suns_roster),as.character(unlist(header[1,])))
Suns_roster<-Suns_roster[,1:8]
Suns_roster <- mutate(Suns_roster, Team = rep.int("Suns",14))

Suns_stats_url <-"http://www.espn.com/nba/team/stats/_/name/phx"

Suns <- Suns_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Suns_game_stats<-Suns[[1]][-1,] 
header<-Suns_game_stats[1,] 
Suns_game_stats<-data.table(Suns_game_stats[-1,])  
setnames(Suns_game_stats,names(Suns_game_stats),as.character(unlist(header[1,])))
Suns_game_stats <- mutate(Suns_game_stats, Team = rep.int("Suns",16))
Suns_game_stats<- Suns_game_stats[-nrow(Suns_game_stats),]

Suns_shooting_stats<-Suns[[2]][-1,] 
header<-Suns_shooting_stats[1,] 
Suns_shooting_stats<-data.table(Suns_shooting_stats[-1,])  
setnames(Suns_shooting_stats,names(Suns_shooting_stats),as.character(unlist(header[1,])))
Suns_shooting_stats <- mutate(Suns_shooting_stats, Team = rep.int("Suns",16))
Suns_shooting_stats<-Suns_shooting_stats[-nrow(Suns_shooting_stats),]


######### TRAILBLAZERS
Trailblazers_roster_url <- "http://www.espn.com/nba/team/roster/_/name/por/portland-trail-blazers"

Trailblazers <- Trailblazers_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Trailblazers_roster<-Trailblazers[[2]][-1,]
header<-Trailblazers_roster[1,] 
Trailblazers_roster<-data.table(Trailblazers_roster[-1,]) 
setnames(Trailblazers_roster,names(Trailblazers_roster),as.character(unlist(header[1,])))
Trailblazers_roster<-Trailblazers_roster[,1:8]
Trailblazers_roster <- mutate(Trailblazers_roster, Team = rep.int("Trailblazers",15))

Trailblazers_stats_url <-"http://www.espn.com/nba/team/stats/_/name/por/portland-trail-blazers "

Trailblazers <- Trailblazers_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Trailblazers_game_stats<-Trailblazers[[1]][-1,] 
header<-Trailblazers_game_stats[1,] 
Trailblazers_game_stats<-data.table(Trailblazers_game_stats[-1,])  
setnames(Trailblazers_game_stats,names(Trailblazers_game_stats),as.character(unlist(header[1,])))
Trailblazers_game_stats <- mutate(Trailblazers_game_stats, Team = rep.int("Trailblazers",16))
Trailblazers_game_stats<- Trailblazers_game_stats[-nrow(Trailblazers_game_stats),]

Trailblazers_shooting_stats<-Trailblazers[[2]][-1,] 
header<-Trailblazers_shooting_stats[1,] 
Trailblazers_shooting_stats<-data.table(Trailblazers_shooting_stats[-1,])  
setnames(Trailblazers_shooting_stats,names(Trailblazers_shooting_stats),as.character(unlist(header[1,])))
Trailblazers_shooting_stats <- mutate(Trailblazers_shooting_stats, Team = rep.int("Trailblazers",16))
Trailblazers_shooting_stats<-Trailblazers_shooting_stats[-nrow(Trailblazers_shooting_stats),]

######### KINGS
Kings_roster_url <- "http://www.espn.com/nba/team/roster/_/name/sac/sacramento-kings"

Kings <- Kings_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Kings_roster<-Kings[[2]][-1,]
header<-Kings_roster[1,] 
Kings_roster<-data.table(Kings_roster[-1,]) 
setnames(Kings_roster,names(Kings_roster),as.character(unlist(header[1,])))
Kings_roster<-Kings_roster[,1:8]
Kings_roster <- mutate(Kings_roster, Team = rep.int("Kings",17))

Kings_stats_url <-"http://www.espn.com/nba/team/stats/_/name/sac"

Kings <- Kings_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Kings_game_stats<-Kings[[1]][-1,] 
header<-Kings_game_stats[1,] 
Kings_game_stats<-data.table(Kings_game_stats[-1,])  
setnames(Kings_game_stats,names(Kings_game_stats),as.character(unlist(header[1,])))
Kings_game_stats <- mutate(Kings_game_stats, Team = rep.int("Kings",16))
Kings_game_stats<- Kings_game_stats[-nrow(Kings_game_stats),]

Kings_shooting_stats<-Kings[[2]][-1,] 
header<-Kings_shooting_stats[1,] 
Kings_shooting_stats<-data.table(Kings_shooting_stats[-1,])  
setnames(Kings_shooting_stats,names(Kings_shooting_stats),as.character(unlist(header[1,])))
Kings_shooting_stats <- mutate(Kings_shooting_stats, Team = rep.int("Kings",16))
Kings_shooting_stats<-Kings_shooting_stats[-nrow(Kings_shooting_stats),]


######### SPURS
Spurs_roster_url <- "http://www.espn.com/nba/team/roster/_/name/sa/san-antonio-spurs"

Spurs <- Spurs_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Spurs_roster<-Spurs[[2]][-1,]
header<-Spurs_roster[1,] 
Spurs_roster<-data.table(Spurs_roster[-1,]) 
setnames(Spurs_roster,names(Spurs_roster),as.character(unlist(header[1,])))
Spurs_roster<-Spurs_roster[,1:8]
Spurs_roster <- mutate(Spurs_roster, Team = rep.int("Spurs",17))

Spurs_stats_url <-"http://www.espn.com/nba/team/stats/_/name/sa/san-antonio-spurs"

Spurs <- Spurs_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Spurs_game_stats<-Spurs[[1]][-1,] 
header<-Spurs_game_stats[1,] 
Spurs_game_stats<-data.table(Spurs_game_stats[-1,])  
setnames(Spurs_game_stats,names(Spurs_game_stats),as.character(unlist(header[1,])))
Spurs_game_stats <- mutate(Spurs_game_stats, Team = rep.int("Spurs",15))
Spurs_game_stats<- Spurs_game_stats[-nrow(Spurs_game_stats),]

Spurs_shooting_stats<-Spurs[[2]][-1,] 
header<-Spurs_shooting_stats[1,] 
Spurs_shooting_stats<-data.table(Spurs_shooting_stats[-1,])  
setnames(Spurs_shooting_stats,names(Spurs_shooting_stats),as.character(unlist(header[1,])))
Spurs_shooting_stats <- mutate(Spurs_shooting_stats, Team = rep.int("Spurs",15))
Spurs_shooting_stats<-Spurs_shooting_stats[-nrow(Spurs_shooting_stats),]

######### RAPTORS
Raptors_roster_url <- "http://www.espn.com/nba/team/roster/_/name/tor/toronto-raptors"

Raptors <- Raptors_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Raptors_roster<-Raptors[[2]][-1,]
header<-Raptors_roster[1,] 
Raptors_roster<-data.table(Raptors_roster[-1,]) 
setnames(Raptors_roster,names(Raptors_roster),as.character(unlist(header[1,])))
Raptors_roster<-Raptors_roster[,1:8]
Raptors_roster <- mutate(Raptors_roster, Team = rep.int("Raptors",16))

Raptors_stats_url <-"http://www.espn.com/nba/team/stats/_/name/tor"

Raptors <- Raptors_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Raptors_game_stats<-Raptors[[1]][-1,] 
header<-Raptors_game_stats[1,] 
Raptors_game_stats<-data.table(Raptors_game_stats[-1,])  
setnames(Raptors_game_stats,names(Raptors_game_stats),as.character(unlist(header[1,])))
Raptors_game_stats <- mutate(Raptors_game_stats, Team = rep.int("Raptors",17))
Raptors_game_stats<- Raptors_game_stats[-nrow(Raptors_game_stats),]

Raptors_shooting_stats<-Raptors[[2]][-1,] 
header<-Raptors_shooting_stats[1,] 
Raptors_shooting_stats<-data.table(Raptors_shooting_stats[-1,])  
setnames(Raptors_shooting_stats,names(Raptors_shooting_stats),as.character(unlist(header[1,])))
Raptors_shooting_stats <- mutate(Raptors_shooting_stats, Team = rep.int("Raptors",17))
Raptors_shooting_stats<-Raptors_shooting_stats[-nrow(Raptors_shooting_stats),]


######### JAZZ
Jazz_roster_url <- "http://www.espn.com/nba/team/roster/_/name/utah/utah-jazz"

Jazz <- Jazz_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Jazz_roster<-Jazz[[2]][-1,]
header<-Jazz_roster[1,] 
Jazz_roster<-data.table(Jazz_roster[-1,]) 
setnames(Jazz_roster,names(Jazz_roster),as.character(unlist(header[1,])))
Jazz_roster<-Jazz_roster[,1:8]
Jazz_roster <- mutate(Jazz_roster, Team = rep.int("Jazz",17))

Jazz_stats_url <-"http://www.espn.com/nba/team/stats/_/name/utah/utah-jazz"

Jazz <- Jazz_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Jazz_game_stats<-Jazz[[1]][-1,] 
header<-Jazz_game_stats[1,] 
Jazz_game_stats<-data.table(Jazz_game_stats[-1,])  
setnames(Jazz_game_stats,names(Jazz_game_stats),as.character(unlist(header[1,])))
Jazz_game_stats <- mutate(Jazz_game_stats, Team = rep.int("Jazz",17))
Jazz_game_stats<- Jazz_game_stats[-nrow(Jazz_game_stats),]

Jazz_shooting_stats<-Jazz[[2]][-1,] 
header<-Jazz_shooting_stats[1,] 
Jazz_shooting_stats<-data.table(Jazz_shooting_stats[-1,])  
setnames(Jazz_shooting_stats,names(Jazz_shooting_stats),as.character(unlist(header[1,])))
Jazz_shooting_stats <- mutate(Jazz_shooting_stats, Team = rep.int("Jazz",17))
Jazz_shooting_stats<-Jazz_shooting_stats[-nrow(Jazz_shooting_stats),]


######### WIZARDS
Wizards_roster_url <- "http://www.espn.com/nba/team/roster/_/name/wsh/washington-wizards"

Wizards <- Wizards_roster_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Wizards_roster<-Wizards[[2]][-1,]
header<-Wizards_roster[1,] 
Wizards_roster<-data.table(Wizards_roster[-1,]) 
setnames(Wizards_roster,names(Wizards_roster),as.character(unlist(header[1,])))
Wizards_roster<-Wizards_roster[,1:8]
Wizards_roster <- mutate(Wizards_roster, Team = rep.int("Wizards",17))

Wizards_stats_url <-"http://www.espn.com/nba/team/stats/_/name/wsh/washington-wizards"

Wizards <- Wizards_stats_url %>%
  read_html() %>%
  html_table(fill= TRUE)

Wizards_game_stats<-Wizards[[1]][-1,] 
header<-Wizards_game_stats[1,] 
Wizards_game_stats<-data.table(Wizards_game_stats[-1,])  
setnames(Wizards_game_stats,names(Wizards_game_stats),as.character(unlist(header[1,])))
Wizards_game_stats <- mutate(Wizards_game_stats, Team = rep.int("Wizards",17))
Wizards_game_stats<- Wizards_game_stats[-nrow(Wizards_game_stats),]

Wizards_shooting_stats<-Wizards[[2]][-1,] 
header<-Wizards_shooting_stats[1,] 
Wizards_shooting_stats<-data.table(Wizards_shooting_stats[-1,])  
setnames(Wizards_shooting_stats,names(Wizards_shooting_stats),as.character(unlist(header[1,])))
Wizards_shooting_stats <- mutate(Wizards_shooting_stats, Team = rep.int("Wizards",17))
Wizards_shooting_stats<-Wizards_shooting_stats[-nrow(Wizards_shooting_stats),]

######### Create three main data tables and save them as a csv

Roster <- rbind(Hawks_roster, Celtics_roster, Nets_roster, Hornets_roster, Bulls_roster, Cavaliers_roster, Mavericks_roster, Nuggets_roster, Pistons_roster, Warriors_roster, Rockets_roster, Pacers_roster, Clippers_roster, Lakers_roster, Grizzlies_roster, Heat_roster, Bucks_roster, Timberwolves_roster, Pelicans_roster, Knicks_roster, Thunder_roster, Magic_roster, Seventysixers_roster, Trailblazers_roster, Kings_roster, Spurs_roster, Raptors_roster, Jazz_roster, Wizards_roster)
fwrite(Roster, "Roster.csv")
Shooting_stats<- rbind(Hawks_shooting_stats, Celtics_shooting_stats, Nets_shooting_stats, Bulls_shooting_stats, Cavaliers_shooting_stats, Mavericks_shooting_stats, Nuggets_shooting_stats, Pistons_shooting_stats, Warriors_shooting_stats, Rockets_shooting_stats, Pacers_shooting_stats, Clippers_shooting_stats, Lakers_shooting_stats, Grizzlies_shooting_stats, Heat_shooting_stats, Bucks_shooting_stats, Timberwolves_shooting_stats, Pelicans_shooting_stats, Knicks_shooting_stats, Thunder_shooting_stats, Magic_shooting_stats ,Seventysixers_shooting_stats, Suns_shooting_stats, Trailblazers_shooting_stats,Kings_shooting_stats, Spurs_shooting_stats, Raptors_shooting_stats, Jazz_shooting_stats, Wizards_shooting_stats)
fwrite(Shooting_stats, "Shooting_stats.csv")
Game_stats<- rbind(Hawks_game_stats, Celtics_game_stats, Nets_game_stats, Bulls_game_stats, Cavaliers_game_stats, Mavericks_game_stats, Nuggets_game_stats, Pistons_game_stats, Warriors_game_stats, Rockets_game_stats, Pacers_game_stats, Clippers_game_stats, Lakers_game_stats, Grizzlies_game_stats, Heat_game_stats, Bucks_game_stats, Timberwolves_game_stats, Pelicans_game_stats, Knicks_game_stats, Thunder_game_stats, Magic_game_stats ,Seventysixers_game_stats, Suns_game_stats, Trailblazers_game_stats,Kings_game_stats, Spurs_game_stats, Raptors_game_stats, Jazz_game_stats, Wizards_game_stats)
fwrite(Game_stats, "Game_Stats.csv")

######### Clean up the data. Make columns numerical with only numerical characters and rename column names

Roster$Salary <- gsub('[$]','',Roster$Salary)
Roster$Salary <- as.numeric(gsub(',','',Roster$Salary))

Game_stats$GP <- as.numeric(Game_stats$GP)
Game_stats$GS <- as.numeric(Game_stats$GS)
Game_stats$MIN <- as.numeric(Game_stats$MIN)
Game_stats$OFFR <- as.numeric(Game_stats$OFFR)
Game_stats$DEFR <- as.numeric(Game_stats$DEFR)
Game_stats$APG <- as.numeric(Game_stats$APG)
Game_stats$RPG <- as.numeric(Game_stats$RPG)
Game_stats$SPG <- as.numeric(Game_stats$SPG)
Game_stats$BPG <- as.numeric(Game_stats$BPG)
Game_stats$TPG <- as.numeric(Game_stats$TPG)
Game_stats$FPG <- as.numeric(Game_stats$FPG)

colnames(Shooting_stats)[4] <- "FGPerc"
colnames(Shooting_stats)[5] <- "ThreePM"
colnames(Shooting_stats)[6] <- "ThreePA"
colnames(Shooting_stats)[7] <- "ThreePerc"
colnames(Shooting_stats)[10] <- "FTPerc"
colnames(Shooting_stats)[11] <- "TwoPM"
colnames(Shooting_stats)[12] <- "TwoPA"
colnames(Shooting_stats)[13] <- "TwoPerc"
colnames(Shooting_stats)[14] <- "PPS"
colnames(Shooting_stats)[15] <- "AFGPerc"

Shooting_stats$FGA <- as.numeric(Shooting_stats$FGA)
Shooting_stats$FGM <- as.numeric(Shooting_stats$FGM)
Shooting_stats$FGPerc <- as.numeric(Shooting_stats$FGPerc)
Shooting_stats$ThreePM <- as.numeric(Shooting_stats$ThreePM)
Shooting_stats$ThreePA <- as.numeric(Shooting_stats$ThreePA)
Shooting_stats$ThreePerc <- as.numeric(Shooting_stats$ThreePerc)
Shooting_stats$FTM <- as.numeric(Shooting_stats$FTM)
Shooting_stats$FTA <- as.numeric(Shooting_stats$FTA)
Shooting_stats$FTPerc <- as.numeric(Shooting_stats$FTPerc)
Shooting_stats$TwoPM <- as.numeric(Shooting_stats$TwoPM)
Shooting_stats$TwoPA <- as.numeric(Shooting_stats$TwoPA)
Shooting_stats$TwoPerc <- as.numeric(Shooting_stats$TwoPerc)
Shooting_stats$PPS <- as.numeric(Shooting_stats$PPS)
Shooting_stats$AFGPerc <- as.numeric(Shooting_stats$AFGPerc)
Game_stats$PPG<-as.numeric(Game_stats$PPG)


######### Create new columns  and variables. Merge some of those new columns together

avg_team_salary <- dcast(Roster, Team~., mean, na.rm=T, value.var = c("Salary"))
setnames(avg_team_salary, ".", "avg_team_salary")
Roster <- merge(Roster, avg_team_salary, by = c("Team"))
Roster$Team<-factor(Roster$Team,levels=(avg_team_salary$Team))

college_count <- dcast(Roster, College~., length, value.var =c("College"))
setnames(college_count, ".", "counts")
college_count <- college_count[-1,]
college_count<-college_count[order(-college_count$counts),] 

avg_position_salary <- dcast(Roster, POS~., mean, na.rm = T,value.var =c("Salary"))
setnames(avg_position_salary, ".", "Average_position_salary")
setnames(avg_position_salary, "POS", "Position")
avg_position_salary$Average_position_salary <- round(avg_position_salary$Average_position_salary, digits = 2)
avg_position_salary$Position <- c("Center", "Front", "Gaurd", "Power_Foreward", "Point_Gaurd","Small_Foreward", "Shooting_Gaurd")

avg_team_salary <- dcast(Roster, Team~., mean, na.rm = T,value.var =c("Salary"))
setnames(avg_team_salary, ".", "Average_team_salary")
avg_team_salary <- avg_team_salary[order(-avg_team_salary$Average_team_salary),]

PPG_dcast<- dcast(Game_stats, Team~., mean, na.rm=TRUE, value.var="PPG")

######### Create plots using ggplot. Included are figure captions to explain the meaning

######### This is a bar plot. Each bar represents a team's average salary  
ggplot(Roster, aes(x=Team, y = avg_team_salary)) + geom_bar(stat = "identity") + ggtitle("Average Team Salary") + geom_text(aes(label = avg_team_salary), angle = 90, position=position_dodge(width=0.9), vjust=-0.25) + ylab("Average Salary") 

######### This is a simple scatterplot. Each point represents the average salary for each NBA position 
ggplot(avg_position_salary, aes(x=Position, y = Average_position_salary)) + geom_point() + ggtitle("Average Position Salary") + ylab("Average Salary") + xlab("Position") + geom_text(aes(label = avg_position_salary$Average_position_salary), size = 4, hjust = 0.5, vjust = 3, position ="stack")

######### This is a box and whisker plot. Each box represents a team with the corresponding box plot values for the average points per game
ggplot(Game_stats, aes(x=Team, y = PPG), na.rm = T) + geom_boxplot() + ylab("Points Per Game") + ggtitle("Points Per Game By Team")

######### This is a scatterplot of Games Played and Points Per Game for players in the NBA. There is a positive trend
ggplot(Game_stats, aes(x=GP, y = PPG)) + geom_point() +ylab("Points Per Game") + xlab("Games Played") + ggtitle("Plot of Points Per Game and Games Played") 

######### Statistical Analysis. All include regression 

######### Do a model selection with backwards selection, using alpha level 0.15
lm_fit <- lm(PER~ GP + GS + MIN + OFFR + DEFR + RPG + APG + SPG + BPG + TPG + FPG, data = Game_stats)
summary(lm_fit)
par(mfrow = c(2,2))
plot(lm_fit)
lm_back1= update(lm_fit, .~. -OFFR)
summary(lm_back1)
lm_back2= update(lm_back1, .~. -GS)
summary(lm_back2)
lm_back3= update(lm_back2, .~. -GP)
summary(lm_back3)
lm_back4 = update(lm_back3, .~. - MIN)
summary(lm_back4)
lm_back5 = update(lm_back4, .~. - SPG)
summary(lm_back5)

######### Fitted a model to predict Adjusted Field Goal Percentage (AFGPerc) with two pointers attempts, two pointers made, three pointers made and three pointers attempted
######### This models explains 78.13% of the variation in the response 

lm_fit2 = lm(AFGPerc ~ TwoPerc + TwoPA + TwoPM + ThreePerc + ThreePA + ThreePM, data = Shooting_stats)
summary(lm_fit2)
par(mfrow = c(2,2))
plot(lm_fit2)

######### Fitted a model to predict Two Pointers made by using the predictor Three Pointers made
######### This is not a good model. It explains only 10.32% of the variation in the response 

lm_fit3 = lm(TwoPM ~ ThreePM, data = Shooting_stats)
summary(lm_fit3)  
par(mfrow = c(2,2))
plot(lm_fit3)

######### Fitted a model to predict three pointers made using the predictors Two Pointers Made and Adjusted Field Goal percentage
######### 

lm_fit4 = lm(ThreePM ~ TwoPM + AFGPerc, data = Shooting_stats)
summary(lm_fit4)
par(mfrow = c(2,2))
plot(lm_fit4)

