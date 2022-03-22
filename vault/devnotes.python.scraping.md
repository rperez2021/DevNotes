---
id: d5nvr7f85mdrbu24x9706r5
title: Scraping
desc: 'Notes on Python Web Scraping'
updated: 1647983088387
created: 1647982605410
---
## General Info

## Beautiful Soup

An html parsing module

Example usage:

```python
import bs4, requests

def getAmazonPrice(productURL):
    res = requests.get(productURL)
    res.raise_for_status()

    soup = bs4.BeautifulSoup(res.text, 'html.parser')
    elems = soup.select('#css-selector > path > goes > here')
    return elems[0].text.strip()
```
