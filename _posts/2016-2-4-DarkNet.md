---
layout: post
title: DarkNet | Tracking the underground drug trade
---

## Background

While at Insight, I carried out a consulting project for researchers at [Epidemico](http://www.epidemico.com), a Boston-based data science company working in the population health domain. 

The goal of the project was to clean and sort a large archive of DarkNet drug sales listings, providing a potentially valuable resource for Epidemico and their clients. I also carried out descriptive analyses of the data, with a focus on metrics such as country of origin, product type, and pricing. In one surprising result, I found evidence of large price differences between DarkNet sales of certain pharmaceuticals and typically reported street prices.

## The Dataset

The dataset consisted of sales listings from two popular, underground websites known as 'Agora' and 'Evolution'. 

Listings spanned the period from early 2014 through mid 2015, and were downloaded from a publicly accessible archive: <http://www.gwern.net/Black-market%20archives>.

## Cleaning the Data

The first task was to extract from the archives all HTML files related to product listings, ignoring configuration files, image files, etc. In total, the dataset contained approximately ~20GB of raw HTML, or ~500,000 product listings.

I navigated individual pages using Beautiful Soup, a standard Python package for processing HTML, searching for listings of drug products. I extracted key information about individual drug listings e.g., title, product, country of origin, vendor and price. 

For example, vendor ID was extracted using code similar to below:

```python
# prepare the soup
soup = BeautifulSoup(current_listing, 'html.parser')

# find vendor info.
temp = soup.find_all("div", "seller-info text-muted")[0]
vendor = temp.find_all("a")[0].string
```

The cleaning process was hampered by occasional changes in website and HTML formatting across the timeline of the archives, as well as by the sheer volume of listings. However, I managed to develop a relatively concise set of Python scripts to parse listings from both websites automatically.

## Sorting the Data

For each date contained in the archives, the extracted information was sorted into a dataframe (Pandas), and saved to .csv file. When data were extracted for the entire timeline, I loaded the resulting .csv files into a MySQL database for final storage.

An example of the type of listings extracted from the archive:

[TBD]

## Descriptive Analyses

I performed several descriptive analyses on the data, with a focus on the broad features of the distribution of drug listings e.g., country of origin, product type, and pricing.

For example, by sourcing where individual listings were 'Shipped From', we can illustrate the distribution of listings by country of origin. Perhaps not surprisingly, the US accounts for a large proportion of individual listings:

[TBD]
An image, located within /images

![an image alt text]({{ site.baseurl }}/images/image_preview.png "an image title")

## Pricing Behavior

A pharmaceutical of particular interest to researchers at Epidemico is Alprazolam ('Xanax'). Why....2 sentence....US, UK, Germany, Australia

![an image alt text]({{ site.baseurl }}/images/image_preview.png "an image title")

## Summary
I successfully cleaned and sorted a large archive of DarkNet drug sales listings, and analyzed a number of features of the archive. 

Numerous large-scale DarkNet marketplaces are still in active operation (e.g., AlphaBay). By developing a database and tools to study such marketplaces, I have provided a valuable resource upon which Epidemico and their clients can base their investigation of currently active marketplaces.
<!--more-->
