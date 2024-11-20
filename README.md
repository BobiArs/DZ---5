import requests
from bs4 import BeautifulSoup

base_url = "http://books.toscrape.com/catalogue/page-{}.html"

book_titles = []

for page_num in range(1, 51):
    url = base_url.format(page_num)
    response = requests.get(url)

    if response.status_code != 200:
        print(f"Не вдалося отримати сторінку {page_num}")
        continue

    soup = BeautifulSoup(response.text, 'html.parser')

    articles = soup.find_all('article', class_='product_pod')

    for article in articles:
        title = article.h3.a['title']
        book_titles.append(title)

for title in book_titles:
    print(title)
