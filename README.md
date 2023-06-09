Development Status :: 3 - Alpha <br>
*Copyright (c) 2023 MinWoo Park*
<br>

# Python Package: YouTuber
![YouTuber](https://img.shields.io/badge/pypi-youtuber-orange)
![Pypi Version](https://img.shields.io/pypi/v/youtuber.svg)
[![Contributor Covenant](https://img.shields.io/badge/contributor%20covenant-v2.0%20adopted-black.svg)](code_of_conduct.md)
[![Python Version](https://img.shields.io/badge/python-3.6%2C3.7%2C3.8-black.svg)](code_of_conduct.md)
![Code convention](https://img.shields.io/badge/code%20convention-pep8-black)
![Black Fomatter](https://img.shields.io/badge/code%20style-black-000000.svg)
![](https://github.com/DSDanielPark/youtuber/blob/main/doc/imgs/youtuber2.png)


Contains several useful features that can be used for youtube related projects.
This package is intended to provide useful features for video editing, including crawling through the YouTube Data API v3 and Selenium.

<br>

# Installation
```
pip install youtuber
```

<br>

# Quick Start
1. Install the Python package `youtuber` - `pip install youtuber`
2. Obtain an API key for YouTube Data API v3 from the following [link](https://console.cloud.google.com/apis/api/youtube.googleapis.com/credentials?project=sincere-canyon-278402) and enter it.
3. Enter the path of chromedriver.exe.
4. Enter the YouTube search keyword, the number of videos to crawl, and the number of comment pages to crawl.
5. Enter the full path of the CSV file to be saved after execution. If encoding issues arise, please save the returned pd.DataFrame object separately.


```python
from youtuber import AutoCrawler

DEVELOPER_KEY = "enter_your_dev_api_key"               # Enter your DEV API KEY at https://console.cloud.google.com/apis/api/youtube.googleapis.com/credentials?project=sincere-canyon-278402
CHOROME_PATH = r'C:\Program Files\chromedriver.exe'    # Enter path of 'chromdriver.exe' 

auto = AutoCrawler(DEVELOPER_KEY, CHOROME_PATH)
search_keyword = 'chatGPT'      # Youtube Search Keyword
max_link_len = 2                # How many videos you target to crawl?
max_comment_pg_len = 2          # How many comment pages you target to crawl?
save_path = './enter/any/path/result.csv'

df = auto.run(search_keyword, max_link_len, max_comment_pg_len, save_path)
```

<br>

# Tutorial
1. Main tutorial: https://github.com/DSDanielPark/youtuber/blob/main/docs/tutorial.ipynb
2. Sub tutorial folder: Tutorials for each function can be found in [this folder](https://github.com/DSDanielPark/youtuber/tree/main/docs). 


<br>

# Features
### 1. `YoutubeAPI`
Retrieve YouTube search results. <br>
You can get your 'Youtube Data API v3' key in [here](https://console.cloud.google.com/apis/api/youtube.googleapis.com/credentials?project=sincere-canyon-278402), and you can find some guide in [here.](https://developers.google.com/youtube/v3/getting-started?hl=ko)


```python
from youtuber import YoutubeAPI

DEVELOPER_KEY = "enter_your_api_key"
youtuber_v3 = YoutubeAPI(DEVELOPER_KEY)
links = youtuber_v3.get_links('chatGPT', 3) #YouTube Search Keyword = 'chatGPT', return 3 links.

links
['https://www.youtube.com/watch?v=xxxxx',
 'https://www.youtube.com/watch?v=xxxxx',
 'https://www.youtube.com/watch?v=xxxxx']
```

### 2. `YoutubeCrawler`
Retrieve comment data.
```python
from youtuber import YoutubeCrawler

chrome_driver = r'C:\Program Files\chromedriver.exe'
youtuber_crawl = YoutubeCrawler(chrome_driver)
df = youtuber_crawl.get_comment_df(links, 1) #if you enter 1, only 1 page of comments will be searched.

df #You can get pd.DataFrame object.
```


### 3. `AutoCrawler`
Due to dependency issues, the AutoCrawler class was created separately without inheritance, but it includes both the YoutubeAPI and YoutubeCrawler methods. The AutoCrawler class performs both search functionality via the Youtube Data API v3 and comment crawling via Selenium.


<br>

# References
[1] YouTube Data API v3: https://developers.google.com/youtube/v3/getting-started?hl=ko
 <br>
[2] Selenium python: https://selenium-python.readthedocs.io/

<br><br>


### `Important Warning:` All legal responsibilities associated with the use of the package lie with the user.
The Python package "youtuber" provides code for Python users to easily access data through the YouTube Data API v3 and Selenium. All licenses follow those of the API and dependent packages, and all responsibility for handling data and using the package lies with the user. There is no monetary compensation received for the use of this code, and it should be noted that there is no liability for the use of the code.
Please refer to the YouTube Data API page for more details.
https://developers.google.com/youtube/v3?hl=ko
