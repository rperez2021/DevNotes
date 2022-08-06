## General Info

## Command Line Automation

```python
#! python3
# mapIt.py - Launches a map in the browser using an address from the
# command line or clipboard.

import webbrowser, sys, pyperclip
if len(sys.argv) > 1:
    # Get address from command line.
    address = ' '.join(sys.argv[1:])
else:
    # Get address from clipboard.
    address = pyperclip.paste()

webbrowser.open('https://www.google.com/maps/place/' + address)
```

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

## Selenium

```python
from selenium import webdriver
browser = webdriver.Firefox()
browser.get('https://automatetheboringstuff.com')
elem = browser.find_element_by_css_selector('#css-selector > path > goes > here')
elem.click()
elems = browser.find_elements_by_css_selector('p')
```

`.send_keys('type whatever u want here')` method is for writing in fields

`.submit()` - automatically submits the active form field

`.back()` , `.forward()` , `.reload()` - basic browser functions
