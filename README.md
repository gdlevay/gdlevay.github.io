# How Do Media Headlines Actually Deceive Us?

#### Misinformation, Disinformation, and Fake News are all words that are thrown around in our current society. Many people claim that it is obvious whether a news article is misleading or not. Even more people will claim that the article is misleading due to its content. I set out to use data to answer some of these questions.

# 1. Data

#### The most important part of answering these questions is gathering enough data to draw a clear picture of the present trends.

### 1.1 Large Data Issue Solution

#### There are challenges working with large data, the first challenge is that it can be hard to analyze at once due to memory limitations in Python/Pandas. To address this first issue, I converted the large CSV file to a DB file using SQL Connections.

```
import csv
import sqlite3
csv.field_size_limit(100000000)

connection = sqlite3.connect('data/news.db')
cursor = connection.cursor()

create_table = '''
CREATE TABLE news(
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    id1 TEXT NOT NULL,
    id2 TEXT NOT NULL,
    date TEXT NOT NULL,
    year TEXT NOT NULL,
    month TEXT NOT NULL,
    day TEXT NOT NULL,
    author TEXT NOT NULL,
    title TEXT NOT NULL,
    article TEXT NOT NULL,
    url TEXT NOT NULL,
    section TEXT NOT NULL,
    publication TEXT NOT NULL
    );'''
cursor.execute(create_table)

file = open('data/all-the-news-2-1.csv', encoding = 'utf-8')

contents = csv.reader(file)

insert_records = "INSERT INTO news (id1,id2,date,year,month,day,author,title,article,url,section,publication) VALUES(?,?,?,?,?,?,?,?,?,?,?,?)"

cursor.executemany(insert_records, contents)
select_all = "SELECT * FROM news"
rows = cursor.execute(select_all).fetchall()
connection.commit()
connection.close()

```

By converting the contents of a CSV file to a DB file, I am able to manipulate the data much more effectively using SQL commands.

### 1.2 Filter Publishers

#### I decided to focus on 6 publishers for this project: 3 publishers assoociated with misleading content (Buzzfeed, Vox, and Vice) and 3 publishers associated with political leaning (CNN, Fox, The Hill). After some additional data cleaning I ended up with a dataset that contained over 320k separate articles. To do this, I wrote a combination of Python and SQL command to filter the original 2M record database to only include the publishers of interest.

```
connection = sqlite3.connect('../data/news.db')
media_list = ["CNN", "Fox News","Buzzfeed News", "Vox", "Vice", "The Hill"]
total_arts = pd.read_sql('SELECT title, article, date, url, publication, section FROM news WHERE publication in ("CNN", "Fox News", "Buzzfeed News", "Vox", "Vice", "The Hill")', connection)

```


#### From these 30, I chose 6 publishers to look at: 3 publishers assoociated with misleading content (Buzzfeed, Vox, and Vice) and 3 publishers associated with political leaning (CNN, Fox, The Hill). After some additional data cleaning I ended up with a dataset that contained over 320k separate articles. The breakdown of the number of articles per publisher is shown below.

![Articles Per Publication](/docs/assets/art_per_pub.png)
