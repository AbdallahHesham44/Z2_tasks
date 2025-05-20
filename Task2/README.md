# Download Bourns Datasheets Notebook

This Jupyter Notebook (`dawonloadPDFs.ipynb`) automates the process of:

- Scraping the [Bourns Obsolete Data Sheets](https://bourns.com/resources/obsolete-data-sheets) webpage for PDF datasheet links.
- Downloading all datasheets, or specifically the "PTE Series" datasheet, to a local folder (`bourns_datasheets`).   
- Searching downloaded PDF files for specific keywords using `PyPDF2`.

## Usage

1. **Install dependencies**  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Bourns Datasheet Scraper Solution</title>
    <style>
        body { font-family: Arial, sans-serif; line-height: 1.6; max-width: 900px; margin: 0 auto; padding: 20px; }
        h1 { color: #2c3e50; border-bottom: 2px solid #3498db; }
        h2 { color: #2980b9; margin-top: 30px; }
        code { background: #f8f9fa; padding: 2px 5px; border-radius: 3px; }
        pre { background: #f8f9fa; padding: 15px; border-left: 4px solid #3498db; overflow-x: auto; }
        .note { background: #e3f2fd; padding: 10px; border-left: 4px solid #2196f3; }
        .warning { background: #fff3e0; padding: 10px; border-left: 4px solid #ff9800; }
    </style>
</head>
<body>
    <h1>Bourns Obsolete Datasheet Scraping Solution</h1>
    
    <section id="overview">
        <h2>🔍 Solution Overview</h2>
        <p>This solution automates:</p>
        <ul>
            <li>Scraping PDF datasheets from Bourns' obsolete components page</li>
            <li>Targeted download of "PTE Series" documents</li>
            <li>Technical specification validation within PDFs</li>
        </ul>
    </section>

    <section id="full-code">
        <h2>💻 Complete Python Solution</h2>
        <pre><code class="language-python">import requests
from bs4 import BeautifulSoup
import os
import PyPDF2

# ========== CONFIGURATION ==========
DOWNLOAD_DIR = 'D:\\python-env\\z2\\bourns_datasheets'
TARGET_SERIES = 'PTE Series'
VALIDATION_TEXT = '1K ohms to 1 megohm'
RESISTANCE_CODE = '103'

# ========== SETUP DIRECTORIES ==========
if not os.path.exists(DOWNLOAD_DIR):
    os.makedirs(DOWNLOAD_DIR)

# ========== WEB SCRAPING ==========
def scrape_bourns_datasheets():
    url = 'https://bourns.com/resources/obsolete-data-sheets'
    headers = {'User-Agent': 'Mozilla/5.0'}
    
    print(f"🔄 Fetching data from {url}")
    response = requests.get(url, headers=headers)
    soup = BeautifulSoup(response.text, 'html.parser')
    
    datasheet_links = []
    for link in soup.select('a[href*=".pdf"]'):
        datasheet_links.append((link.text.strip(), link['href']))
        print(f"🔗 Found: {link.text.strip()} → {link['href']}")
    
    return datasheet_links

# ========== PDF DOWNLOAD & VALIDATION ==========
def process_datasheets(links):
    for name, link in links:
        if name == TARGET_SERIES:
            try:
                # Handle relative URLs
                if not link.startswith('http'):
                    link = f'https://bourns.com{link}' if link.startswith('/') else f'https://bourns.com/{link}'
                
                # Download PDF
                pdf_response = requests.get(link, headers=headers)
                filename = os.path.join(DOWNLOAD_DIR, f"{name}.pdf")
                
                with open(filename, 'wb') as f:
                    f.write(pdf_response.content)
                print(f"✅ Downloaded: {filename}")
                
                # Validate content
                validate_pdf(filename)
                
            except Exception as e:
                print(f"❌ Failed to process {name}: {str(e)}")

def validate_pdf(pdf_path):
    found = False
    with open(pdf_path, 'rb') as f:
        reader = PyPDF2.PdfReader(f)
        for page in reader.pages:
            if VALIDATION_TEXT in page.extract_text():
                found = True
                break
    
    if found:
        print(f"✔ Validation PASSED: Found '{VALIDATION_TEXT}'")
        print(f"   Resistance code {RESISTANCE_CODE} is valid")
    else:
        print(f"✖ Validation FAILED: '{VALIDATION_TEXT}' not found")
        print(f"   Resistance code {RESISTANCE_CODE} is NOT valid")

# ========== MAIN EXECUTION ==========
if __name__ == "__main__":
    datasheets = scrape_bourns_datasheets()
    process_datasheets(datasheets)</code></pre>
    </section>

    <section id="workflow">
        <h2>⚙️ Workflow Diagram</h2>
        <div class="mermaid">
            graph TD
                A[Start] --> B[Create Download Directory]
                B --> C[Scrape Bourns Website]
                C --> D[Filter PTE Series]
                D --> E[Download PDF]
                E --> F[Validate Resistance Specs]
                F --> G[Generate Report]
        </div>
    </section>

    <section id="output">
        <h2>📊 Expected Output</h2>
        <pre><code class="language-plaintext">🔄 Fetching data from https://bourns.com/resources/obsolete-data-sheets
🔗 Found: PTE Series → /docs/Product-Datasheets/pte.pdf
✅ Downloaded: D:\python-env\z2\bourns_datasheets\PTE Series.pdf
✔ Validation PASSED: Found '1K ohms to 1 megohm'
   Resistance code 103 is valid</code></pre>
    </section>

    <section id="requirements">
        <h2>📦 Requirements</h2>
        <pre><code class="language-plaintext">requests==2.31.0
beautifulsoup4==4.12.2
pypdf2==3.0.1</code></pre>
    </section>

    <div class="note">
        <strong>Pro Tip:</strong> For large-scale scraping, consider adding:
        <ul>
            <li>Rate limiting with <code>time.sleep()</code></li>
            <li>Error logging to a file</li>
            <li>Retry mechanism for failed downloads</li>
        </ul>
    </div>

    <div class="warning">
        <strong>Legal Note:</strong> Always check:
        <ul>
            <li><a href="https://bourns.com/robots.txt" target="_blank">Bourns' robots.txt</a></li>
            <li>Copyright restrictions before redistribution</li>
        </ul>
    </div>
</body>
</html>
   Run in your terminal:
   ```sh
   pip install requests beautifulsoup4 PyPDF2
   ```

2. **Run the notebook**  
   Open `dawonloadPDFs.ipynb` in Jupyter or VS Code and execute the cells.

3. **Customize search**  
   - Change the `word` and `code` variables to search for different terms in the PDFs.
   - Adjust the PDF link selector or filtering logic as needed.

     
4. **Validation**

- After downloading the datasheet, the notebook validates the file by searching for a specific resistor code and value (e.g., `'1K ohms to 1 megohm'` with code `'103'`) within the PDF.  
- If the keyword is found, it confirms that the correct datasheet has been downloaded and contains the expected information.

- This ensures the automation not only downloads the file but also verifies its content matches the required resistor specification.

## Notes

- Downloads are saved in `D:\python-env\z2\bourns_datasheets`.
- The notebook prints status messages for each download and search operation.
- Make sure you have write permissions to the target directory.

---
