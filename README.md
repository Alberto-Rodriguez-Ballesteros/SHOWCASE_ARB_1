# SHOWCASE_ARB_1
Showcase GitHub Bees repository
getwd()

library(tidyverse)
library("readxl")
library("psych")
library("ggplot2")
library("dplyr")

#loading the data
sdata <- read_excel("/Users/albertorodriguezballesteros/myrepo/SHOWCASE_code/SHOWCASE_Coding_ARB/Guadalquivida_Bees2022_ARB.xlsx")

#Checking the data
headTail(sdata)
str(sdata)
summary(sdata)

#Notes on quantitative variables:
#Mean Temperature: 20,21º
#Mean Cloud Cover: 26.52

#FARMS dataframe
farms1 <- select(sdata, Farm, Round, Order, Genus, Species, Genus_species)


#Transforming farms data frame
farms1$Farm <- as.factor(farms1$Farm)
farms1$Order <- as.factor(farms1$Order)
farms1$Genus <- as.factor(farms1$Genus)
farms1$Species <- as.factor(farms1$Species)
farms1$Genus_species <- as.factor(farms1$Genus_species)

farms1$Farm
farms1$Order
farms1$Genus
farms1$Species
farms1$Genus_species

#Notes: 8 orders, 54 Genus, 92 species in total!

ggplot(farms1, aes(x = Round, y = Genus_species)) + 
  geom_point(position = position_jitter(0.05)) +
  theme_minimal()
  
ggplot(farms1, aes(x = Round)) +   
  geom_histogram() + 
  facet_wrap(~ Genus_species, ncol = 1)




