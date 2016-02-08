---
layout: post
title: DarkNet | Tracking the underground drug trade
---

## Background

While at Insight, I carried out a consulting project for researchers at [Epidemico](http://www.epidemico.com), a Boston-based data science company working in the population health domain. 

The goal of the project was to clean and sort a large archive of underground drug sales listings. I also carried out descriptive analyses of the data, studying relationships between country of origin, product type, and vendor.

## The Dataset

The dataset consisted of an archive of sales listings from a popular, underground marketplace known as 'Evolution'. Sales listings were originally scraped from the Evolution website by a [psuedo-anonymous hacker](http://www.gwern.net), at semi-regular intervals between January 2014 and March 2015, and can be d from a publicly available archive: <http://www.gwern.net/Black-market%20archives>

## Cleaning the Data

I began by extracting the raw HTML files from the archive, ignoring configuration files, image files etc. In total, the Evolution dataset contained approximately ~15GB of raw HTML or ~500,000 product listings over the time period covered by the archive. 

I then set about processing tools and a little patience. This process was hampered by changes in page format at a number of points in the site's history. I employed standard Python packages (e.g., Beautiful Soup, Pandas) to extract and organize relevant information from individual listings. For example, vendor ID was extracted for each listing:

```python
soup = BeautifulSoup(current_listing, 'html.parser')
...
...
# find vendor info.
temp = soup.find_all("div", "seller-info text-muted")[0]
vendor = temp.find_all("a")[0].string
```

I then sorted the extracted information into python dataframes, detailing key information about individual listings e.g., title, product, country of origin, vendor, price, etc.

[show example rows of dataframe]

## Descriptive Analyses

## Summary
Unfortunately, in parallel to legitimate internet commerce, a network of underground sales channels have spawned into life over the past decade or so, with powerful pharmaceuticals and harder drugs forming a large proportion of sales listings. While many of these so called 'DarkNet' sites eventually succumb to law enforcement endeavours or internal fraud, numerous large-scale marketplaces still exist such as AlphaBay and East India Company.
<!--more-->
