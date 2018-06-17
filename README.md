
<!-- README.md is generated from README.Rmd. Please edit that file -->
tiles
=====

``` r
# devtools::install_github("ropensci/osmdata")                                            
library(osmdata)                                                                        
#> Data (c) OpenStreetMap contributors, ODbL 1.0. http://www.openstreetmap.org/copyright
library(raster)                                                                         
#> Loading required package: sp
library(tiler)                                                                          
bb = getbb("Accra")                                                                     
ex = extent(bb)                                                                         
r = raster(ex, nrows = 100, ncols = 100)                                                
values(r) = rep(1:100, 100)                                                             
plot(r)                                                                                 
```

![](README_files/figure-markdown_github/unnamed-chunk-1-1.png)

``` r
writeRaster(r, "r.tif", overwrite = TRUE)                                           
system("gdal2tiles.py -s EPSG:4326 -z 2-14 r.tif accra")
browseURL("accra/leaflet.html")                                   
```

``` r
library("leaflet")
leaflet() %>%
  setView(0, 5, zoom = 9) %>% 
  # addTiles() %>% 
  addTiles(urlTemplate = "http://ATFutures.github.io/tiles/accra/{z}/{x}/{y}.png",
           options = tileOptions(minZoom = 15, maxZoom = 18, tms = TRUE))
```

![](README_files/figure-markdown_github/unnamed-chunk-2-1.png)
