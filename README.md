# Flipkart Web Scraping Project
![Flipkart  image](https://github.com/user-attachments/assets/25089333-7774-4c94-a6d7-fc1c1aef2e80)


## **web scraped dataset file link:** [mobiles_dataset](https://github.com/RapoluSomesh/Flipkart_web_scraping_project/blob/main/mobiles_dataset.csv)

## **web scraped jupyter notebook file link:** [web scraping python](https://github.com/RapoluSomesh/Flipkart_web_scraping_project/blob/main/webscraping%20python.ipynb)

```python
import requests
import pandas as pd
from bs4 import BeautifulSoup
import re
```
```python
url = 'https://www.flipkart.com/search?q=samsung&sid=tyy%2C4io&as=on&as-show=on&otracker=AS_QueryStore_OrganicAutoSuggest_2_3_na_na_ps&otracker1=AS_QueryStore_OrganicAutoSuggest_2_3_na_na_ps&as-pos=2&as-type=RECENT&suggestionId=samsung%7CMobiles&requestId=d60111c4-4d88-4ed9-b97d-8822422cf58a&as-backfill=on&page=1'
```
```python
response = requests.get(url)
response
```
```python
soup = BeautifulSoup(response.content, 'html.parser')
print(soup.prettify())
```
```python
# data of product name
name = soup.find_all('div',class_='KzDlHZ')
names=[]
for i in name[0:20]:
    data = i.get_text()
    names.append(data)
# data of final price details
price = soup.find_all('div',attrs={'class':'Nx9bqj _4b5DiR'})
prices=[]
for i in price[0:20]:
    data=i.get_text()
    numeric_price = re.sub(r'[^\d]', '', data)
    prices.append(numeric_price)
# data of ram details
ram = soup.find_all('li',class_='J+igdf')
rams=[]
for i in ram[0:20]:
    data=i.get_text()
    rams.append(data)
# data of rating details
rating = soup.find_all('div',class_='XQDdHH')
ratings=[]
for i in rating[0:20]:
    data=i.get_text()
    ratings.append(data)
# data of discount details
discount = soup.find_all('div',class_='UkUFwK')
discounts=[]
for i in discount[0:20]:
    data=i.get_text()
    discounts.append(data)
# data of real price
real_price = soup.find_all('div',class_='yRaY8j ZYYwLA')
real_prices=[]
for i in real_price[0:20]:
    data=i.get_text()
    numeric_price = re.sub(r'[^\d]', '', data)
    real_prices.append(numeric_price)
# link of the products
link = soup.find_all('a',class_='CGtC98')
links=[]
for i in link[0:20]:
    data='https://www.flipkart.com'+i['href']
    links.append(data)
df=pd.DataFrame()
df['names']=names
df['links']=links
df['ratings']=ratings
df['real_price']=real_prices
df['discounts']=discounts
df['final_price']=prices
df
```

# CONCLUSION
This project successfully demonstrates the application of web scraping techniques to extract and structure product data from Flipkart. By utilizing Python libraries such as requests, BeautifulSoup, and pandas, essential product details like names, prices, discounts, ratings, and product links were efficiently gathered and organized into a user-friendly format.

The project highlights the practical value of web scraping for real-time data collection, which can be leveraged for market analysis, competitive research, and trend forecasting. It also emphasizes the importance of data extraction and structuring skills in enabling data-driven decision-making in e-commerce and retail analytics. This approach provides businesses with valuable insights into consumer preferences and market trends, contributing to more informed strategies and better outcomes.
