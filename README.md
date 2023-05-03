# SHOWCASE_ARB_1
Showcase GitHub Bees repository
getwd()

library("readxl")
library("dplyr")

#loading the data
sdata <- read_excel("/Users/albertorodriguezballesteros/myrepo/SHOWCASE_code/SHOWCASE_Coding_ARB/Guadalquivida_Bees2022_ARB.xlsx")

nspecies <- sdata %>% 
group_by(Farm, Treatment) %>% 
summarise(nspecies=n_distinct(Genus_species),
ninsects=sum(Count))

nspecies

#Visualizing the data for Richness
farmsplot <- ggplot(data=nspecies, aes(x=Farm, y=nspecies, fill=Treatment)) +
geom_bar(stat="identity", position=position_dodge())

farmsplot

#Adding labels

farmsplot + labs(title="Richness", 
         x="Farms", y = "Nº species")+
   scale_fill_manual(values=c('brown','lightgreen'))+
   theme_classic()

#Visualizing the data for Abundance
farmsplot <- ggplot(data=nspecies, aes(x=Farm, y=ninsects, fill=Treatment)) +
geom_bar(stat="identity", position=position_dodge())

farmsplot + labs(title="Abundance", 
         x="Farms", y = "Nº individuals")+
   scale_fill_manual(values=c('brown','lightgreen'))+
   theme_classic()

#Adding labels

#Checking the data
headTail(sdata)
str(sdata)

names(sdata) 
summary(sdata)

colSums(is.na(sdata))

#Tranformingdata

sdata$Farm <- as.factor(sdata$Farm)
sdata$Treatment <- as.factor(sdata$Treatment)
sdata$Genus_species <- as.factor(sdata$Genus_species)

sdata$Genus_species <- as.numeric(sdata$Genus_species)

#Visualizing the data
farmsplot <- ggplot(data=sdata, aes(x=Farm, y=n_distinct(Genus_species), fill=Treatment)) +
geom_bar(stat="identity", position=position_dodge())

#Adding labels

farmsplot + labs(title="Control and intervention between farms", 
         x="Farms", y = "Nº species")+
   scale_fill_manual(values=c('black','lightgray'))+
   theme_classic()


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

farms1[is.na(farms1)] <- 0
summary(farms1)
headTail(farms1)

#Notes: 8 orders, 54 Genus, 92 species in total!







