# Data Collection Challenge
> How can we collect data if we don't have access to affordable APIs or readily available CSVs to download?
## Folder Contents
- A `mars_news.ipynb` Notebook file that scrapes text from the [Mars Planet Science News site](https://static.bc-edx.com/data/web/mars_news/index.html).
- A `mars_weather.ipynb` Notebook file that scrapes text from the [Mars Temperature Data site](https://static.bc-edx.com/data/web/mars_facts/temperature.html) and does some minor text processing to make charts and visualizations.
- A `Results` folder containing the output of the Notebook files.
  - JSON file `mars_text.json` contains the titles and blurb text of the various articles scraped with the `mars_news.ipynb` Notebook.
  - CSV file `mars_weather.csv` contains the table data scraped with the `mars_weather.ipynb` Notebook.
- A `.gitignore` file that ignores common things like PyCache, Jupyter Notebook checkpoints, and other common gitignorable Python entities. 

### Installation/Prerequisites
- Make sure you can run Python. The development environment I used was set-up with:
```
conda create -n dev python=3.10 anaconda -y
```
#### Imported Modules
- Installing via the conda command given should give you access to most of the script's modules locally. Be sure to grab yourself the following libraries:
  - [Pandas](https://pandas.pydata.org/docs/getting_started/install.html) and [MatPlotLib](https://matplotlib.org/stable/users/installing/index.html) for your basic data manipulation and visualization.
  - [Splinter](https://splinter.readthedocs.io/en/latest/install/install.html) for automated browser actions. `pip install "splinter[selenium4]"` is the exact driver used for this project.
  - [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#installing-beautiful-soup) is your ~~webscraper~~ HTML/XML text parser and the star of this project.
    - [html5lib](https://pypi.org/project/html5lib/) and [lxml](https://pypi.org/project/lxml/) are dependencies Beautiful Soup uses to parse websites.

#### The Other Key Driver
- [ChromeDriver](https://splinter.readthedocs.io/en/latest/install/external.html) for enabling automation and all the magic the aforementioned modules will make.
  - NOTE: As the name may suggest, ChromeDriver and `splinter[selenium4]` work exclusively for the Google Chrome browser and this project is run strictly on the Google Chrome browser. You'll need to look elsewhere for other drivers and installation instructions if you choose to use another browser.

## Code Breakdown
As usual, most of the reasoning and coding techniques are discussed at length in the comments of the notebook files, so this part is more about the workflow of a HTML data collection project. It can roughly be broken down into these steps:
1. **Checking the Terms** ([BBC Terms of Use Example](https://www.bbc.co.uk/usingthebbc/terms/)) - Different sites can handle different amounts of traffic. Depending on what you do, you could accidentally DDoS a website with your sudden influx of HTTP requests, so be careful who you upset.
2. **Inspecting the Page** - By right clicking and clicking the Inspect option, you can see the public HTML layout of the webpage for yourself. Given how structured and formulaic most online content is, you should be able to find what you need under a consistent umbrella of HTML tags.
3. **Processing the Soup** - Once you find what you need, you can then collect the HTML text through BeautifulSoup and store its contents somewhere.

Generally, your data collection project would look like this:

```python
# Get to your page
browser = Browser("whateverBrowserYouUse")
browser.visit(someURL)

# Collect the big Soup
soup = BeautifulSoup(browser.html, "html.parser")

# Filter to get the data you want with smaller Soup bowls
subSoup = soup.select(someHTMLTag)

# Do stuff

# Close your automated browser
browser.quit()
```

![Scraping text data](https://cdn.discordapp.com/attachments/939673945240637450/1130937272922030190/image.png)

In this example, I scraped text data from articles.

![Scraping table data](https://cdn.discordapp.com/attachments/939673945240637450/1130937919738232923/image.png)

In this example, I scraped text data from tables.

What ultimately makes your project stand out depends on what you look for and how well you can select the content you need. For example, Sabrina Cruz used BeautifulSoup in order to programmatically scrape job site postings to figure out [why resume-writing is an abysmal experience](https://www.youtube.com/watch?v=Kpm8rEywBDQ).

## Resources that helped a lot
- Surprisingly, [Splinter](https://splinter.readthedocs.io/en/latest/browser.html) and [BeautifulSoup documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) are fairly easy to work with. Assuming you have experience with HTML code and CSS selectors, the code documentation is fairly intuitive and tells you how you can extract them in a straightforward manner.
- If you don't have HTML/CSS/JS experience, however, then a tutorial such as [Mosh's](https://www.youtube.com/watch?v=qz0aGYrrlhU) and frequent trips to [W3Schools](https://www.w3schools.com/css/css_selectors.asp) is strongly recommended.

## FINAL NOTES
> Project completed on July 6, 2023
