# Python Lists — Notes

## 1. What is a List?

A list stores multiple values in a single variable.

```python
languages = ["Java", "Python", "C++"]
```

Python lists are similar to Java's `List`.

### Java

```java
List<String> languages = List.of("Java", "Python", "C++");
```

### Python

```python
languages = ["Java", "Python", "C++"]
```

Python does not require explicit type declaration.

---

## 2. Creating Lists

```python
languages = ["Java", "Python", "C++"]

numbers = [10, 20, 30, 40]

names = ["Mini", "John", "Rahul"]
```

A list can technically contain different types:

```python
data = ["Mini", 9, 65.5, True]
```

Although Python allows mixed types, production code generally keeps lists logically consistent.

---

## 3. List Type

Use `type()` to check whether something is a list.

```python
languages = ["Java", "Python", "C++"]

print(type(languages))
```

Output:

```text
<class 'list'>
```

---

## 4. List Indexing

Python uses zero-based indexing.

```python
languages = ["Java", "Python", "C++"]
```

Indexes:

```text
Java     Python     C++
 0          1        2
```

Access an element:

```python
print(languages[0])
print(languages[1])
print(languages[2])
```

Output:

```text
Java
Python
C++
```

---

## 5. Negative Indexing

Python allows indexing from the end.

```text
Java     Python     C++
 0          1        2
-3         -2       -1
```

Therefore:

```python
print(languages[-1])
```

returns:

```text
C++
```

`-1` means the last element.

---

## 6. List Slicing

Lists support slicing just like strings.

Syntax:

```python
list[start:end]
```

Important rule:

> Start is included, end is excluded.

Example:

```python
languages = ["Java", "Python", "C++", "Go", "Rust"]

print(languages[0:2])
```

Output:

```text
['Java', 'Python']
```

### Useful slicing

```python
languages[:3]     # First 3 elements
languages[2:]     # From index 2 to the end
languages[-2:]    # Last 2 elements
languages[:-2]    # Everything except the last 2
```

---

## 7. Lists are Mutable

One of the most important differences between strings and lists:

> Lists are mutable.

This means a list can be modified after it is created.

```python
languages = ["Java", "Python", "C++"]

languages[0] = "JavaScript"

print(languages)
```

Output:

```text
['JavaScript', 'Python', 'C++']
```

Compare this with strings:

```python
text = "Python"

# text[0] = "J"   # Error
```

Strings are immutable, while lists are mutable.

---

## 8. append()

`append()` adds one item to the end of a list.

```python
languages = ["Java", "Python"]

languages.append("C++")

print(languages)
```

Output:

```text
['Java', 'Python', 'C++']
```

Syntax:

```python
list.append(item)
```

---

## 9. insert()

`insert()` adds an item at a specific index.

```python
languages = ["Java", "Python", "C++"]

languages.insert(1, "Go")

print(languages)
```

Output:

```text
['Java', 'Go', 'Python', 'C++']
```

Syntax:

```python
list.insert(index, value)
```

---

## 10. remove()

`remove()` removes an item by its value.

```python
languages = ["Java", "Python", "C++"]

languages.remove("Python")

print(languages)
```

Output:

```text
['Java', 'C++']
```

If the value does not exist, Python raises an error.

---

## 11. pop()

`pop()` removes an item by index and returns the removed item.

```python
languages = ["Java", "Python", "C++"]

removed = languages.pop(1)

print(removed)
print(languages)
```

Output:

```text
Python
['Java', 'C++']
```

If no index is provided:

```python
languages.pop()
```

the last element is removed.

---

## 12. len()

`len()` returns the number of elements in a list.

```python
languages = ["Java", "Python", "C++"]

print(len(languages))
```

Output:

```text
3
```

---

## 13. Checking Membership

Use `in` to check whether an item exists in a list.

```python
languages = ["Java", "Python", "C++"]

print("Python" in languages)
```

Output:

```text
True
```

Example:

```python
print("Rust" in languages)
```

Output:

```text
False
```

---

## 14. Looping Through a List

A `for` loop can iterate through every item.

```python
languages = ["Java", "Python", "C++"]

for language in languages:
    print(language)
```

Output:

```text
Java
Python
C++
```

General pattern:

```python
for item in collection:
    # code
```

Python uses indentation to define the loop body.

### Java

```java
for (String language : languages) {
    System.out.println(language);
}
```

### Python

```python
for language in languages:
    print(language)
```

---

## 15. Lists of Dictionaries

A very common Python structure is a list containing dictionaries.

```python
products = [
    {
        "name": "Laptop",
        "price": 70000
    },
    {
        "name": "Phone",
        "price": 30000
    }
]
```

The structure is:

```text
List
 ↓
Dictionary
 ↓
Key / Value
```

Access the first dictionary:

```python
print(products[0])
```

Access its name:

```python
print(products[0]["name"])
```

Access its price:

```python
print(products[0]["price"])
```

---

## 16. Looping Through a List of Dictionaries

```python
products = [
    {"name": "Laptop", "price": 70000},
    {"name": "Phone", "price": 30000}
]

for product in products:
    print(product["name"])
```

Output:

```text
Laptop
Phone
```

Using an f-string:

```python
for product in products:
    print(f"{product['name']} costs ₹{product['price']}")
```

Output:

```text
Laptop costs ₹70000
Phone costs ₹30000
```

This pattern is extremely common in Python APIs and AI applications.

---

## 17. List Comprehension

List comprehension provides a concise way to create a new list.

### Normal for loop

```python
numbers = [1, 2, 3, 4, 5]

squares = []

for number in numbers:
    squares.append(number * number)

print(squares)
```

Output:

```text
[1, 4, 9, 16, 25]
```

### List comprehension

```python
numbers = [1, 2, 3, 4, 5]

squares = [number * number for number in numbers]

print(squares)
```

Output:

```text
[1, 4, 9, 16, 25]
```

General structure:

```python
[new_value for item in collection]
```

---

## 18. List Comprehension with a Condition

List comprehensions can also filter values.

Example:

```python
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = [number for number in numbers if number % 2 == 0]

print(even_numbers)
```

Output:

```text
[2, 4, 6]
```

General structure:

```python
[value for item in collection if condition]
```

This becomes very useful for data processing.

---

# AI/ML Connection

Lists are fundamental to Python AI/ML applications.

They are commonly used for:

* Documents
* Document chunks
* Search results
* Tokens
* Embeddings
* Messages
* Products
* Tool results
* Agent state
* Model outputs

### Example: Documents

```python
documents = [
    "Kafka is an event streaming platform.",
    "Python is widely used for AI.",
    "RAG combines retrieval with generation."
]
```

Process them:

```python
for document in documents:
    print(document)
```

---

## AI Example: Search Results

An AI search tool might return:

```python
results = [
    {"title": "Document 1", "score": 0.91},
    {"title": "Document 2", "score": 0.87},
    {"title": "Document 3", "score": 0.82}
]
```

We can process the results:

```python
for result in results:
    print(result["title"])
```

This same structure appears in:

* RAG systems
* Search applications
* AI agents
* Product recommendation systems
* API responses
* LLM applications

---

# Important List Methods — Quick Reference

| Method     | Purpose          | Example              |
| ---------- | ---------------- | -------------------- |
| `append()` | Add item at end  | `items.append(x)`    |
| `insert()` | Add at position  | `items.insert(1, x)` |
| `remove()` | Remove by value  | `items.remove(x)`    |
| `pop()`    | Remove by index  | `items.pop(1)`       |
| `len()`    | Number of items  | `len(items)`         |
| `in`       | Check membership | `x in items`         |

---

# Strings vs Lists

| Feature    | String          | List            |
| ---------- | --------------- | --------------- |
| Stores     | Characters/text | Multiple values |
| Indexing   | Yes             | Yes             |
| Slicing    | Yes             | Yes             |
| Mutable    | No              | Yes             |
| `len()`    | Yes             | Yes             |
| `in`       | Yes             | Yes             |
| `append()` | No              | Yes             |

Example:

```python
text = "Python"
languages = ["Java", "Python"]
```

String:

```python
# text[0] = "J"  # Error
```

List:

```python
languages[0] = "C++"  # Valid
```

---

# Common Mistakes

## Mistake 1 — Forgetting zero-based indexing

```python
languages = ["Java", "Python", "C++"]

print(languages[1])
```

This prints:

```text
Python
```

not Java.

---

## Mistake 2 — Forgetting that the end of a slice is excluded

```python
languages[0:2]
```

returns the elements at indexes `0` and `1`, not `2`.

---

## Mistake 3 — Confusing remove() and pop()

```python
languages.remove("Python")
```

removes by **value**.

```python
languages.pop(1)
```

removes by **index** and returns the removed element.

---

## Mistake 4 — Forgetting indentation

Correct:

```python
for language in languages:
    print(language)
```

Incorrect:

```python
for language in languages:
print(language)
```

Python uses indentation to define code blocks.

---

# Key Takeaways

1. A list stores multiple values.
2. Lists use square brackets `[]`.
3. Python uses zero-based indexing.
4. Negative indexing starts from `-1`.
5. Lists support slicing.
6. Lists are mutable.
7. `append()` adds to the end.
8. `insert()` adds at a specific position.
9. `remove()` removes by value.
10. `pop()` removes by index and returns the removed value.
11. `len()` returns the number of elements.
12. `in` checks membership.
13. `for` loops iterate through lists.
14. Lists can contain dictionaries.
15. List comprehensions provide a concise way to create lists.
16. List comprehensions can also filter data.
17. Lists of dictionaries are extremely common in APIs and AI applications.
18. Lists are heavily used for documents, chunks, search results, messages, embeddings and agent state.

---

# Mental Model

```text
List
 ↓
Multiple values
 ↓
Indexing
 ↓
Slicing
 ↓
Mutable
 ↓
append / insert / remove / pop
 ↓
Loop
 ↓
List + Dictionary
 ↓
List Comprehension
 ↓
AI/ML data processing
```
