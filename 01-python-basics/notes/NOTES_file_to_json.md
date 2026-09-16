# Lesson 10 — File I/O & JSON

## 1. What is File I/O?

I/O means **Input / Output**.

File I/O means reading data from and writing data to files.

Python uses:

```python
open()
```

to work with files.

Basic example:

```python
file = open("example.txt", "r")
```

---

# 2. File Modes

Common modes:

| Mode   | Meaning           |
| ------ | ----------------- |
| `"r"`  | Read              |
| `"w"`  | Write             |
| `"a"`  | Append            |
| `"x"`  | Create a new file |
| `"rb"` | Read binary       |
| `"wb"` | Write binary      |

Important:

```text
"w" → overwrites existing content
"a" → adds to existing content
```

---

# 3. Reading a File

Basic approach:

```python
file = open("example.txt", "r")

content = file.read()

print(content)

file.close()
```

However, the preferred Python approach is `with open()`.

---

# 4. `with open()` — Preferred Approach

```python
with open("example.txt", "r") as file:
    content = file.read()

print(content)
```

`with` automatically handles closing the file.

Mental model:

```text
open file
   ↓
use file
   ↓
automatically close file
```

This pattern is very common in Python.

---

# 5. Reading Line by Line

```python
with open("example.txt", "r") as file:
    for line in file:
        print(line)
```

This is useful for processing large files without necessarily loading the entire file into memory.

---

# 6. `readlines()`

`readlines()` returns the lines as a list.

```python
with open("example.txt", "r") as file:
    lines = file.readlines()

print(lines)
```

If the file contains:

```text
Python
Java
AI
```

the result may be:

```python
["Python\n", "Java\n", "AI\n"]
```

The `\n` represents a newline.

You can remove it with `.strip()`:

```python
with open("example.txt", "r") as file:
    lines = [line.strip() for line in file]

print(lines)
```

Result:

```python
["Python", "Java", "AI"]
```

This combines:

* file iteration
* list comprehensions
* string methods

---

# 7. Writing to a File

Use `"w"` mode:

```python
with open("output.txt", "w") as file:
    file.write("Hello Python")
```

This creates `output.txt`.

If the file already exists, `"w"` overwrites its contents.

---

# 8. Writing Multiple Lines

```python
with open("output.txt", "w") as file:
    file.write("Python\n")
    file.write("AI\n")
    file.write("LLM\n")
```

The file contains:

```text
Python
AI
LLM
```

---

# 9. Append to a File

Use `"a"`:

```python
with open("output.txt", "a") as file:
    file.write("RAG\n")
```

Existing content is preserved and the new content is added.

---

# 10. Handling Missing Files

Trying to read a file that doesn't exist:

```python
with open("does_not_exist.txt", "r") as file:
    content = file.read()
```

raises:

```text
FileNotFoundError
```

We can combine file I/O with exception handling:

```python
try:
    with open("does_not_exist.txt", "r") as file:
        content = file.read()

except FileNotFoundError:
    print("File not found")
```

---

# 11. What is JSON?

JSON stands for:

**JavaScript Object Notation**

JSON is a common data interchange format.

Example:

```json
{
  "name": "Mini",
  "role": "Software Engineer",
  "skills": ["Java", "Python", "AI"]
}
```

JSON is used extensively in:

* REST APIs
* LLM APIs
* tool calling
* structured outputs
* configuration
* databases
* agent state
* data exchange between services

---

# 12. Python Dictionary vs JSON

Python:

```python
user = {
    "name": "Mini",
    "age": 31
}
```

JSON:

```json
{
  "name": "Mini",
  "age": 31
}
```

They look similar, but they are different concepts.

### Python dictionary

An object/data structure stored in Python memory.

### JSON

A text-based data interchange format.

Mental model:

```text
Python dictionary
       ↓
serialization
       ↓
JSON
```

And:

```text
JSON
       ↓
deserialization
       ↓
Python dictionary
```

---

# 13. Python's `json` Module

Python provides the `json` module as part of its standard library.

No installation is required.

```python
import json
```

---

# 14. `json.dumps()`

`json.dumps()` converts a Python object into a JSON string.

```python
import json

user = {
    "name": "Mini",
    "age": 31
}

json_string = json.dumps(user)

print(json_string)
```

Output:

```text
{"name": "Mini", "age": 31}
```

Mental model:

```text
Python dict
    ↓
json.dumps()
    ↓
JSON string
```

---

# 15. Pretty JSON

Use `indent` to make JSON easier to read:

```python
json_string = json.dumps(user, indent=2)

print(json_string)
```

Output:

```json
{
  "name": "Mini",
  "age": 31
}
```

This is useful when debugging API responses.

---

# 16. `json.loads()`

`json.loads()` converts a JSON string into a Python object.

```python
import json

json_string = '{"name": "Mini", "age": 31}'

user = json.loads(json_string)

print(user)
print(type(user))
```

Output:

```text
{'name': 'Mini', 'age': 31}
<class 'dict'>
```

Mental model:

```text
JSON string
    ↓
json.loads()
    ↓
Python dictionary
```

---

# 17. `dump()` vs `dumps()`

This is an important distinction.

### `dumps()`

Python object → JSON string

```python
json.dumps(data)
```

### `dump()`

Python object → JSON file

```python
json.dump(data, file)
```

Similarly:

### `loads()`

JSON string → Python object

```python
json.loads(json_string)
```

### `load()`

JSON file → Python object

```python
json.load(file)
```

Easy memory trick:

```text
s = string
```

Therefore:

```text
dumps  → JSON string
loads  → Python from JSON string

dump   → JSON file
load   → Python from JSON file
```

---

# 18. Writing JSON to a File

```python
import json

user = {
    "name": "Mini",
    "skills": ["Java", "Python", "AI"]
}

with open("user.json", "w") as file:
    json.dump(user, file, indent=2)
```

This creates:

```text
user.json
```

containing:

```json
{
  "name": "Mini",
  "skills": [
    "Java",
    "Python",
    "AI"
  ]
}
```

---

# 19. Reading JSON from a File

```python
import json

with open("user.json", "r") as file:
    user = json.load(file)

print(user)
```

`user` is now a Python dictionary.

Mental model:

```text
user.json
    ↓
json.load()
    ↓
Python dictionary
```

---

# 20. Nested JSON

Real API responses are often deeply nested.

Example:

```python
response = {
    "model": "my-model",
    "usage": {
        "prompt_tokens": 100,
        "completion_tokens": 50
    },
    "choices": [
        {
            "message": {
                "role": "assistant",
                "content": "Hello"
            }
        }
    ]
}
```

Access values:

```python
response["model"]
```

```python
response["usage"]["prompt_tokens"]
```

```python
response["choices"][0]["message"]["content"]
```

This pattern is extremely common when working with APIs.

---

# 21. JSON + Exception Handling

JSON parsing can fail.

```python
import json

json_string = '{"name": "Mini", "age": }'

try:
    data = json.loads(json_string)

except json.JSONDecodeError:
    print("Invalid JSON")
```

The important exception is:

```python
json.JSONDecodeError
```

This connects Lesson 9 and Lesson 10.

---

# 22. AI Example — Tool Calling

Later, an LLM may produce structured tool information such as:

```json
{
  "tool": "search_products",
  "arguments": {
    "query": "running shoes",
    "max_price": 5000
  }
}
```

Python can parse it:

```python
import json

tool_response = '''
{
    "tool": "search_products",
    "arguments": {
        "query": "running shoes",
        "max_price": 5000
    }
}
'''

data = json.loads(tool_response)

print(data["tool"])
print(data["arguments"]["query"])
```

Output:

```text
search_products
running shoes
```

Later, when we learn **tool calling and AI agents**, this becomes a major concept.

---

# 23. AI Example — Configuration

Configuration can also be stored as JSON.

`config.json`:

```json
{
  "model": "my-model",
  "temperature": 0.2,
  "max_tokens": 1000
}
```

Python:

```python
import json

with open("config.json", "r") as file:
    config = json.load(file)

print(config["model"])
print(config["temperature"])
```

Production applications often use environment variables and dedicated configuration systems, but JSON is useful for structured configuration and experiments.

---

# 24. AI Example — Documents

Imagine a RAG system has:

```text
documents/
├── doc1.txt
├── doc2.txt
└── doc3.txt
```

Python can read a document:

```python
with open("doc1.txt", "r") as file:
    text = file.read()
```

Eventually, the pipeline becomes:

```text
Document
   ↓
Read file
   ↓
Extract text
   ↓
Clean text
   ↓
Split into chunks
   ↓
Create embeddings
   ↓
Store in vector database
```

This is one of the first steps toward building a RAG system.

---

# 25. File Paths

A relative path:

```python
open("data/file.txt")
```

means the path is relative to the current working directory.

An absolute path looks like:

```python
open("/home/user/data/file.txt")
```

For modern Python applications, you'll often use `pathlib`.

Example:

```python
from pathlib import Path

file_path = Path("data") / "file.txt"

print(file_path)
```

We'll study `pathlib` more deeply later.

---

# 26. AI Engineering Mental Model

File I/O and JSON are fundamental because AI applications constantly move data between files, Python objects, APIs, and external systems.

```text
File / API
    ↓
JSON / text
    ↓
Python object
    ↓
Processing
    ↓
LLM / RAG / Agent
    ↓
Python object
    ↓
JSON
    ↓
API / File / Database
```

---

# 27. Key Takeaways

1. `open()` is used for file operations.
2. Prefer `with open(...)` because it automatically closes the file.
3. `"r"` means read.
4. `"w"` means write/overwrite.
5. `"a"` means append.
6. `read()` reads the entire content.
7. Iterating over a file processes it line by line.
8. `.strip()` removes surrounding whitespace/newlines.
9. JSON is a text-based data interchange format.
10. Python dictionaries and JSON look similar but are different concepts.
11. `json.dumps()` converts Python → JSON string.
12. `json.loads()` converts JSON string → Python.
13. `json.dump()` writes Python → JSON file.
14. `json.load()` reads JSON file → Python.
15. `JSONDecodeError` occurs when JSON cannot be parsed.
16. JSON is heavily used in APIs, LLM responses, tool calling, configuration, and agent systems.
17. File I/O is an important foundation for document processing and RAG.

---

# 28. Quick Reference

```python
# Read
with open("file.txt", "r") as file:
    content = file.read()

# Write
with open("file.txt", "w") as file:
    file.write("Hello")

# Append
with open("file.txt", "a") as file:
    file.write("World")

# Python → JSON string
json_string = json.dumps(data)

# JSON string → Python
data = json.loads(json_string)

# Python → JSON file
with open("data.json", "w") as file:
    json.dump(data, file, indent=2)

# JSON file → Python
with open("data.json", "r") as file:
    data = json.load(file)
```

---
