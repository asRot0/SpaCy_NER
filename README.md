# 🚀 Named Entity Recognition (NER) with spaCy

This project performs **Named Entity Recognition (NER)** using **spaCy**, web scrapes text from Wikipedia, and visualizes extracted entities using **displaCy**, Matplotlib, and Rich tables.

---

## 📌 Features
- 🔹 **NER on Sample Text** using `en_core_web_sm`
- 🔹 **Web Scraping Wikipedia** for real-world text
- 🔹 **Organizing Extracted Entities** into a dictionary
- 🔹 **Visualizing Entity Frequencies** with Matplotlib
- 🔹 **Beautiful Rich Table Output** for structured display
- 🔹 **Entity Rendering with displaCy** (see below)

---

## 📥 Installation
```bash
pip install spacy beautifulsoup4 requests matplotlib rich
python -m spacy download en_core_web_sm
```

## 📝 Code Overview

### 1️⃣ Load Pre-trained Model & Run NER
```bash
import spacy
NER = spacy.load("en_core_web_sm")

text = "Apple is looking at buying a U.K. startup for $1 billion."
doc = NER(text)

for ent in doc.ents:
    print(f"{ent.text} -> {ent.label_}")
```

### 2️⃣ Web Scrape a Wikipedia Article
```bash
import requests
from bs4 import BeautifulSoup

url = 'https://en.wikipedia.org/wiki/Wikipedia'
response = requests.get(url)
soup = BeautifulSoup(response.text, "html.parser")

article_text = " ".join([p.text for p in soup.find_all("p")])
```

### 3️⃣ Perform NER on Scraped Text
```bash
doc = NER(article_text)
```

### 4️⃣ Visualize Named Entities with displaCy
```bash
from spacy import displacy
displacy.render(doc, style='ent', jupyter=True)
```

### 5️⃣ Entity Frequency Visualization
```bash
import matplotlib.pyplot as plt

entity_counts = {key: len(set(value)) for key, value in entity_dict.items()}
plt.figure(figsize=(10, 5))
plt.bar(entity_counts.keys(), entity_counts.values(), color='cornflowerblue')
plt.xlabel("Entity Type", fontsize=12, fontweight='bold')
plt.ylabel("Count", fontsize=12, fontweight='bold')
plt.title("NER Distribution", fontsize=14, fontweight='bold')
plt.xticks(rotation=45)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()
```

### 6️⃣ Rich Table Output
```bash
from rich.console import Console
from rich.table import Table

console = Console()
table = Table(title="🔵 Named Entity Recognition Results", title_style="bold cyan")
table.add_column("🔹 Entity Type", style="bold deep_sky_blue3", justify="center")
table.add_column("🔸 Entities", style="bold light_slate_grey", justify="left")

for entity_type, values in entity_dict.items():
    table.add_row(f"[bold bright_white]{entity_type}[/bold bright_white]", f"[italic dark_sea_green3]{', '.join(set(values))}[/italic dark_sea_green3]")

console.print(table)
```

### 🎨 displaCy Visualization Example

displaCy is a built-in visualization tool in spaCy that renders named entities in a user-friendly format.
<!-- Example HTML Output -->
Apple <span style="background-color: #ffeb3b; padding: 3px; border-radius: 3px;">ORG</span> 
is looking at buying a U.K. <span style="background-color: #8bc34a; padding: 3px; border-radius: 3px;">GPE</span> 
startup for $1 billion <span style="background-color: #03a9f4; padding: 3px; border-radius: 3px;">MONEY</span>.


#### 🔗 Try it in Jupyter Notebook with:
```bash
displacy.render(doc, style='ent', jupyter=True)
```