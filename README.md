# Web Text Mining - NLP Assignment

A comprehensive Natural Language Processing project that demonstrates web scraping, text preprocessing, and various NLP techniques using Python.

## Overview

This project implements a complete text mining pipeline that:
1. Crawls and extracts content from Wikipedia pages
2. Applies various text preprocessing techniques
3. Performs linguistic analysis using NLP tools
4. Utilizes WordNet for semantic analysis

## Project Structure

```
web_text_mining/
├── web_text_mining (1).ipynb   # Main Jupyter notebook with implementation
├── Assignment .pdf              # Assignment requirements
├── report.docx                  # Project report
└── README.md                    # This file
```

## Features

### 1. Web Crawler
- Scrapes Wikipedia pages using BeautifulSoup
- Extracts main content from article body
- Example implementation: Albert Einstein Wikipedia page

### 2. Text Preprocessing
The project implements multiple preprocessing techniques:
- **Punctuation Removal**: Cleans special characters from text
- **Lowercase Conversion**: Normalizes text to lowercase
- **Stopword Removal**: Filters common words using NLTK stopwords
- **Stemming**: Reduces words to root form using Porter Stemmer
- **Lemmatization**: Converts words to dictionary base form using WordNet Lemmatizer

### 3. Tokenization
- Uses NLTK's `word_tokenize` for breaking text into individual tokens
- Handles complex text structures and punctuation

### 4. Parse Tree Generation
- Utilizes spaCy for dependency parsing
- Visualizes grammatical structure of sentences
- Supports both server mode and Jupyter notebook rendering

### 5. Part-of-Speech (POS) Tagging
- Tags each word with its grammatical category
- Uses spaCy's pre-trained English model (`en_core_web_sm`)
- Returns tuples of (word, POS_tag)

### 6. Named Entity Recognition (NER)
- Identifies and classifies named entities in text
- Recognizes: persons, organizations, locations, dates, etc.
- Example output: `('Apple Inc.', 'ORG')`, `('Steve Jobs', 'PERSON')`

### 7. WordNet Integration

#### a. Synonym Finding
- Extracts all synonyms for each word in the text
- Filters out stopwords from results
- Uses WordNet synsets for comprehensive synonym lists

#### b. Hypernym and Hyponym Relations
- **Hypernyms**: More general terms (e.g., "vehicle" is hypernym of "car")
- **Hyponyms**: More specific terms (e.g., "sedan" is hyponym of "car")
- Provides complete lexical hierarchy for each word

#### c. Semantic Distance
- Calculates shortest path distance between words in WordNet
- Uses synset relationships to determine semantic proximity
- Returns numerical distance values (lower = more related)

### 8. Word Similarity
- Computes Wu-Palmer similarity between word pairs
- Returns similarity score (0.0 to 1.0)
- Based on depth of common ancestors in WordNet taxonomy

## Dependencies

Install required packages:

```bash
pip install requests beautifulsoup4 nltk spacy
python -m spacy download en_core_web_sm
```

### Required NLTK Data
```python
nltk.download('stopwords')
nltk.download('wordnet')
nltk.download('punkt')
nltk.download('averaged_perceptron_tagger')
```

## Usage

### 1. Web Scraping
```python
from bs4 import BeautifulSoup
import requests

name_to_search = "Albert_Einstein"
result = get_wikipedia_body(name_to_search)
```

### 2. Text Preprocessing
```python
cleaned_text, no_stop_text, stemmed_text, lemmatized_text = preprocess_text(original_text)
```

### 3. Tokenization
```python
tokens = tokenize_text(preprocessed_text)
```

### 4. Parse Tree Visualization
```python
parse_tree = generate_parse_tree(text)
displacy.render(parse_tree, style='dep', jupyter=True)
```

### 5. POS Tagging
```python
pos_tags = pos_tagging(text)
# Output: [('This', 'PRON'), ('is', 'AUX'), ('example', 'NOUN'), ...]
```

### 6. Named Entity Recognition
```python
entities = named_entity_recognition(text)
# Output: [('Albert Einstein', 'PERSON'), ('Germany', 'GPE'), ...]
```

### 7. Finding Synonyms
```python
synonyms = get_synonyms(text)
# Returns dictionary: {word: [list_of_synonyms]}
```

### 8. Finding Relations (Hypernyms/Hyponyms)
```python
relations = get_relations(text)
# Returns: {word: {'synonyms': [...], 'hypernyms': [...], 'hyponyms': [...]}}
```

### 9. Semantic Distance
```python
distance = semantic_distance_between_words("theory", "relativity", text)
# Output: 2 (lower values indicate closer semantic relationship)
```

### 10. Word Similarity
```python
similarity = word_similarity_between_words("theory", "relativity", text)
# Output: 0.9 (scale 0.0 to 1.0, higher = more similar)
```

## Example Results

### Preprocessing Example
**Original Text:**
```
This is an example sentence with punctuation, stopwords, and various words.
```

**After Cleaning (lowercase):**
```
this is an example sentence with punctuation, stopwords, and various words.
```

**Without Stopwords:**
```
example sentence punctuation, stopwords, various words.
```

**After Stemming:**
```
exampl sentenc punctuation, stopwords, variou words.
```

**After Lemmatization:**
```
example sentence punctuation, stopwords, various words.
```

### Semantic Analysis Example
Using the Albert Einstein Wikipedia page:

**Semantic Distance:**
- "theory" and "relativity": 2 (closely related)
- "albert" and "einstein": 7
- "albert" and "physics": 10

**Word Similarity:**
- "theory" and "relativity": 0.9 (highly similar)
- "albert" and "einstein": 0.57
- "albert" and "physics": 0.375

## Technical Details

### Preprocessing Pipeline
1. Text input → Lowercase conversion
2. → Stopword removal (English stopwords from NLTK)
3. → Stemming (Porter Stemmer algorithm)
4. → Lemmatization (WordNet Lemmatizer)
5. → Tokenization output

### NLP Models Used
- **spaCy**: `en_core_web_sm` - English language model for POS tagging, NER, and dependency parsing
- **NLTK**: Porter Stemmer, WordNet Lemmatizer, stopwords corpus
- **WordNet**: Lexical database for semantic relationships

## Assignment Context

This project was developed as part of a Natural Language Processing course assignment with the following objectives:
- Understand web scraping techniques
- Apply text preprocessing methods
- Implement various NLP analysis techniques
- Work with lexical databases (WordNet)
- Analyze semantic relationships between words

**Instructor:** Dr. Rasekh
**Institution:** Zand University

## Key Functions

| Function | Purpose |
|----------|---------|
| `get_wikipedia_body(name)` | Scrapes Wikipedia article content |
| `preprocess_text(text)` | Applies all preprocessing steps |
| `tokenize_text(text)` | Tokenizes text into words |
| `generate_parse_tree(text)` | Creates dependency parse tree |
| `pos_tagging(text)` | Tags parts of speech |
| `named_entity_recognition(text)` | Extracts named entities |
| `get_synonyms(text)` | Finds synonyms for all words |
| `get_relations(text)` | Extracts hypernym/hyponym relations |
| `semantic_distance_between_words(w1, w2, text)` | Calculates semantic distance |
| `word_similarity_between_words(w1, w2, text)` | Computes similarity score |

## Notes

- The project uses the Albert Einstein Wikipedia page as the primary example
- All preprocessing steps preserve intermediate results for comparison
- WordNet operations filter out stopwords for better results
- Parse tree visualization supports both server and Jupyter notebook modes

## License

This is an educational project developed for academic purposes.

## Author

Developed as part of NLP coursework at Zand University.
