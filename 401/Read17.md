# Web Scraping

Web scraping is a technique to automatically access and extract large amounts of information from a website, which can save a huge amount of time and effort.

## How To Scrap

### Inspect the website

In the browser, we can use inspection to find the HTML tag we need and we can use the arrow on the top left corner of inspection box to choose the part we need.

### Code

* we need to import some libraries as the following:

```python
import requests
import urllib.request
import time
from bs4 import BeautifulSoup
```

* Then we access the website link with request library:

```python
url = 'http://web.mta.info/developers/turnstile.html'
response = requests.get(url)
```

* We will get a 200 response if the connection was established.

* Then we parse the HTML file using BeautifulSoup library, to get a better looking HTML.

```python
soup = BeautifulSoup(response.text, “html.parser”)
soup.findAll('a')
```

we can locate any tag we need using `findAll()`

* Choose the located  link using:

```python
one_a_tag = soup.findAll(‘a’)[38]
link = one_a_tag[‘href’]
```

* Now the file is downloaded to our variable link 
we can also download the link using request library by the following code:

```python
download_url = 'http://web.mta.info/developers/'+ link
urllib.request.urlretrieve(download_url,'./'+link[link.find('/turnstile_')+1:])
```

* After that, we set a timer to stop scraping for a second so that we are not spamming the website with requests. This helps us avoid getting flagged as a spammer, using:
`time.sleep(1)`

* We also can download an entire set of data with for loop, as the following code:

```python
import requests
import urllib.request
import time
from bs4 import BeautifulSoup

# Set the URL you want to webscrape from
url = 'http://web.mta.info/developers/turnstile.html'

# Connect to the URL
response = requests.get(url)

# Parse HTML and save to BeautifulSoup object¶
soup = BeautifulSoup(response.text, "html.parser")

# To download the whole data set, let's do a for loop through all a tags
line_count = 1 #variable to track what line you are on
for one_a_tag in soup.findAll('a'):  #'a' tags are for links
    if line_count >= 36: #code for text files starts at line 36
        link = one_a_tag['href']
        download_url = 'http://web.mta.info/developers/'+ link
        urllib.request.urlretrieve(download_url,'./'+link[link.find('/turnstile_')+1:]) 
        time.sleep(1) #pause the code for a sec
    #add 1 for next line
    line_count +=1
```

## Web Scrapping techniques

* Copy/Paste, which is manually copying and pasting data from a web page into a text file or spreadsheet.
* Text pattern matching, based on the UNIX grep command or regular expression-matching facilities of programming languages.
* HTTP programming, posting HTTP requests to the remote web server using socket programming.
* HTML parsing, as we did in the previous example.
* DOM parsing, By embedding a full-fledged web browser.
* Vertical aggregation, There are several companies that have developed vertical specific harvesting platforms. These platforms create and monitor a multitude of "bots" for specific verticals with no "man in the loop" (no direct human involvement), and no work related to a specific target site.
* Semantic annotation recognizing, The pages being scraped may embrace metadata or semantic markups and annotations, which can be used to locate specific data snippets.
* Computer vision web-page analysis, There are efforts using machine learning and computer vision that attempt to identify and extract information from web pages by interpreting pages visually as a human being might.
