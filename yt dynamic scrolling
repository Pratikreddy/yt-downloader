from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.by import By
import time

# Set up Chrome options for headless mode
chrome_options = Options()
#chrome_options.add_argument("--headless")
chrome_options.add_argument("--disable-gpu")
chrome_options.add_argument("--window-size=1920x1080")

# Initialize the Chrome driver with options
service = Service(ChromeDriverManager().install())
driver = webdriver.Chrome(service=service, options=chrome_options)

# Open the YouTube page
driver.get("https://www.youtube.com/@DanaWang/shorts")  # Replace with your desired link

# Scroll down to load more content
last_height = driver.execute_script("return document.documentElement.scrollHeight")
while True:
    driver.execute_script("window.scrollTo(0, document.documentElement.scrollHeight);")
    time.sleep(5)  # Wait for new content to load
    new_height = driver.execute_script("return document.documentElement.scrollHeight")
    if new_height == last_height:
        break
    last_height = new_height

# Extract all links
links = driver.find_elements(By.TAG_NAME, 'a')
urls = [link.get_attribute('href') for link in links if link.get_attribute('href')]

# Save the URLs to a text file
file_path = r'/Users/p/Desktop/links2.txt'  # Change to your desired path
with open(file_path, 'w', encoding='utf-8') as file:
    for url in urls:
        file.write(f"{url}\n")
print(f'URLs saved to {file_path}')

driver.quit()
