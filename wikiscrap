import requests
from bs4 import BeautifulSoup
import csv

# URL of the Wikipedia page with the quotes table
url = 'URL'

# Send a GET request to the URL
response = requests.get(url)
response.raise_for_status()  # Check for request errors

# Parse the HTML content using BeautifulSoup
soup = BeautifulSoup(response.content, 'html.parser')

# Find the table - this assumes it's the first table on the page
table = soup.find('table', {'class': 'wikitable sortable'})

# List to store the scraped data
scraped_data = []

# Iterate over each row in the table (skip the first row if it contains headers)
for row in table.find_all('tr')[1:]:
    # Find all the cells in the row
    cells = row.find_all('td')
    
    # Check if the row has enough cells to extract the needed data
    if len(cells) >= 6:
        
        quote = cells[1].get_text(strip=True)  # Assuming 'Quotation' is the 2nd cell
        
        # Remove any existing quotes surrounding the quote text
        quote = quote.strip('""')  # Remove extra quotation marks
        
        film = cells[4].get_text(strip=True)   # Assuming 'Film' is the 5th cell
        year = cells[5].get_text(strip=True)   # Assuming 'Year' is the 6th cell
        
        # Append the extracted data to the list
        scraped_data.append({"Quote": quote, "Movie": film, "Year": year})

# Write the scraped data to a CSV file
file_path = 'wikipedia_movie_quotes.csv'
with open(file_path, mode='w', newline='', encoding='utf-8') as file:
    writer = csv.DictWriter(file, fieldnames=["Quote", "Movie", "Year"])
    writer.writeheader()
    writer.writerows(scraped_data)

print(f"Data has been written to {file_path}")
