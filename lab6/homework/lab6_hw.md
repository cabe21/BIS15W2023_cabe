---
title: "Lab 6 Homework"
author: "Chris Abe"
date: "2023-02-01"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(skimr)
```

For this assignment we are going to work with a large data set from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. These data are pretty wild, so we need to do some cleaning. First, load the data.  

Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv(file = "data/FAO_1950to2012_111914.csv")
```

```
## Rows: 17692 Columns: 71
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr (69): Country, Common name, ISSCAAP taxonomic group, ASFIS species#, ASF...
## dbl  (2): ISSCAAP group#, FAO major fishing area
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

```r
summary(fisheries)
```

```
##    Country          Common name        ISSCAAP group#  ISSCAAP taxonomic group
##  Length:17692       Length:17692       Min.   :11.00   Length:17692           
##  Class :character   Class :character   1st Qu.:33.00   Class :character       
##  Mode  :character   Mode  :character   Median :36.00   Mode  :character       
##                                        Mean   :37.38                          
##                                        3rd Qu.:38.00                          
##                                        Max.   :77.00                          
##  ASFIS species#     ASFIS species name FAO major fishing area
##  Length:17692       Length:17692       Min.   :18.00         
##  Class :character   Class :character   1st Qu.:31.00         
##  Mode  :character   Mode  :character   Median :37.00         
##                                        Mean   :45.34         
##                                        3rd Qu.:57.00         
##                                        Max.   :88.00         
##    Measure              1950               1951               1952          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1953               1954               1955               1956          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1957               1958               1959               1960          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1961               1962               1963               1964          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1965               1966               1967               1968          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1969               1970               1971               1972          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1973               1974               1975               1976          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1977               1978               1979               1980          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1981               1982               1983               1984          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1985               1986               1987               1988          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1989               1990               1991               1992          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1993               1994               1995               1996          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1997               1998               1999               2000          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2001               2002               2003               2004          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2005               2006               2007               2008          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2009               2010               2011               2012          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
## 
```

```r
names(fisheries)
```

```
##  [1] "Country"                 "Common name"            
##  [3] "ISSCAAP group#"          "ISSCAAP taxonomic group"
##  [5] "ASFIS species#"          "ASFIS species name"     
##  [7] "FAO major fishing area"  "Measure"                
##  [9] "1950"                    "1951"                   
## [11] "1952"                    "1953"                   
## [13] "1954"                    "1955"                   
## [15] "1956"                    "1957"                   
## [17] "1958"                    "1959"                   
## [19] "1960"                    "1961"                   
## [21] "1962"                    "1963"                   
## [23] "1964"                    "1965"                   
## [25] "1966"                    "1967"                   
## [27] "1968"                    "1969"                   
## [29] "1970"                    "1971"                   
## [31] "1972"                    "1973"                   
## [33] "1974"                    "1975"                   
## [35] "1976"                    "1977"                   
## [37] "1978"                    "1979"                   
## [39] "1980"                    "1981"                   
## [41] "1982"                    "1983"                   
## [43] "1984"                    "1985"                   
## [45] "1986"                    "1987"                   
## [47] "1988"                    "1989"                   
## [49] "1990"                    "1991"                   
## [51] "1992"                    "1993"                   
## [53] "1994"                    "1995"                   
## [55] "1996"                    "1997"                   
## [57] "1998"                    "1999"                   
## [59] "2000"                    "2001"                   
## [61] "2002"                    "2003"                   
## [63] "2004"                    "2005"                   
## [65] "2006"                    "2007"                   
## [67] "2008"                    "2009"                   
## [69] "2010"                    "2011"                   
## [71] "2012"
```

```r
dim(fisheries)
```

```
## [1] 17692    71
```

```r
anyNA(fisheries)
```

```
## [1] TRUE
```

2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 

```r
fisheries <- janitor::clean_names(fisheries)
```


```r
"country" <- 
  as.factor("country") 
"issacaap_group_number" <- 
  as.factor("issacaap_group_number") 
"afis_species_number" <- 
  as.factor("afis_species_number") 
"fao_major_fishing_area" <- 
  as.factor("fao_major_fishing_area") 
```

We need to deal with the years because they are being treated as characters and start with an X. We also have the problem that the column names that are years actually represent data. We haven't discussed tidy data yet, so here is some help. You should run this ugly chunk to transform the data for the rest of the homework. It will only work if you have used janitor to rename the variables in question 2!

```r
fisheries_tidy <- fisheries %>% 
  pivot_longer(-c(country,common_name,isscaap_group_number,isscaap_taxonomic_group,asfis_species_number,asfis_species_name,fao_major_fishing_area,measure),
               names_to = "year",
               values_to = "catch",
               values_drop_na = TRUE) %>% 
  mutate(year= as.numeric(str_replace(year, 'x', ''))) %>% 
  mutate(catch= str_replace(catch, c(' F'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('...'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('-'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('0 0'), replacement = ''))

fisheries_tidy$catch <- as.numeric(fisheries_tidy$catch)
```

3. How many countries are represented in the data? Provide a count and list their names.

```r
fisheries %>% 
  tabyl(country)
```

```
##                    country   n      percent
##                    Albania  67 3.787022e-03
##                    Algeria  59 3.334841e-03
##             American Samoa  32 1.808727e-03
##                     Angola  88 4.974000e-03
##                   Anguilla   3 1.695682e-04
##        Antigua and Barbuda  22 1.243500e-03
##                  Argentina 140 7.913181e-03
##                      Aruba   5 2.826136e-04
##                  Australia 301 1.701334e-02
##                    Bahamas  14 7.913181e-04
##                    Bahrain  62 3.504409e-03
##                 Bangladesh   8 4.521818e-04
##                   Barbados  21 1.186977e-03
##                    Belgium  57 3.221795e-03
##                     Belize 133 7.517522e-03
##                      Benin  68 3.843545e-03
##                    Bermuda  47 2.656568e-03
##   Bonaire/S.Eustatius/Saba   2 1.130454e-04
##     Bosnia and Herzegovina   1 5.652272e-05
##                     Brazil 136 7.687090e-03
##   British Indian Ocean Ter   7 3.956591e-04
##     British Virgin Islands  18 1.017409e-03
##          Brunei Darussalam   8 4.521818e-04
##                   Bulgaria 197 1.113498e-02
##           C<f4>te d'Ivoire  67 3.787022e-03
##                 Cabo Verde  26 1.469591e-03
##                   Cambodia   8 4.521818e-04
##                   Cameroon  36 2.034818e-03
##                     Canada 125 7.065340e-03
##             Cayman Islands   4 2.260909e-04
##            Channel Islands  65 3.673977e-03
##                      Chile 141 7.969704e-03
##                      China 236 1.333936e-02
##       China, Hong Kong SAR  32 1.808727e-03
##           China, Macao SAR   4 2.260909e-04
##                   Colombia  81 4.578340e-03
##                    Comoros  43 2.430477e-03
##    Congo, Dem. Rep. of the  21 1.186977e-03
##         Congo, Republic of  53 2.995704e-03
##               Cook Islands  55 3.108750e-03
##                 Costa Rica  45 2.543522e-03
##                    Croatia 103 5.821840e-03
##                       Cuba 162 9.156681e-03
##                 Cura<e7>ao   9 5.087045e-04
##                     Cyprus  96 5.426181e-03
##                    Denmark 103 5.821840e-03
##                   Djibouti  14 7.913181e-04
##                   Dominica  13 7.347954e-04
##         Dominican Republic  50 2.826136e-03
##                    Ecuador 100 5.652272e-03
##                      Egypt  87 4.917477e-03
##                El Salvador  25 1.413068e-03
##          Equatorial Guinea  15 8.478408e-04
##                    Eritrea  49 2.769613e-03
##                    Estonia 184 1.040018e-02
##                   Ethiopia   5 2.826136e-04
##     Falkland Is.(Malvinas)  33 1.865250e-03
##              Faroe Islands  96 5.426181e-03
##          Fiji, Republic of  50 2.826136e-03
##                    Finland  16 9.043636e-04
##                     France 489 2.763961e-02
##              French Guiana  18 1.017409e-03
##           French Polynesia  31 1.752204e-03
##       French Southern Terr   3 1.695682e-04
##                      Gabon  45 2.543522e-03
##                     Gambia  49 2.769613e-03
##                    Georgia  86 4.860954e-03
##                    Germany 306 1.729595e-02
##                      Ghana  94 5.313136e-03
##                  Gibraltar   1 5.652272e-05
##                     Greece 125 7.065340e-03
##                  Greenland  60 3.391363e-03
##                    Grenada  47 2.656568e-03
##                 Guadeloupe   8 4.521818e-04
##                       Guam  23 1.300023e-03
##                  Guatemala  38 2.147863e-03
##                     Guinea  56 3.165272e-03
##               GuineaBissau  32 1.808727e-03
##                     Guyana  11 6.217499e-04
##                      Haiti   6 3.391363e-04
##                   Honduras  68 3.843545e-03
##                    Iceland 107 6.047931e-03
##                      India 108 6.104454e-03
##                  Indonesia 223 1.260457e-02
##     Iran (Islamic Rep. of)  64 3.617454e-03
##                       Iraq  16 9.043636e-04
##                    Ireland 191 1.079584e-02
##                Isle of Man  41 2.317432e-03
##                     Israel  79 4.465295e-03
##                      Italy 261 1.475243e-02
##                    Jamaica   6 3.391363e-04
##                      Japan 611 3.453538e-02
##                     Jordan  12 6.782727e-04
##                      Kenya  31 1.752204e-03
##                   Kiribati  27 1.526113e-03
##   Korea, Dem. People's Rep  14 7.913181e-04
##         Korea, Republic of 620 3.504409e-02
##                     Kuwait  23 1.300023e-03
##                     Latvia 162 9.156681e-03
##                    Lebanon  20 1.130454e-03
##                    Liberia  76 4.295727e-03
##                      Libya  56 3.165272e-03
##                  Lithuania 215 1.215239e-02
##                 Madagascar  35 1.978295e-03
##                   Malaysia 166 9.382772e-03
##                   Maldives  12 6.782727e-04
##                      Malta 104 5.878363e-03
##           Marshall Islands  13 7.347954e-04
##                 Martinique  16 9.043636e-04
##                 Mauritania  93 5.256613e-03
##                  Mauritius  30 1.695682e-03
##                    Mayotte  14 7.913181e-04
##                     Mexico 198 1.119150e-02
##  Micronesia, Fed.States of  13 7.347954e-04
##                     Monaco   1 5.652272e-05
##                 Montenegro  24 1.356545e-03
##                 Montserrat   1 5.652272e-05
##                    Morocco 153 8.647976e-03
##                 Mozambique  30 1.695682e-03
##                    Myanmar   5 2.826136e-04
##                    Namibia  76 4.295727e-03
##                      Nauru   9 5.087045e-04
##                Netherlands 155 8.761022e-03
##       Netherlands Antilles  17 9.608863e-04
##              New Caledonia  26 1.469591e-03
##                New Zealand 208 1.175673e-02
##                  Nicaragua  59 3.334841e-03
##                    Nigeria  50 2.826136e-03
##                       Niue  11 6.217499e-04
##             Norfolk Island   1 5.652272e-05
##       Northern Mariana Is.  19 1.073932e-03
##                     Norway 188 1.062627e-02
##                       Oman  53 2.995704e-03
##                  Other nei 100 5.652272e-03
##                   Pakistan  60 3.391363e-03
##                      Palau  33 1.865250e-03
##    Palestine, Occupied Tr.  25 1.413068e-03
##                     Panama 121 6.839249e-03
##           Papua New Guinea  20 1.130454e-03
##                       Peru  54 3.052227e-03
##                Philippines 138 7.800136e-03
##           Pitcairn Islands   1 5.652272e-05
##                     Poland 263 1.486548e-02
##                   Portugal 763 4.312684e-02
##                Puerto Rico  49 2.769613e-03
##                      Qatar  35 1.978295e-03
##                 R<e9>union  37 2.091341e-03
##                    Romania 191 1.079584e-02
##         Russian Federation 523 2.956138e-02
##        Saint Barth<e9>lemy   1 5.652272e-05
##               Saint Helena  19 1.073932e-03
##      Saint Kitts and Nevis  28 1.582636e-03
##                Saint Lucia  27 1.526113e-03
##   Saint Vincent/Grenadines  71 4.013113e-03
##                SaintMartin   1 5.652272e-05
##                      Samoa  15 8.478408e-04
##      Sao Tome and Principe  35 1.978295e-03
##               Saudi Arabia 128 7.234908e-03
##                    Senegal 140 7.913181e-03
##      Serbia and Montenegro  45 2.543522e-03
##                 Seychelles  70 3.956591e-03
##               Sierra Leone  59 3.334841e-03
##                  Singapore  40 2.260909e-03
##               Sint Maarten   2 1.130454e-04
##                   Slovenia  50 2.826136e-03
##            Solomon Islands  18 1.017409e-03
##                    Somalia   3 1.695682e-04
##               South Africa 200 1.130454e-02
##                      Spain 915 5.171829e-02
##                  Sri Lanka  34 1.921773e-03
##    St. Pierre and Miquelon  40 2.260909e-03
##                      Sudan   3 1.695682e-04
##             Sudan (former)   3 1.695682e-04
##                   Suriname  27 1.526113e-03
##     Svalbard and Jan Mayen   1 5.652272e-05
##                     Sweden  72 4.069636e-03
##       Syrian Arab Republic  34 1.921773e-03
##   Taiwan Province of China 310 1.752204e-02
##   Tanzania, United Rep. of  49 2.769613e-03
##                   Thailand 150 8.478408e-03
##                 TimorLeste   7 3.956591e-04
##                       Togo  78 4.408772e-03
##                    Tokelau  10 5.652272e-04
##                      Tonga  14 7.913181e-04
##        Trinidad and Tobago  39 2.204386e-03
##                    Tunisia  85 4.804431e-03
##                     Turkey  76 4.295727e-03
##       Turks and Caicos Is.   6 3.391363e-04
##                     Tuvalu  10 5.652272e-04
##                    Ukraine 294 1.661768e-02
##         Un. Sov. Soc. Rep. 515 2.910920e-02
##       United Arab Emirates  52 2.939182e-03
##             United Kingdom 362 2.046123e-02
##   United States of America 627 3.543975e-02
##                    Uruguay 131 7.404477e-03
##          US Virgin Islands  29 1.639159e-03
##                    Vanuatu  71 4.013113e-03
##    Venezuela, Boliv Rep of  80 4.521818e-03
##                   Viet Nam  14 7.913181e-04
##      Wallis and Futuna Is.   5 2.826136e-04
##             Western Sahara   3 1.695682e-04
##                      Yemen  39 2.204386e-03
##             Yugoslavia SFR  36 2.034818e-03
##                   Zanzibar  19 1.073932e-03
```

```r
fisheries %>% 
summarise(n_country=n_distinct(country))
```

```
## # A tibble: 1 x 1
##   n_country
##       <int>
## 1       204
```

4. Refocus the data only to include country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
fisheries_tidy%>% 
  select(country, isscaap_taxonomic_group, asfis_species_number, asfis_species_name, year, catch)
```

```
## # A tibble: 376,771 x 6
##    country isscaap_taxonomic_group asfis_species_n~ asfis_species_n~  year catch
##    <chr>   <chr>                   <chr>            <chr>            <dbl> <dbl>
##  1 Albania Sharks, rays, chimaeras 10903XXXXX       Squatinidae       1995    NA
##  2 Albania Sharks, rays, chimaeras 10903XXXXX       Squatinidae       1996    53
##  3 Albania Sharks, rays, chimaeras 10903XXXXX       Squatinidae       1997    20
##  4 Albania Sharks, rays, chimaeras 10903XXXXX       Squatinidae       1998    31
##  5 Albania Sharks, rays, chimaeras 10903XXXXX       Squatinidae       1999    30
##  6 Albania Sharks, rays, chimaeras 10903XXXXX       Squatinidae       2000    30
##  7 Albania Sharks, rays, chimaeras 10903XXXXX       Squatinidae       2001    16
##  8 Albania Sharks, rays, chimaeras 10903XXXXX       Squatinidae       2002    79
##  9 Albania Sharks, rays, chimaeras 10903XXXXX       Squatinidae       2003     1
## 10 Albania Sharks, rays, chimaeras 10903XXXXX       Squatinidae       2004     4
## # ... with 376,761 more rows
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?

```r
fisheries_tidy %>% 
summarise(n_fish_species=n_distinct(asfis_species_number))
```

```
## # A tibble: 1 x 1
##   n_fish_species
##            <int>
## 1           1551
```

6. Which country had the largest overall catch in the year 2000?

```r
fisheries_tidy %>% 
  group_by(country) %>% 
  filter(year == 2000) %>% 
  select(country, catch) %>% 
  summarize(total_catch=sum(catch, na.rm=T)) %>% 
  arrange(desc(total_catch))
```

```
## # A tibble: 193 x 2
##    country                  total_catch
##    <chr>                          <dbl>
##  1 China                          25899
##  2 Russian Federation             12181
##  3 United States of America       11762
##  4 Japan                           8510
##  5 Indonesia                       8341
##  6 Peru                            7443
##  7 Chile                           6906
##  8 India                           6351
##  9 Thailand                        6243
## 10 Korea, Republic of              6124
## # ... with 183 more rows
```
CHINA
7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?

```r
 fisheries_tidy %>% 
   group_by(country) %>% 
   filter(between(year, 1990, 2000)) %>%   
   select(country, catch, asfis_species_name) %>% 
   filter(asfis_species_name == "Sardina pilchardus") %>% 
   summarize(total_catch=sum(catch, na.rm=T)) %>% 
   arrange(desc(total_catch))
```

```
## # A tibble: 37 x 2
##    country               total_catch
##    <chr>                       <dbl>
##  1 Morocco                      7470
##  2 Spain                        3507
##  3 Russian Federation           1639
##  4 Ukraine                      1030
##  5 France                        966
##  6 Portugal                      818
##  7 Greece                        528
##  8 Italy                         507
##  9 Serbia and Montenegro         478
## 10 Denmark                       477
## # ... with 27 more rows
```
Morocco 
8. Which five countries caught the most cephalopods between 2008-2012?

```r
fisheries_tidy %>% 
  group_by(country) %>% 
  filter(between(year, 2008, 2012)) %>%   
  select(country, catch, isscaap_taxonomic_group) %>% 
  filter(isscaap_taxonomic_group == "Squids, cuttlefishes, octopuses") %>% 
  summarize(total_catch=sum(catch, na.rm=T)) %>% 
  arrange(desc(total_catch))
```

```
## # A tibble: 122 x 2
##    country                  total_catch
##    <chr>                          <dbl>
##  1 China                           8349
##  2 Korea, Republic of              3480
##  3 Peru                            3422
##  4 Japan                           3248
##  5 Chile                           2775
##  6 United States of America        2417
##  7 Indonesia                       1622
##  8 Taiwan Province of China        1394
##  9 Spain                           1147
## 10 France                          1138
## # ... with 112 more rows
```
China, Republic of Korea, Peru, Japan, Chile. 


9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species)

```r
fisheries_tidy %>% 
  group_by(isscaap_taxonomic_group) %>% 
  filter(between(year, 2008, 2012)) %>%   
  select(catch, isscaap_taxonomic_group) %>% 
  summarize(total_catch=sum(catch, na.rm=T)) %>% 
  arrange(desc(total_catch))
```

```
## # A tibble: 30 x 2
##    isscaap_taxonomic_group         total_catch
##    <chr>                                 <dbl>
##  1 Miscellaneous coastal fishes         177754
##  2 Tunas, bonitos, billfishes           159544
##  3 Herrings, sardines, anchovies        151940
##  4 Miscellaneous pelagic fishes         141871
##  5 Cods, hakes, haddocks                118836
##  6 Marine fishes not identified         107808
##  7 Miscellaneous demersal fishes         86185
##  8 Sharks, rays, chimaeras               62381
##  9 Squids, cuttlefishes, octopuses       49805
## 10 Shrimps, prawns                       43609
## # ... with 20 more rows
```

10. Use the data to do at least one analysis of your choice.
Question trying to answer: which countries caught the most rays, sharks, and chimaeras from 2000-2012

```r
fisheries_tidy %>% 
  group_by(country) %>% 
  filter(isscaap_taxonomic_group == "Sharks, rays, chimaeras") %>% 
  filter(between(year, 2000, 2012)) %>%   
  select(catch, country, isscaap_taxonomic_group) %>% 
  summarize(total_catch=sum(catch, na.rm=T)) %>% 
  arrange(desc(total_catch))
```

```
## # A tibble: 153 x 2
##    country                  total_catch
##    <chr>                          <dbl>
##  1 Spain                          13666
##  2 Portugal                       13422
##  3 United States of America        6894
##  4 France                          6272
##  5 United Kingdom                  5488
##  6 New Zealand                     5155
##  7 Indonesia                       3320
##  8 Taiwan Province of China        2985
##  9 Uruguay                         2497
## 10 Australia                       2358
## # ... with 143 more rows
```

  
  
## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
