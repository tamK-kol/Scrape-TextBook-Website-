# Scrape-TextBook-Website-
##Overview
This Python script is designed to scrape book data from the website "https://books.toscrape.com/" and store it in a CSV file named "Books.csv". It utilizes the web grabbing client and HTML parsing capabilities of the urllib and BeautifulSoup libraries, respectively.

## Prerequisites
Before running the script, ensure that you have the required libraries installed. You can install them using the following command:

pip install beautifulsoup4

## Usage
Clone the repository or download the script directly.
Open the script in a Python environment.

# import web grabbing client and HTML parser
from urllib.request import urlopen as uReq
from bs4 import BeautifulSoup as soup
import csv

# variable to store website link as a string
myurl = "https://books.toscrape.com/"

# grab website and store it in the variable uclient
uClient = uReq(myurl)

# read and close HTML
page_html = uClient.read()
uClient.close()

# call BeautifulSoup for parsing
page_soup = soup(page_html, "html.parser")

# grabs all the products under the list tag
bookshelf = page_soup.findAll("li", {"class": "col-xs-6 col-sm-4 col-md-3 col-lg-3"})

# create a CSV file of all products
filename = "Books.csv"
f = open(filename, "w")
headers = "Book title, Price\n"
f.write(headers)

for books in bookshelf:
    # collect title of all books
    book_title = books.h3.a["title"]
    
    # collect book price of all books
    book_price = books.findAll("p", {"class": "price_color"})
    price = book_price[0].text.strip()
    
    print("Title of the book: " + book_title)
    print("Price of the book: " + price)
    
    f.write(book_title + "," + price + "\n")

f.close()

## Output
The script will print the title and price of each book on the console and store the data in a CSV file named "Books.csv" in the same directory as the script.

Note: Ensure that you comply with the terms of use of the website you are scraping and respect their robots.txt file. Web scraping may be subject to legal restrictions, and it is essential to review and adhere to the terms and conditions of the target website.

