---
layout: post
title: DarkNet | Tracking the underground drug trade
---

## Background

While at Insight, I carried out a consulting project for researchers at [Epidemico](http://www.epidemico.com), a Boston-based data science company working in the population health domain. 

The goal of the project was to clean and sort a large archive of DarkNet drug sales listings, providing a potentially valuable database for Epidemico and their clients. In one surprising finding, I found evidence of large price differences between DarkNet sales of certain pharmaceuticals and typically reported street prices. I also carried out detailed descriptive analyses of the data, with a focus on unique country, product type, and vendor combinations.

## The Dataset

The dataset consisted of sales listings from two popular, underground websites known as 'Agora' and 'Evolution'. 

Listings spanned the period from early 2014 through mid 2015, and were downloaded in raw form from a publicly accessible archive: <http://www.gwern.net/Black-market%20archives>.

## Cleaning the Data

The first task was to extract from the archives all HTML files related to product listings, ignoring configuration files, image files etc. In total, the dataset contained approximately ~20GB of raw HTML, or ~500,000 product listings.

I navigated individual pages using Beautiful Soup, a standard Python package for processing HTML, searching for listings of drug products. I extracted key information about individual drug listings e.g., title, product, country of origin, vendor, price. 

For example, vendor ID was extracted using code similar to below:

```python
# prepare the soup
soup = BeautifulSoup(current_listing, 'html.parser')

# find vendor info.
temp = soup.find_all("div", "seller-info text-muted")[0]
vendor = temp.find_all("a")[0].string
```

The cleaning process was hampered by occasional changes in website/HTML format, and by the sheer volume of listings. However, I managed to develop a relatively consice set of Python scripts to parse listings from both websites automatically.

## Sorting the Data

For each date contained in the archives, the extracted information was sorted into a dataframe (Pandas), and saved to .csv file. When data was extracted for the entire archive timeline, I loaded the resulting .csv files into a MySQL database for final storage.

An example of the type of listings extracted from the archive:

[TBD]

## Descriptive Analyses

I performed several descriptive analyses of the data, focussing on broad markers of the distribution of drug listings e.g., country of origin, vendor and product type.

For example, by sourcing where individual listings were 'Shipped From', we can illustrate the distribution of listings by country of origin. Perhaps not surprisingly, the US accounts for a large proportion of individual listings:

[TBD]

## From DarkNet to the street


## Summary
I successfully cleaned and sorted a large archive of DarkNet drug sales listings, and analyzed key markers of the distribution of drug listings. 

Numerous large-scale DarkNet marketplaces still exist (e.g., AlphaBay). By developing a database and tools to study such marketplaces, I have provided a valuable resource from which Epidemico and their clients can study and predict sales listings behavior on currently active marketplaces.
<!--more-->
