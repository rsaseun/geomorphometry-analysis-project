# geomorphometry-analysis-project
Tools of analysis for geomorphometry for spatial planning of sub-watershed to address soil erosion challenges

# Computational procedure for the Geomorphometry of the Anambra Basin

#Step 1: Install needed libraries

library(raster)

library(ggplot2)

library(tidyverse)

library(raster)

library(sf)

library(whitebox)

library(tmap)


#Step 2: set working directory


setwd("C:/data/R data/Geomorphmetric prioritization of the Anambra Basin")

r = raster("Elevation.tif")

#Step 3: Process raster data for terrain layers and attributes

r = aggregate(r, fact = 5)

plot(r)

df = as.data.frame(r, xy = TRUE)

ggplot()+
  geom_tile(data = df, aes(x = x, y = y, fill = Elevation))+
  scale_fill_gradientn(colors = terrain.colors(5))+
  theme_bw()


#Step 4: Create terrain layers

#1. Slope

slp = terrain(r, opt = "slope", unit = "degrees")

slp_df = as.data.frame(slp,xy = TRUE)

ggplot()+
  geom_tile(data = slp_df, aes(x = x, y = y, fill = slope))+
  scale_fill_gradientn(colors = topo.colors(10))+
  theme_bw()

#2. Aspect

asp = terrain(r, opt = "aspect", unit = "degrees")

asp_df = as.data.frame(asp, xy = TRUE)

ggplot()+
  geom_tile(data = asp_df, aes(x = x, y = y, fill = aspect))+
  scale_fill_gradientn(colors = rainbow(10))+
  theme_bw()

#Step 5: save raster layers for further geospatial analysis

writeRaster(slp, "slope.tif", NAflag = -9999, overwrite = TRUE)

list.files()
