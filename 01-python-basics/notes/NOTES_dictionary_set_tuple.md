# Lesson 4 — Dictionaries, Tuples & Sets

## 1. Overview

Python provides several built-in collection types:

* **List** → ordered, mutable collection; duplicates allowed
* **Dictionary** → key-value mapping
* **Tuple** → ordered, immutable collection
* **Set** → collection of unique values

For AI/ML engineering, dictionaries are especially important because JSON, API requests/responses, model configuration, metadata, tool definitions, and agent state are commonly represented using dictionaries.

---

# 2. Dictionaries

## What is a dictionary?

A dictionary stores data as **key → value** pairs.

```python
user = {
    "name": "Mini",
    "age": 31,
    "role": "Software Engineer"
}
```

Access a value using its key:

```python
print(user["name"])
print(user["age"])
```

Output:

```text
Mini
31
```

### Java comparison

Python:

```python
user = {
    "name": "Mini",
    "age": 31
}
```

Conceptually similar to:

```java
Map<String, Object> user = new HashMap<>();
```

Python dictionaries are heavily used for JSON-like data.

---

# 3. Accessing Dictionary Values

## Using `[]`

```python
user["name"]
```

If the key doesn't exist, Python raises `KeyError`.

```python
user["city"]
```

Result:

```text
KeyError
```

---

## Using `.get()`

```python
user.get("city")
```

If the key doesn't exist, the result is:

```text
None
```

You can provide a default value:

```python
user.get("city", "Unknown")
```

Result:

```text
Unknown
```

### Important difference

```python
user["city"]
```

means:

> I expect this key to exist.

```python
user.get("city")
```

means:

> Give me this value if it exists.

`.get()` is particularly useful when processing API responses where fields may be optional.

---

# 4. Adding and Updating Values

Create a dictionary:

```python
user = {
    "name": "Mini",
    "age": 31
}
```

Add a new key:

```python
user["city"] = "Bangalore"
```

Update an existing key:

```python
user["age"] = 32
```

Python uses the same syntax for both adding and updating.

---

# 5. Removing Dictionary Values

## `del`

```python
del user["city"]
```

This removes the key-value pair.

---

## `pop()`

```python
age = user.pop("age")
```

`pop()` removes the item and returns its value.

```python
print(age)
```

---

# 6. Checking Whether a Key Exists

Use `in`:

```python
user = {
    "name": "Mini",
    "age": 31
}

print("name" in user)
```

Output:

```text
True
```

```python
print("city" in user)
```

Output:

```text
False
```

For dictionaries, `in` checks **keys**.

---

# 7. Looping Through Dictionaries

## Loop through keys

```python
for key in user:
    print(key)
```

or:

```python
for key in user.keys():
    print(key)
```

---

## Loop through values

```python
for value in user.values():
    print(value)
```

---

## Loop through key-value pairs

Use `.items()`:

```python
for key, value in user.items():
    print(key, value)
```

This pattern is extremely common in Python.

---

# 8. Nested Dictionaries

Dictionaries can contain other dictionaries.

```python
employee = {
    "name": "Mini",
    "job": {
        "title": "Senior Software Engineer",
        "company": "Walmart"
    }
}
```

Access nested values:

```python
print(employee["job"]["title"])
```

Output:

```text
Senior Software Engineer
```

Nested dictionaries are common when working with JSON and API responses.

---

# 9. List of Dictionaries

A very important structure for AI applications is:

```python
documents = [
    {
        "id": 1,
        "title": "Python Basics",
        "score": 0.91
    },
    {
        "id": 2,
        "title": "Machine Learning",
        "score": 0.87
    },
    {
        "id": 3,
        "title": "RAG Systems",
        "score": 0.95
    }
]
```

Access an item:

```python
print(documents[0]["title"])
```

Output:

```text
Python Basics
```

Loop through the documents:

```python
for document in documents:
    print(document["title"], document["score"])
```

### Java mental model

Think approximately:

```text
List<Map<String, Object>>
```

This mental translation is useful when moving from Java to Python.

---

# 10. Dictionary Comprehension

Dictionary comprehensions provide a concise way to create dictionaries.

```python
numbers = [1, 2, 3, 4, 5]

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

With a condition:

```python
even_squares = {
    number: number * number
    for number in numbers
    if number % 2 == 0
}
```

---

# 11. AI/LLM Example — Model Configuration

Dictionaries are frequently used for configuration.

```python
model_config = {
    "model": "some-model",
    "temperature": 0.7,
    "max_tokens": 500
}

print(model_config["model"])
print(model_config["temperature"])
```

This pattern will become very familiar when working with LLM APIs.

---

# 12. AI/LLM Example — Messages

LLM applications commonly work with a list of message dictionaries.

```python
messages = [
    {
        "role": "system",
        "content": "You are a helpful assistant."
    },
    {
        "role": "user",
        "content": "Explain RAG."
    }
]
```

The structure is:

```text
List
 └── Dictionary
      ├── role
      └── content
```

This is an important structure to recognize in AI code.

---

# 13. AI Example — Agent State

An agent can maintain state using a dictionary:

```python
agent_state = {
    "user": {
        "name": "Mini"
    },
    "messages": [],
    "tools_used": set(),
    "metadata": {
        "session_id": 123
    }
}
```

We can add a message:

```python
agent_state["messages"].append({
    "role": "user",
    "content": "Hello"
})
```

Add tools to the set:

```python
agent_state["tools_used"].add("search")
agent_state["tools_used"].add("calculator")
```

Access nested data:

```python
print(agent_state["user"]["name"])
```

This type of nested structure will become important when learning AI agents.

---

# 14. Tuples

A tuple is an **ordered, immutable collection**.

```python
coordinates = (10, 20)
```

Access values:

```python
print(coordinates[0])
print(coordinates[1])
```

Tuples support indexing and slicing like lists.

But tuples cannot be modified.

```python
coordinates[0] = 100
```

This produces an error because tuples are immutable.

---

# 15. List vs Tuple

List:

```python
numbers = [10, 20]
numbers[0] = 100
```

Works because lists are mutable.

Tuple:

```python
coordinates = (10, 20)
coordinates[0] = 100
```

Fails because tuples are immutable.

### When to use a tuple?

Use a tuple when the collection represents data that should not be modified.

Example:

```python
dimensions = (1920, 1080)
```

---

# 16. Tuple Unpacking

Tuple values can be unpacked into variables.

```python
coordinates = (10, 20)

x, y = coordinates

print(x)
print(y)
```

Output:

```text
10
20
```

Another example:

```python
result = ("RAG", 0.95)

topic, score = result

print(topic)
print(score)
```

Tuple unpacking is common in Python code.

---

# 17. Sets

A set stores **unique values**.

```python
numbers = {1, 2, 3, 4}
```

Duplicates are automatically removed:

```python
numbers = {1, 2, 2, 3, 3, 4}

print(numbers)
```

Result:

```text
{1, 2, 3, 4}
```

Sets are useful for:

* Removing duplicates
* Fast membership checks
* Comparing collections
* Tracking unique items

---

# 18. Adding to a Set

Use `.add()`:

```python
skills = {"Java", "Python"}

skills.add("Kafka")
```

---

# 19. Set Membership

Use `in`:

```python
print("Python" in skills)
```

Result:

```text
True
```

Sets are particularly useful when you frequently need to check whether an item exists.

---

# 20. Set Operations

Example:

```python
backend = {"Java", "Python", "Kafka", "SQL"}

ai = {"Python", "SQL", "PyTorch", "LangChain"}
```

## Union

Everything from both sets:

```python
backend | ai
```

---

## Intersection

Items present in both:

```python
backend & ai
```

Result:

```text
{"Python", "SQL"}
```

---

## Difference

Items present in `backend` but not `ai`:

```python
backend - ai
```

---

# 21. RAG Example — Deduplication

Suppose a search system returns duplicate document IDs:

```python
document_ids = [101, 102, 101, 103, 102, 104, 101]
```

Convert to a set:

```python
unique_ids = set(document_ids)
```

Result:

```text
{101, 102, 103, 104}
```

If a list is required afterward:

```python
unique_ids = list(set(document_ids))
```

Sets are therefore useful for removing duplicate results.

Note: converting a set to a list does not guarantee a meaningful ordering.

---

# 22. Collection Comparison

| Type       | Ordered          | Mutable | Duplicates  | Main purpose        |
| ---------- | ---------------- | ------- | ----------- | ------------------- |
| List       | Yes              | Yes     | Yes         | Collection of items |
| Tuple      | Yes              | No      | Yes         | Fixed collection    |
| Set        | No               | Yes     | No          | Unique items        |
| Dictionary | Insertion order* | Yes     | Keys unique | Key → value mapping |

* Modern Python dictionaries preserve insertion order, but their primary purpose is mapping keys to values.

---

# 23. AI/ML Mental Model

Remember these associations:

```text
LIST
 ↓
documents
chunks
messages
search results
embeddings
tool results
agent steps
```

```text
DICTIONARY
 ↓
API JSON
model configuration
LLM messages
tool schemas
metadata
agent state
```

```text
TUPLE
 ↓
fixed groups of values
coordinates
returned values
unpacking
```

```text
SET
 ↓
deduplication
unique IDs
membership checks
common items
```

---

# 24. Important Python Naming Rule

Do not use Python built-in names as variable names.

Avoid:

```python
set = ...
list = ...
dict = ...
str = ...
type = ...
sum = ...
```

For example:

```python
set = {"Java", "Python"}
```

Now `set` no longer refers to Python's built-in `set` type.

This causes:

```python
set()
```

to fail with:

```text
TypeError: 'set' object is not callable
```

If this happens in Colab, restart the runtime or delete the variable:

```python
del set
```

Then:

```python
set()
```

works again.

---

# 25. Key Takeaways

### Dictionaries

```python
user["name"]
user.get("name")
user["city"] = "Bangalore"
user.pop("age")

for key, value in user.items():
    print(key, value)
```

Remember:

> Dictionary = key → value

---

### Tuples

```python
point = (10, 20)

x, y = point
```

Remember:

> Tuple = ordered + immutable

---

### Sets

```python
numbers = {1, 2, 3}

numbers.add(4)

print(2 in numbers)
```

Remember:

> Set = unique values

---

### Most important AI pattern

```python
documents = [
    {
        "title": "RAG",
        "score": 0.95
    }
]
```

Think:

> List of dictionaries

This pattern will appear repeatedly in RAG, APIs, tool calling, and agents.

---

# 26. Exercises Completed

The Lesson 4 exercises covered:

1. Model configuration dictionary
2. Safe dictionary access with `.get()`
3. Adding and updating dictionary values
4. Iterating over a list of dictionaries
5. Filtering documents by score
6. Dictionary comprehension
7. Tuple unpacking
8. Set-based deduplication
9. Nested AI-style agent state

The final agent-state structure was:

```python
agent_state = {
    "user": {
        "name": "Mini"
    },
    "messages": [],
    "tools_used": set(),
    "metadata": {
        "session_id": 123
    }
}
```

This combines the concepts from the lesson:

```text
Dictionary
 ├── user → Dictionary
 ├── messages → List
 ├── tools_used → Set
 └── metadata → Dictionary
```

This is exactly the kind of nested Python structure you should become comfortable reading before moving into LLM frameworks and agent code.
