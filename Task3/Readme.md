# Capacitor Specification Validator

A web scraping solution that validates electronic capacitor specifications against industry standards using Selenium and BeautifulSoup.

## 🔍 Overview
This tool:
1. Scrapes capacitor data from [FindChips.com](https://www.findchips.com)
2. Validates key specifications against expected values
3. Returns a clear validation report with ✅/❌ indicators

## 🛠️ Technical Stack
- **Python 3.x**
- **Selenium** (Headless Chrome for scraping)
- **BeautifulSoup** (HTML parsing)
- **Regex** (Pattern validation)

## ⚙️ Installation
1. Install requirements:
   ```bash
   pip install selenium beautifulsoup4
