---
layout: post
title: DarkNet | Tracking the underground drug trade
---

## Background

While at Insight, I carried out a consulting project for researchers at [Epidemico](http://www.epidemico.com), a Boston-based data science company working in the population health domain. 

The goal of the project was to clean and sort a large archive of DarkNet drug sales listings, providing a potentially valuable database for Epidemico and clients. I also carried out descriptive analyses of the data, focussing on unique country, product type, and vendor combinations. 

In one surprising finding, I found evidence of large price differences between DarkNet sales of certain pharmaceuticals and typical street prices reported on a crowdsourcing website (<http://www.streetrx.com>).

## The Dataset

The dataset consisted of an archive of sales listings from a popular, underground website known as 'Evolution'. These listings spanned the time period from January 2014 to March 2015, and were downloaded in raw form from a publicly available archive: <http://www.gwern.net/Black-market%20archives>.

## Cleaning the Data

I began by extracting from the archive all HTML files related to product listings, ignoring configuration, image files etc. In total, the entire dataset contained approximately ~20GB of raw HTML, or ~500,000 product listings, over the 14-month time period.

I then set about navigating individual pages using Beautiful Soup, a standard Python package for processing HTML. I extracted key information about individual listings e.g., title, product, country of origin, vendor and price. 

For example, vendor ID was extracted using code similar to below:

```python
# prepare the soup
soup = BeautifulSoup(current_listing, 'html.parser')

# find vendor info.
temp = soup.find_all("div", "seller-info text-muted")[0]
vendor = temp.find_all("a")[0].string
```

The cleaning process was hampered by the sheer volume of listings, as well as changes in the webpage format (and associated HTML tags) at a number of points in the site's history.

## Sorting the Data

The extracted information was sorted into Python dataframes (Pandas), and saved to .csv files for each date contained in the archive. The data was also loaded into a MySQL database.

An example of the type of listings extracted from the archive:

[TBD]

## Descriptive Analyses

I performed several descriptive analyses of the data, focussing on broad markers of the distribution of drug listings e.g., by country of origin, vendor and product type.

For example, by sourcing where individual listings were 'Shipped From', we can illustrate the distribution of listings by country of origin. Not surprisingly, the US accounts for a large proportion of individual listings:

[TBD]

## Summary
I successfully cleaned and sorted a large archive of black market, drug sales listings. Numerous large-scale DarkNet marketplaces still exist (e.g., AlphaBay). By creating a clean database and developing the tools to study such marketplaces, I have added a valuable resource from which to study and predict sales listings behavior on currently active marketplaces.
<!--more-->
