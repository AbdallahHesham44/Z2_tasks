# Capacitor Specification Validator

## 📝 Description
A Python script that scrapes and validates capacitor specifications from electronic component websites using Selenium and BeautifulSoup.

## 🛠️ Technologies Used
```python
from selenium import webdriver            # Web automation
from selenium.webdriver.chrome.service import Service  # ChromeDriver service
from selenium.webdriver.chrome.options import Options  # Browser options
from bs4 import BeautifulSoup            # HTML parsing
import time                              # Delays
import re                                # Regular expressions
```
## 🚀 Features
Web scraping of capacitor specifications

Automatic validation against industry standards

Clear pass/fail reporting with visual indicators (✅/❌)

| Specification  | Validation Pattern               | Example         |
|---------------|----------------------------------|-----------------|
| **Type**      | Exact match to expected types    | `Ceramic Capacitor` → ✅ |
| **Voltage**   | `^\d+V$` regex                   | `50V` → ✅       |
| **Tolerance** | `^\d+% [±]Tol$` regex            | `10% +Tol` → ✅  |
| **Dielectric**| Match to expected dielectrics    | `X7R` → ✅       |
| **Capacitance**| `^\d*\.?\d+(uF\|nF\|pF)$` regex | `10uF` → ✅      |
| **Size**      | 4-digit size code                | `0603` → ✅      |




