# 📄 PDF Validation Assignment — z2data

## 📚 Overview

This project is a simple Python-based solution for downloading a PDF file for any electronic component (e.g., **PTE Series**) and validating its content to ensure the file is correct.

The validation is done by extracting key data from the PDF file and checking for specific expected content.

---

## 📌 Task Details
- **Created** the Save Directory
- **Fetched the Webpage** Defined the URL: https://bourns.com/resources/obsolete-data-sheets.
- **Download** a PDF file for a given component (example: **PTE Series**).
- **Read** and extract the content of the PDF file.
- **Search for validation data** inside the PDF, such as:
  - Component part numbers
  - Series name
  - Manufacturer name
  - Any other identifiable information ,I used resistor standard code and the resistor value 
- **Confirm** the PDF is valid by checking if expected data exists.

---

## 🛠️ Libraries I Used

* `requests` — to send HTTP requests and download the PDF file.
* `BeautifulSoup` — to parse and scrape the HTML content from the target web page.
* `os` — to manage file paths and handle file operations when saving the downloaded PDF.
* `PyPDF2` — to read and extract text from PDF files.

---

## 📂 What I Did

* Checked if the directory `D:\python-env\z2\bourns_datasheets` exists.
* If the directory does not exist, created it using `os.makedirs()`.
---
## 🌐 Web Scraping Steps

* Defined the URL of the target page: `https://bourns.com/resources/obsolete-data-sheets`.
* Set custom headers to mimic a real browser using `User-Agent`.
* Sent an HTTP GET request to fetch the page content using `requests`.
* Parsed the HTML content of the response using `BeautifulSoup`.

---
## 🔗 Extracting PDF Links

* Created an empty list called `datasheet_links`.
* Used `BeautifulSoup` to select all `<a>` tags with `href` attributes containing `.pdf`.
* For each PDF link found:
  * Retrieved the link text and URL.
  * Added both to the `datasheet_links` list as a tuple.
  * Printed the link text and URL to the console.
---
## 📥 Downloading the PTE Series PDF

* Looping through the `datasheet_links` list to find the PDF with the name `PTE Series`.
* When found:
  * Sent an HTTP GET request to download the PDF file.
  * Defined the file path as `bourns_datasheets/PTE Series.pdf`.
  * Opened a new file in binary write mode (`'wb'`) and wrote the PDF content into it.
  * Printed a confirmation message after successfully downloading.
* Added error handling with a `try-except` block to catch and display any download errors.
---
## 📝 Validating PDF Content

* Defined the target keyword to search for: `'1K ohms to 1 megohm'`.
* Defined a resistance code: `'103'`.
* Opened the downloaded PDF file in binary read mode (`'rb'`).
* Used `PyPDF2` to read the PDF file and extract text from each page.
* Loop through each page:
  * Checked if the target word exists in the page text.
  * If found, set a `found` flag to `True` and broke the loop.
* Printed a message indicating whether the word was found in the PDF.
* Also printed whether the associated resistance code is valid based on the result.

## 📦 How to Run

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd <your-project-folder>
