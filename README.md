# Parsing-of-tables-in-python

To parse tables in Python, we have several libraries and tools at your disposal, each suited to different formats and use cases. Here's an overview:

1. Parsing HTML Tables:

pandas: The pandas library offers a convenient read_html() function that can extract tables directly from HTML content, whether from a URL or a local file.

import pandas as pd

url = 'https://example.com/page_with_table.html'
tables = pd.read_html(url)
df = tables[0]  # Select the first table
This approach is straightforward and efficient for well-structured HTML tables.

BeautifulSoup: For more complex HTML parsing tasks, BeautifulSoup from the bs4 library provides fine-grained control.

from bs4 import BeautifulSoup

with open('local_file.html') as file:
    soup = BeautifulSoup(file, 'html.parser')

table = soup.find('table')
rows = table.find_all('tr')
data = []
for row in rows:
    cols = row.find_all('td')
    cols = [ele.text.strip() for ele in cols]
    data.append(cols)
This method allows for detailed extraction and manipulation of HTML table data.

2. Parsing Tables from PDFs:

Camelot: Camelot is a Python library specifically designed for extracting tables from PDF files.

import camelot

tables = camelot.read_pdf('file.pdf')
df = tables[0].df  # Access the first table as a DataFrame
Camelot is effective for PDFs with clearly defined table structures. 
Camelot

3. Parsing Tables from Excel Files:

openpyxl: For Excel files (.xlsx), the openpyxl library allows you to read and write data.

from openpyxl import load_workbook

wb = load_workbook('file.xlsx')
sheet = wb.active
data = []
for row in sheet.iter_rows(values_only=True):
    data.append(row)
This approach is useful for handling Excel files with complex structures or when you need to manipulate the workbook at a low level.

4. Parsing Tables from Plain Text or Custom Formats:

Regular Expressions: For text files with tables in custom formats, Python's re module can be employed to parse the data.

import re

with open('file.txt') as file:
    content = file.read()

pattern = re.compile(r'Your regex pattern here')
matches = pattern.findall(content)
Regular expressions offer flexibility for parsing complex and irregular table structures.

5. Additional Resources:

table-parser: This is a simple Python program that demonstrates parsing HTML tables and related pages, extracting data into lists and dictionaries, and storing it in an SQLite database. 
GitHub

python-tabulate: The tabulate library is useful for pretty-printing tabular data in Python. It can format lists of lists, dictionaries, or other tabular data types into nicely formatted tables.
