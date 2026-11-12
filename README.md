## Objectives

- Pull information from a web page with Python
- Write the scraped data to a CSV file

## Data Source

[Programming_Languages.html](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/labs/datasets/Programming_Languages.html): results of a salary survey of programming languages.

Fields scraped:

| Field | Description |
|---|---|
| Language | Name of the programming language |
| Created By | Creator(s) of the language |
| Average Annual Salary | Average annual salary (USD) |
| Learning Difficulty | How hard the language is to learn |

## Tools & Libraries

- Python 3
- [requests](https://pypi.org/project/requests/): downloads the web page
- [BeautifulSoup (bs4)](https://pypi.org/project/beautifulsoup4/): parses the HTML
- [pandas](https://pypi.org/project/pandas/): builds the DataFrame and exports the CSV

## How It Works

1. Download the HTML page with `requests.get(url)`
2. Parse it with `BeautifulSoup(data, "html.parser")`
3. Find the `<table>` and loop over its rows, skipping the header row
4. Take the language, creator, salary and difficulty from each row
5. Load the records into a pandas DataFrame
6. Save it to `popular-languages.csv`

```python
table = soup.find("table")
records = []
for row in table.find_all("tr")[1:]:
    cols = [td.get_text(strip=True) for td in row.find_all("td")]
    records.append(cols[1:5])

df = pd.DataFrame(records, columns=["Language", "Created By", "Average Annual Salary", "Learning Difficulty"])
df.to_csv("popular-languages.csv", index=False)
```

## Results

| Language | Created By | Average Annual Salary | Learning Difficulty |
|---|---|---|---|
| Python | Guido van Rossum | $114,383 | Easy |
| Java | James Gosling | $101,013 | Easy |
| R | Robert Gentleman, Ross Ihaka | $92,037 | Hard |
| Javascript | Netscape | $110,981 | Easy |
| Swift | Apple | $130,801 | Easy |
| C++ | Bjarne Stroustrup | $113,865 | Hard |
| C# | Microsoft | $88,726 | Hard |
| PHP | Rasmus Lerdorf | $84,727 | Easy |
| SQL | Donald D. Chamberlin, Raymond F. Boyce. | $84,793 | Easy |
| Go | Robert Griesemer, Ken Thompson, Rob Pike. | $94,082 | Difficult |

## How to Run

```bash
pip install requests beautifulsoup4 pandas
jupyter notebook Web-Scraping-Lab.ipynb
```

## Files

- `Web-Scraping-Lab.ipynb`: the notebook with the scraping code
- `popular-languages.csv`: the scraped output
