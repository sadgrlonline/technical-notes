# Python

## Table of Contents
- [Install / Setup](#install)
- [Basic Syntax](#basic-syntax)
- [Array Manipulation](#array-manipulation)
- [Date and Time](#date-and-time)
- [Writing to a File](#writing-to-a-file)
- [Modules](#modules)
    - [Beautiful Soup & Requests](#beautiful-soup--requests)
	- [Pandas](#pandas)


## Install
```bash
# check what version is installed
python3 -V

# install pip
sudo apt install -y python3-pip

# install a pip package
pip3 install package_name

# install a python library manually (no pip)
# after cloning the repository, go to where setup.py is located
python3 setup.py install
```

## Basic Syntax

```python
# print to console
print("hello!")

# remove whitespace in string
text.strip()

# creating function
def my_function():
	# logic here

# calling function
my_function()

# if statement
if 5 > 3:
	print("true")
else:
	print("false")
```


## Array manipulation

```python
# create an array
my_array = []

# get length of array
len(my_array)

# push to array
array.append('item')

# loop through all items of array
for x in array:
	print(x)

# while loop - this one counts up to 20
page = 0
while page != 20:
	page = page + 1
	print(page)

```

## Date and time

```python
# import datetime
from datetime import datetime

# get current datetime
now = datetime.now()
print(now.strftime("%d/%m/%Y %H:%M:%S"))
```

## Writing to a File
```python
# replace 'w' with 'a' to append
f = open('file.txt', 'w', encoding="utf-8")
f.write("Testing...")
f.close()
```

## Modules

### Beautiful Soup & Requests

```python
# for webscraping
# pip install bs4
# pip install requests

# import BeautifulSoup
from bs4 import BeautifulSoup
import requests

url = website.com
link = requests.get(url)
site = BeautifulSoup(link.content, "html-parser")
```

### Pandas

```python
# for exporting cleanly to excel
# pip install pandas

# import pandas
import pandas as pd

# export to XLSX
df = pd.DataFrame(data).T
df.columns = ["Column 1, Column 2, Column 3"]
df.to_excel(excel_writer = "myfile.xlsx")
```

### PyMySQL
```python
# for connecting to a database
# pip install pymysql

# import pymysql
import pymysql

# establish db connection
connection = pymysql.connect(host="localhost", user="root", passwd="", database="jobs")
cursor = connection.cursor()

# submit to database
insert = "INSERT INTO table(col1, col2, col3, col4) values(%s, %s, %s, %s);"
cursor.execute(insert, (col1, col2, col3, col4))

# commit & close connection
connection.commit()
connection.close()
```