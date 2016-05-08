---
layout: post
title: DarkNet | Tracking the underground drug trade
---

## Background

While at Insight, I carried out a consulting project for researchers at [Epidemico](http://www.epidemico.com), a Boston-based data science company working in the population health domain. 

The goal of the project was to clean and sort a large archive of DarkNet drug sales listings, providing a potentially valuable resource for Epidemico and their clients. I also carried out descriptive analyses of the data, with a focus on metrics such as country of origin, product type, and pricing.

## The Dataset

The dataset consisted of sales listings from two popular, underground websites known as 'Agora' and 'Evolution'. 

Listings spanned the period from early 2014 through mid 2015, and were downloaded from a publicly accessible archive: <http://www.gwern.net/Black-market%20archives>.

## Cleaning the Data

The first task was to extract from the archives all HTML files related to product listings, ignoring configuration files, image files, etc. In total, the dataset contained approximately 20GB of raw HTML, with approximately 2,500,000 product listings. Aside from the sheer volume of raw HTML to be processed, cleaning was hampered by factors such as:
  
- large changes in website formatting across the timeline of the archives
- the lack of detailed drug labeling and categorization at the level of the raw HTML

Individual pages were navigated using Beautiful Soup, a standard Python package for processing HTML. I searched for key information about individual drug listings (e.g., product, country of origin, vendor, price, etc.). 

For example, vendor ID was extracted using code similar to below:

```python
# prepare the soup
soup = BeautifulSoup(current_listing, 'html.parser')

# find vendor info.
temp = soup.find_all("div", "seller-info text-muted")[0]
vendor = temp.find_all("a")[0].string
```

## Sorting the Data

For each date contained in the archives, the extracted information was then sorted into a dataframe (Pandas), and saved to .csv file. When data were extracted for the entire timeline, the resulting .csv files were loaded into a MySQL database for final storage.

Example listings from the Evolution dataset are shown below (note that prices are in BitCoin, and the product info. has been cleaned up for illustrative purposes):

![Example drug listings]({{ site.baseurl }}/images/table1.png "Example drug listings")

## Descriptive Analyses

### Country of Origin

I performed several descriptive analyses on the data, with a focus on the broad features of the distribution of drug listings e.g., country of origin, product type, and pricing.

For example, by sourcing where individual listings were 'Shipped From', we can illustrate the distribution of listings by country of origin. Perhaps not surprisingly, the USA accounts for a large proportion of individual listings (just under 30%), with several European countries also accounting for sizeable portions of the overall market listings:

![Listings origin]({{ site.baseurl }}/images/figure1.png "Listings origin")

## Summary
The key goal of my consulting project was to provide a cleaned and sorted archive of DarkNet drug sales listings, which I successfully delivered on. 

Numerous large-scale, DarkNet websites are still in active operation (e.g., AlphaBay). By developing tools to study these markets, I've provided a valuable resource which Epidemico and their clients can take advantage of in studying black market drug trading.
<!--more-->
