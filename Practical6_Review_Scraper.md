# Practical 6 — Review Scraper (Web Scraping)

## Cell 1 — Install Libraries
```python
!pip install requests beautifulsoup4 pandas
```

## Cell 2 — Import Libraries
```python
import requests
from bs4 import BeautifulSoup
import pandas as pd
```

## Cell 3 — Send Request
```python
url = "http://books.toscrape.com/"
headers = {"User-Agent": "Mozilla/5.0"}
response = requests.get(url, headers=headers)
print("Status Code:", response.status_code)
```

## Cell 4 — Scrape Data
```python
soup = BeautifulSoup(response.content, 'html.parser')

titles = []
ratings = []
prices = []

rating_map = {'One': 1, 'Two': 2, 'Three': 3, 'Four': 4, 'Five': 5}

books = soup.find_all('article', class_='product_pod')

for book in books:
    title = book.find('h3').find('a')['title']
    titles.append(title)
    rating_word = book.find('p', class_='star-rating')['class'][1]
    rating = rating_map.get(rating_word, 0)
    ratings.append(rating)
    price = book.find('p', class_='price_color').text.strip()
    prices.append(price)

print(f"Total books scraped: {len(titles)}")
```

## Cell 5 — Show as DataFrame
```python
df = pd.DataFrame({
    'Book Title': titles,
    'Rating (out of 5)': ratings,
    'Price': prices
})
print(df.shape)
df.head(10)
```

## Cell 6 — Save to CSV
```python
df.to_csv(r'C:\Users\DELL\Downloads\book_reviews.csv', index=False)
print("Saved successfully!")
```
