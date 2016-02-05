---
layout: post
title: DarkNet | Tracking the underground drug trade
---

## Background and Problem

During my time at Insight, I carried out a consulting project in collaboration with researchers at epidemico.com, a Boston-based data science company working in the population health domain.

These days you can buy almost anything you want online. Unfortunately, in parallel to legitimate internet commerce, a network of underground sales channels have spawned into life over the past decade or so, with powerful pharmaceuticals and harder drugs forming a large proportion of sales listings. While many of these so called 'DarkNet' sites eventually succumb to law enforcement endeavours or internal fraud, numerous large-scale marketplaces still exist such as AlphaBay and East India Company. 

## The Dataset

The dataset consisted of an archive of sales listings from a popular, underground marketplaces known as 'Evolution'. Listings were scraped at semi-regular intervals between January 2014 and March 2015, and were downloaded in their original, raw HTML format from a publicly available archive [give link]
<http://www.gwern.net/Black-market%20archives>

[give example pic of HTML, and associated website page picture]

## Cleaning the Data

Parsing and cleaning data from approximately ~500,000 HTML listings requires mutliple processing tools and a little patience. I employed standard Python packages (e.g., Beautiful Soup, Pandas) to extract and organize relevant information from individual listings:

```# find vendor info.```
```temp = soup.find_all("div", "seller-info text-muted")[0]```
```vendor = temp.find_all("a")[0].string```

This process was hampered by changes in page format at a number of points in the site's history. The extracted information was sorted under relevant headings using 

[show example rows of dataframe

## Descriptive Analyses

## Summary
