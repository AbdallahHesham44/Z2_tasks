# Download Bourns Datasheets Notebook

This Jupyter Notebook (`dawonloadPDFs.ipynb`) automates the process of:

- Scraping the [Bourns Obsolete Data Sheets](https://bourns.com/resources/obsolete-data-sheets) webpage for PDF datasheet links.
- Downloading all datasheets, or specifically the "PTE Series" datasheet, to a local folder (`bourns_datasheets`).   
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

     
4. **Validation**

- After downloading the datasheet, the notebook validates the file by searching for a specific resistor code and value (e.g., `'1K ohms to 1 megohm'` with code `'103'`) within the PDF.  
- If the keyword is found, it confirms that the correct datasheet has been downloaded and contains the expected information.

- This ensures the automation not only downloads the file but also verifies its content matches the required resistor specification.

## Notes

- Downloads are saved in `D:\python-env\z2\bourns_datasheets`.
- The notebook prints status messages for each download and search operation.
- Make sure you have write permissions to the target directory.

---
