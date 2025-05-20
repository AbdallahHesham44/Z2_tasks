# Download Bourns Datasheets Notebook

This Jupyter Notebook (`dawonloadPDFs.ipynb`) automates the process of:

- Scraping the [Bourns Obsolete Data Sheets](https://bourns.com/resources/obsolete-data-sheets) webpage for PDF datasheet links.
- Downloading all datasheets, or specifically the "PTE Series" datasheet, to a local folder (`bourns_datasheets`).
- Optionally downloading the PFAS Declaration PDF.
- Searching downloaded PDF files for specific keywords using `PyPDF2`.

## Usage

1. **Install dependencies**  
   Run in your terminal:
   ```sh
   pip install requests beautifulsoup4 PyPDF2
   ```

2. **Run the notebook**  
   Open `dawonloadPDFs.ipynb` in Jupyter or VS Code and execute the cells.

3. **Customize search**  
   - Change the `word` and `code` variables to search for different terms in the PDFs.
   - Adjust the PDF link selector or filtering logic as needed.

## Notes

- Downloads are saved in `D:\python-env\z2\bourns_datasheets`.
- The notebook prints status messages for each download and search operation.
- Make sure you have write permissions to the target directory.

---
