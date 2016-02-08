---
layout: post
title: DarkNet | Tracking the underground drug trade
---

## Background

While at Insight, I carried out a consulting project for researchers at [Epidemico](http://www.epidemico.com), a Boston-based data science company working in the population health domain. 

The goal of the project was to clean and sort a large archive of underground drug sales listings. I also carried out descriptive analyses of the data, studying the relationships between country of origin, vendor, and product type.

## The Dataset

The dataset consisted of an archive of sales listings from a popular, underground marketplace known as 'Evolution', spanning the time period from January 2014 and March 2015. Sales listings were originally scraped from the Evolution website by a [psuedo-anonymous hacker](http://www.gwern.net), and can be downloaded from a publicly available archive: <http://www.gwern.net/Black-market%20archives>

## Cleaning the Data

I began by extracting all HTML files related to product listings from the archive, ignoring configuration, image files etc. In total, the Evolution dataset contained approximately ~15GB of raw HTML or ~500,000 product listings over the time period covered by the archive. 

I then set about navigating individual pages using Beautiful Soup, a standard Python package for processing HTML. I extracted key information about individual listings e.g., title, product, country of origin, vendor and price. For example, vendor ID was extracted using code similar to below:

```python
# prepare the soup
soup = BeautifulSoup(current_listing, 'html.parser')

# find vendor info.
temp = soup.find_all("div", "seller-info text-muted")[0]
vendor = temp.find_all("a")[0].string
```

Overall, the cleaning process was hampered by the sheer volume of listings, as well as changes in the webpage format (and associated HTML tags) at a number of points in the site's history.

## Sorting the Data

The extracted information was sorted into python dataframes (Pandas), and saved to .csv files for each date contained in the archive.

[show example rows of dataframe]

## Descriptive Analyses

Country of Origin

Top Five drugs by country

Top Five drugs by vendor

1g cocaine / 1g oxycodone

## Summary
I successfully cleaned and sorted a large archive of black market, drug sales listings.  Unfortunately, in parallel to legitimate internet commerce, a network of underground sales channels have spawned into life over the past decade or so, with powerful pharmaceuticals and harder drugs forming a large proportion of sales listings. While many of these so called 'DarkNet' sites eventually succumb to law enforcement endeavours or internal fraud, numerous large-scale marketplaces still exist such as AlphaBay and East India Company.
<!--more-->
