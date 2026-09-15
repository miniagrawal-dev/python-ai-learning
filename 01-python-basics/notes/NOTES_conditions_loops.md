# Lesson 5 — Conditions & Loops

## 1. Overview

Control flow determines:

* **what code should execute**
* **when it should execute**
* **how many times it should execute**

The main Python constructs are:

* `if`
* `elif`
* `else`
* `for`
* `range()`
* `break`
* `continue`
* `enumerate()`
* `zip()`

These are fundamental for processing AI/ML data, filtering search results, processing documents, iterating through messages, and implementing agent logic.

---

# 2. `if`, `elif`, `else`

Python uses indentation instead of `{}`.

```python
age = 25

if age >= 18:
    print("Adult")
else:
    print("Minor")
```

Structure:

```text
if condition:
    code

elif another_condition:
    code

else:
    code
```

Only the first matching branch executes.

Example:

```python
score = 0.92

if score >= 0.95:
    print("Excellent")
elif score >= 0.90:
    print("Good")
else:
    print("Needs improvement")
```

Output:

```text
Good
```

---

# 3. Python Indentation

Indentation is part of Python syntax.

```python
if score > 0.9:
    print("Relevant")
```

The indented line belongs to the `if` block.

Python convention:

> Use 4 spaces for indentation.

Incorrect indentation can cause an `IndentationError`.

---

# 4. Comparison Operators

Python supports:

```python
a == b    # equal
a != b    # not equal
a > b
a < b
a >= b
a <= b
```

Important:

```python
=
```

means assignment.

```python
score = 0.9
```

while:

```python
==
```

means comparison.

```python
if score == 0.9:
    print("Match")
```

---

# 5. Logical Operators

Python uses words instead of Java's `&&`, `||`, and `!`.

## AND

```python
if score > 0.8 and category == "AI":
    print("Relevant")
```

Java equivalent:

```java
if (score > 0.8 && category.equals("AI"))
```

---

## OR

```python
if role == "AI Engineer" or role == "ML Engineer":
    print("Target role")
```

Java equivalent:

```java
if (role.equals("AI Engineer") || role.equals("ML Engineer"))
```

---

## NOT

```python
if not is_complete:
    print("Continue")
```

Java equivalent:

```java
if (!isComplete)
```

---

# 6. Truthiness

Python objects can be directly used in conditions.

For example:

```python
messages = []

if messages:
    print("Messages exist")
else:
    print("No messages")
```

Output:

```text
No messages
```

An empty list is considered false.

With a non-empty list:

```python
messages = ["Hello"]

if messages:
    print("Messages exist")
```

Output:

```text
Messages exist
```

Common values considered false:

```python
False
None
0
""
[]
{}
set()
```

Almost everything else is truthy.

---

# 7. Useful Truthiness Pattern

Instead of:

```python
if len(messages) > 0:
    print("Messages exist")
```

Python code commonly uses:

```python
if messages:
    print("Messages exist")
```

This is more idiomatic Python.

However, remember that:

```python
if result:
```

checks whether the value is truthy.

If you specifically want to check whether something is not `None`, use:

```python
if result is not None:
    print(result)
```

These two checks are not always equivalent.

---

# 8. `for` Loops

Python commonly loops directly over a collection.

```python
documents = [
    {"title": "Python", "score": 0.91},
    {"title": "RAG", "score": 0.95},
    {"title": "Agents", "score": 0.88}
]

for document in documents:
    print(document["title"])
```

Output:

```text
Python
RAG
Agents
```

General pattern:

```python
for item in collection:
    # process item
```

---

# 9. `range()`

Use `range()` when you need a sequence of numbers.

```python
for i in range(5):
    print(i)
```

Output:

```text
0
1
2
3
4
```

The ending value is excluded.

---

## Start and end

```python
for i in range(2, 6):
    print(i)
```

Output:

```text
2
3
4
5
```

---

## Start, end, step

```python
for i in range(0, 10, 2):
    print(i)
```

Output:

```text
0
2
4
6
8
```

Syntax:

```python
range(start, end, step)
```

---

# 10. `break`

`break` stops the entire loop.

Example:

```python
documents = [
    {"title": "Python", "score": 0.72},
    {"title": "RAG", "score": 0.95},
    {"title": "Agents", "score": 0.91}
]

for document in documents:
    if document["score"] >= 0.95:
        print("Found:", document["title"])
        break
```

Output:

```text
Found: RAG
```

Once `break` executes, the loop ends.

### AI use case

In a retrieval system, you might stop searching once you have found a sufficiently relevant result.

Mental model:

```text
break
 ↓
stop the entire loop
```

---

# 11. `continue`

`continue` skips the current iteration and moves to the next iteration.

```python
scores = [0.4, 0.91, 0.3, 0.95]

for score in scores:
    if score < 0.8:
        continue

    print("Relevant:", score)
```

Output:

```text
Relevant: 0.91
Relevant: 0.95
```

Mental model:

```text
continue
 ↓
skip current iteration
 ↓
go to next iteration
```

Difference:

```text
break
→ stop loop completely

continue
→ skip current iteration
```

---

# 12. Nested Loops

A loop can contain another loop.

```python
documents = [
    ["chunk1", "chunk2"],
    ["chunk3", "chunk4"]
]

for document in documents:
    for chunk in document:
        print(chunk)
```

This can be useful when processing structures such as:

```text
documents
    ↓
chunks
```

or:

```text
batches
    ↓
records
```

Avoid unnecessarily complicated nested loops when simpler approaches exist.

---

# 13. `enumerate()`

Use `enumerate()` when you need both the index and the value.

Instead of:

```python
documents = ["Python", "RAG", "Agents"]

for i in range(len(documents)):
    print(i, documents[i])
```

Use:

```python
for i, document in enumerate(documents):
    print(i, document)
```

Output:

```text
0 Python
1 RAG
2 Agents
```

This is the more idiomatic Python approach.

---

# 14. `zip()`

`zip()` lets you iterate over multiple collections together.

Example:

```python
titles = ["Python", "RAG", "Agents"]
scores = [0.91, 0.95, 0.88]

for title, score in zip(titles, scores):
    print(title, score)
```

Output:

```text
Python 0.91
RAG 0.95
Agents 0.88
```

Conceptually:

```text
titles     scores
  ↓          ↓
Python     0.91
RAG        0.95
Agents     0.88
```

`zip()` is useful when processing parallel data.

---

# 15. AI Example — Filtering Search Results

Suppose a retrieval system returns:

```python
documents = [
    {"title": "Python", "score": 0.72},
    {"title": "RAG", "score": 0.95},
    {"title": "Agents", "score": 0.88},
    {"title": "LLMs", "score": 0.93}
]
```

We want documents with score >= `0.90`.

```python
relevant_documents = []

for document in documents:
    if document["score"] >= 0.90:
        relevant_documents.append(document)

print(relevant_documents)
```

Result:

```text
[
    {'title': 'RAG', 'score': 0.95},
    {'title': 'LLMs', 'score': 0.93}
]
```

This is a simple version of filtering retrieval results.

---

# 16. AI Example — Stop After Enough Results

Suppose we only need two relevant documents:

```python
relevant_documents = []

for document in documents:

    if document["score"] < 0.80:
        continue

    relevant_documents.append(document)

    if len(relevant_documents) == 2:
        break
```

This combines:

* `for`
* `if`
* `continue`
* `append()`
* `break`
* `len()`

These patterns will become useful when building retrieval and agent systems.

---

# 17. Java → Python Mental Translation

| Java                | Python                |   |      |
| ------------------- | --------------------- | - | ---- |
| `&&`                | `and`                 |   |      |
| `                   |                       | ` | `or` |
| `!`                 | `not`                 |   |      |
| `{}` blocks         | indentation           |   |      |
| `for (x : list)`    | `for x in list`       |   |      |
| `for (int i=0;...)` | `for i in range(...)` |   |      |
| `break`             | `break`               |   |      |
| `continue`          | `continue`            |   |      |
| `Map` iteration     | `.items()`            |   |      |
| `list.size()`       | `len(list)`           |   |      |

---

# 18. Common Mistakes

## Mistake 1 — Using `=` instead of `==`

Wrong:

```python
if score = 0.9:
```

Correct:

```python
if score == 0.9:
```

---

## Mistake 2 — Forgetting the colon

Wrong:

```python
if score > 0.9
```

Correct:

```python
if score > 0.9:
```

---

## Mistake 3 — Incorrect indentation

Wrong:

```python
if score > 0.9:
print("Good")
```

Correct:

```python
if score > 0.9:
    print("Good")
```

---

## Mistake 4 — Using `range(len(...))` unnecessarily

Instead of:

```python
for i in range(len(documents)):
    print(documents[i])
```

prefer:

```python
for document in documents:
    print(document)
```

And when you need the index:

```python
for i, document in enumerate(documents):
    print(i, document)
```

---

# 19. Key Takeaways

### Conditions

```python
if condition:
    ...

elif another_condition:
    ...

else:
    ...
```

### Logical operators

```python
and
or
not
```

### Loop

```python
for item in collection:
    ...
```

### Range

```python
for i in range(5):
    ...
```

### Stop loop

```python
break
```

### Skip iteration

```python
continue
```

### Index + value

```python
for i, item in enumerate(items):
    ...
```

### Multiple collections

```python
for a, b in zip(list1, list2):
    ...
```

---

# 20. AI Engineering Mental Model

Control flow appears everywhere in AI systems:

```text
FOR
 ↓
process documents
process chunks
process messages
process search results
process tools
process datasets
```

```text
IF
 ↓
is the document relevant?
is the response valid?
is the tool available?
did the model return an error?
```

```text
CONTINUE
 ↓
ignore irrelevant result
skip invalid record
skip failed item
```

```text
BREAK
 ↓
enough search results found
agent has completed its task
success condition reached
```

A simplified agent loop might eventually look conceptually like:

```python
while not task_complete:

    result = call_model()

    if result.requires_tool:
        execute_tool()
        continue

    if result.is_final:
        break
```

You don't need to understand the agent implementation yet. The important thing is that the Python control-flow concepts you're learning now are the building blocks for it.

---

# Lesson 5 Complete

You have now covered:

* `if`
* `elif`
* `else`
* comparison operators
* `and`
* `or`
* `not`
* truthiness
* `for`
* `range()`
* `break`
* `continue`
* nested loops
* `enumerate()`
* `zip()`
* AI-style filtering and processing

Next lesson: **Functions** — one of the most important Python concepts before we move into AI libraries.

We will cover:

```text
def
parameters
arguments
return
default parameters
keyword arguments
*args
**kwargs
scope
type hints
```

and then build a small **AI-style utility function** rather than doing only generic examples.
