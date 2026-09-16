# Lesson 7 — Comprehensions, Lambda, map & filter

## 1. Overview

Python provides concise ways to transform and filter collections.

Important concepts:

* List comprehension
* Dictionary comprehension
* Nested comprehensions
* `lambda`
* `map()`
* `filter()`
* `sorted()` with `lambda`

These patterns are common in:

* Data preprocessing
* AI/ML pipelines
* RAG systems
* LLM response processing
* API data transformation
* Search result filtering

---

# 2. List Comprehension

A list comprehension provides a concise way to create a list.

Traditional loop:

```python
numbers = [1, 2, 3, 4, 5]

squares = []

for number in numbers:
    squares.append(number * number)
```

List comprehension:

```python
squares = [number * number for number in numbers]
```

Result:

```text
[1, 4, 9, 16, 25]
```

Basic pattern:

```python
[output for item in collection]
```

Read it as:

> Create `output` for every `item` in the collection.

---

# 3. List Comprehension with Condition

Traditional:

```python
even_numbers = []

for number in numbers:
    if number % 2 == 0:
        even_numbers.append(number)
```

Comprehension:

```python
even_numbers = [
    number
    for number in numbers
    if number % 2 == 0
]
```

Result:

```text
[2, 4]
```

Pattern:

```python
[output for item in collection if condition]
```

---

# 4. Transformation + Filtering

A comprehension can both filter and transform.

```python
numbers = [1, 2, 3, 4, 5]

squares_of_even = [
    number * number
    for number in numbers
    if number % 2 == 0
]
```

Result:

```text
[4, 16]
```

Mental model:

```text
Input
  ↓
Filter
  ↓
Transform
  ↓
Output list
```

---

# 5. AI Example — Extract Document Titles

Given:

```python
documents = [
    {"title": "Python", "score": 0.91},
    {"title": "RAG", "score": 0.95},
    {"title": "Agents", "score": 0.88}
]
```

Extract titles:

```python
titles = [
    document["title"]
    for document in documents
]
```

Result:

```text
['Python', 'RAG', 'Agents']
```

This is a common pattern when processing search or retrieval results.

---

# 6. AI Example — Filter Retrieved Documents

```python
relevant_documents = [
    document
    for document in documents
    if document["score"] >= 0.9
]
```

Only documents meeting the relevance threshold are retained.

This is a simple example of retrieval-result processing.

---

# 7. Dictionary Comprehension

Dictionary comprehensions work similarly to list comprehensions.

Given:

```python
numbers = [1, 2, 3, 4, 5]
```

Create a dictionary of squares:

```python
squares = {
    number: number * number
    for number in numbers
}
```

Result:

```python
{
    1: 1,
    2: 4,
    3: 9,
    4: 16,
    5: 25
}
```

Basic pattern:

```python
{key: value for item in collection}
```

---

# 8. Dictionary Comprehension with Condition

```python
even_squares = {
    number: number * number
    for number in numbers
    if number % 2 == 0
}
```

Result:

```python
{
    2: 4,
    4: 16
}
```

---

# 9. Transforming a Dictionary

Given:

```python
scores = {
    "Python": 0.91,
    "RAG": 0.95,
    "Agents": 0.88
}
```

Keep only high scores:

```python
high_scores = {
    title: score
    for title, score in scores.items()
    if score >= 0.9
}
```

Result:

```python
{
    "Python": 0.91,
    "RAG": 0.95
}
```

---

# 10. Nested Comprehensions

Comprehensions can contain multiple loops.

Example:

```python
matrix = [
    [1, 2],
    [3, 4]
]
```

Flatten:

```python
flattened = [
    number
    for row in matrix
    for number in row
]
```

Result:

```text
[1, 2, 3, 4]
```

Conceptually:

```text
for row in matrix:
    for number in row:
        take number
```

Nested comprehensions should be used carefully.

If they become difficult to read, use a normal loop.

---

# 11. `lambda`

A lambda is a small anonymous function.

Normal function:

```python
def square(x):
    return x * x
```

Lambda:

```python
square = lambda x: x * x
```

Use:

```python
square(5)
```

Result:

```text
25
```

Basic syntax:

```python
lambda arguments: expression
```

A lambda is best suited to a small, simple operation.

---

# 12. Lambda with `sorted()`

This is one of the most useful real-world patterns.

Given:

```python
documents = [
    {"title": "Python", "score": 0.72},
    {"title": "RAG", "score": 0.95},
    {"title": "Agents", "score": 0.88}
]
```

Sort by score:

```python
sorted_documents = sorted(
    documents,
    key=lambda document: document["score"]
)
```

Ascending order:

```text
Python → 0.72
Agents → 0.88
RAG → 0.95
```

Descending order:

```python
sorted_documents = sorted(
    documents,
    key=lambda document: document["score"],
    reverse=True
)
```

Result:

```text
RAG → 0.95
Agents → 0.88
Python → 0.72
```

Important pattern:

```python
sorted(
    collection,
    key=lambda item: item["field"],
    reverse=True
)
```

This is extremely common in data-processing and AI code.

---

# 13. `map()`

`map()` applies a function to every item in a collection.

Example:

```python
numbers = [1, 2, 3, 4]

def square(x):
    return x * x
```

Apply the function:

```python
result = map(square, numbers)
```

`map()` returns an iterator.

To convert it into a list:

```python
result = list(map(square, numbers))
```

Result:

```text
[1, 4, 9, 16]
```

Mental model:

```text
Input collection
       ↓
      map()
       ↓
Function applied to every item
       ↓
Transformed values
```

---

# 14. `map()` with Lambda

Instead of defining a separate function:

```python
result = list(
    map(lambda x: x * x, numbers)
)
```

Result:

```text
[1, 4, 9, 16]
```

---

# 15. `filter()`

`filter()` keeps items that satisfy a condition.

Given:

```python
numbers = [1, 2, 3, 4, 5]
```

Keep only even numbers:

```python
result = filter(
    lambda x: x % 2 == 0,
    numbers
)
```

Convert to a list:

```python
result = list(result)
```

Result:

```text
[2, 4]
```

Mental model:

```text
Input collection
       ↓
    filter()
       ↓
Keep items satisfying condition
       ↓
Filtered values
```

---

# 16. `filter()` with Documents

```python
documents = [
    {"title": "Python", "score": 0.91},
    {"title": "RAG", "score": 0.95},
    {"title": "Agents", "score": 0.88}
]
```

Filter relevant documents:

```python
relevant = list(
    filter(
        lambda document: document["score"] >= 0.9,
        documents
    )
)
```

The result contains:

```text
Python → 0.91
RAG → 0.95
```

---

# 17. Comprehension vs `map()` / `filter()`

The same transformation can often be written in different ways.

## Traditional loop

```python
squares = []

for number in numbers:
    squares.append(number * number)
```

## List comprehension

```python
squares = [number * number for number in numbers]
```

## `map()`

```python
squares = list(
    map(lambda number: number * number, numbers)
)
```

All can produce:

```text
[1, 4, 9, 16, 25]
```

---

# 18. Which Style Should You Prefer?

For simple transformations, comprehensions are often easier to read.

Prefer:

```python
squares = [x * x for x in numbers]
```

over:

```python
squares = list(map(lambda x: x * x, numbers))
```

However, understanding `map()` and `filter()` is important because:

* You will encounter them in existing Python code
* Libraries may use them
* They are part of Python's functional programming tools

The goal is not to use the shortest possible syntax.

The goal is:

> **Write clear, readable Python.**

---

# 19. Don't Overuse Comprehensions

Readable:

```python
result = [
    document["title"]
    for document in documents
    if document["score"] >= 0.9
]
```

Potentially difficult to read:

```python
result = [
    transform(x)
    for group in groups
    for x in group
    if condition(x)
    if another_condition(x)
]
```

If a comprehension becomes complicated, use a normal loop.

Pythonic code prioritizes readability.

---

# 20. AI Example — Processing LLM Results

Suppose an LLM pipeline produces:

```python
responses = [
    {
        "text": "RAG uses retrieval.",
        "score": 0.95
    },
    {
        "text": "Agents use tools.",
        "score": 0.88
    },
    {
        "text": "Python is a language.",
        "score": 0.72
    }
]
```

Extract text:

```python
texts = [
    response["text"]
    for response in responses
]
```

Filter high-confidence responses:

```python
high_confidence = [
    response
    for response in responses
    if response["score"] >= 0.9
]
```

Sort by confidence:

```python
sorted_responses = sorted(
    responses,
    key=lambda response: response["score"],
    reverse=True
)
```

These patterns are common in AI application code.

---

# 21. AI Pipeline Example

Given:

```python
documents = [
    {"title": "Python", "score": 0.82},
    {"title": "RAG", "score": 0.95},
    {"title": "Agents", "score": 0.91},
    {"title": "Kafka", "score": 0.60}
]
```

A simple processing pipeline can be:

### Step 1 — Filter

```python
relevant = [
    document
    for document in documents
    if document["score"] >= 0.8
]
```

### Step 2 — Sort

```python
sorted_documents = sorted(
    relevant,
    key=lambda document: document["score"],
    reverse=True
)
```

### Step 3 — Extract titles

```python
titles = [
    document["title"]
    for document in sorted_documents
]
```

Result:

```text
["RAG", "Agents", "Python"]
```

Conceptually:

```text
Retrieved documents
       ↓
     Filter
       ↓
      Sort
       ↓
Extract titles
```

This resembles real retrieval-result processing.

---

# 22. Important Concepts to Remember

## List comprehension

```python
[expression for item in collection]
```

With condition:

```python
[expression for item in collection if condition]
```

---

## Dictionary comprehension

```python
{key: value for item in collection}
```

---

## Lambda

```python
lambda x: expression
```

Small anonymous function.

---

## `map()`

```python
list(map(function, collection))
```

Transforms every item.

---

## `filter()`

```python
list(filter(function, collection))
```

Keeps items that satisfy a condition.

---

## Sorting with lambda

```python
sorted(
    items,
    key=lambda item: item["score"],
    reverse=True
)
```

---

# 23. Java → Python Mental Model

Java often requires more explicit iteration:

```java
for (Document document : documents) {
    if (document.getScore() >= 0.9) {
        ...
    }
}
```

Python can express the same idea concisely:

```python
relevant = [
    document
    for document in documents
    if document["score"] >= 0.9
]
```

Don't think of comprehensions as merely "shorter loops."

Think:

> **A comprehension describes how to construct a new collection from an existing collection.**

---

# 24. Lesson 7 Summary

You learned:

* List comprehensions
* Conditional comprehensions
* Transformation + filtering
* Dictionary comprehensions
* Nested comprehensions
* `lambda`
* `map()`
* `filter()`
* `sorted()` with `lambda`
* AI/LLM data-processing patterns

The most useful patterns to recognize are:

```python
[x * 2 for x in numbers]
```

```python
[x for x in numbers if x > 5]
```

```python
{x: x * x for x in numbers}
```

```python
sorted(items, key=lambda x: x["score"], reverse=True)
```

```python
list(map(function, items))
```

```python
list(filter(function, items))
```

---

# Python Fundamentals Progress

You have now covered:

```text
01. Variables & Data Types
        ↓
02. Strings
        ↓
03. Lists
        ↓
04. Dictionaries / Tuples / Sets
        ↓
05. Conditions & Loops
        ↓
06. Functions
        ↓
07. Comprehensions / Lambda / map / filter
```

The next lesson is:

# Lesson 8 — Modules, Packages & Imports

This is an important transition from writing isolated Colab code to understanding **real Python projects**.

We'll cover:

```text
import
from ... import
modules
packages
__name__
__main__
pip
requirements.txt
virtual environments
project structure
```

We'll also connect this to how real **FastAPI, LangChain, LlamaIndex, and AI projects** are structured.
