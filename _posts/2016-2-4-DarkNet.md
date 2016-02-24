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

The first task was to extract from the archives all HTML files related to product listings, ignoring configuration files, image files, etc. In total, the dataset contained approximately 20GB of raw HTML, with over 500,000 product listings.

I navigated individual pages using Beautiful Soup, a standard Python package for processing HTML, searching for listings of drug products. I extracted key information about individual drug listings (e.g., product, country of origin, vendor, price, etc.). 

For example, vendor ID was extracted using code similar to below:

```python
# prepare the soup
soup = BeautifulSoup(current_listing, 'html.parser')

# find vendor info.
temp = soup.find_all("div", "seller-info text-muted")[0]
vendor = temp.find_all("a")[0].string
```

Aside from the sheer volume of raw HTML to be processed, cleaning was hampered by factors such as: 
- large changes in website formatting across the timeline of the archives
- a lack of detailed drug labeling and categorization at the level of the raw HTML

In the end, I managed to develop a relatively concise set of Python scripts that parsed the archives automatically.

## Sorting the Data

For each date contained in the archives, the extracted information was then sorted into a dataframe (Pandas), and saved to .csv file. When data were extracted for the entire timeline, I loaded the resulting .csv files into a MySQL database for final storage.

The archive contains listings of very many drug types and from thousands of vendors. To focus on a particular drug, we can extract listings that include text matches to a given product or for a given date, for example, and from there do additional post-processing or analyses. An example of the type of listings extracted from the archive:

![Example drug listings]({{ site.baseurl }}/images/table1.png "Example drug listings")

## Descriptive Analyses

I performed several descriptive analyses on the data, with a focus on the broad features of the distribution of drug listings e.g., country of origin, product type, and pricing.

For example, by sourcing where individual listings were 'Shipped From', we can illustrate the distribution of listings by country of origin. Perhaps not surprisingly, the US accounts for a large proportion of individual listings:

![Listings origin]({{ site.baseurl }}/images/fig3_mod.png "Listings origin")

## Summary
I successfully cleaned and sorted a large archive of DarkNet drug sales listings. Numerous large-scale DarkNet marketplaces are still in active operation (e.g., AlphaBay). By developing a database and tools to study such marketplaces, I have provided a valuable resource upon which Epidemico and their clients can base investigation of currently active marketplaces.
<!--more-->
