# Idai-Emergency
Cleveland dot-plot for Mozambique's district exposure to Cyclone Idai (2019).
Plot created for third-year Geography project at the University of Bristol using the tidyverse() library in Rstudio. 

Dataframe ordered by districts, with a row for the exposure (and associated percentage exposure) in each return period.

Naming conventions: 

H20 = The population exposured in a 1-in-20-year flood.

H1000PR = The percentage of the district exposed to a 1-in-1000-year flood. 

NAME_2 = The name of the District 

```{r}

 Dataframe %>% 
 #top 10 most exposed districts.
  arrange(desc(H20)) >%>
  head(10) %>%
  
 #creating the plot
 #order the graph in terms of the population exposed to the 1-in-20-year flood
 
 ggplot(aes(x=reorder(NAME_2,H20))) + 
 
 #create a line between the two return periods
 
  geom_linerange(aes(ymin=H20,ymax=H1000), 
    colour = "#f3d478", size = 2, alpha = 0.8) +
    
 #create a point on each end of the line, representing the exposure to the two return periods, with seperate colours for each return period.
 
  geom_point(aes(y=H1000),color="red",size=4) +
  geom_point(aes(y=H20),colour="blue",size=4) +
  labs(x="Districts",y="Population Exposured",title="Top 10 Most Exposed Districts",subtitle="% represent the % in district exposed to fluvial flooding") + 
  scale_y_continuous(trans = "log10", expand=c(0,0.16) +
  coord_flip() +
  
#add a label for the percentage of the district exposed on each end of the line, coloured the same as the point. hjust is used to shift the label across from the point.

  geom_text(aes(y=H20, label = scales::percent(round(H20PR/100,2),accuracy=1L)),size=4,hjust=1.5,colour="blue",fontface="bold") + 
  geom_text(aes(y=H1000, label = scales::percent(round(H1000PR/100,2),accuracy=1L)),size=4,hjust=-0.5,colour="red") +
  theme_light()
  
```

The image can be seen as:

![alt text](https://raw.github.com/EJPullen/Idai-Emergency/blob/main/markdowngraph


