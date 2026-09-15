# Python Variables & Strings — Notes

## 1. Variables

A variable in Python is a **name that refers to an object/value**.

```python
name = "Mini"
experience = 9
salary = 6500000
is_learning_ai = True
```

Python does not require us to explicitly declare the type of a variable.

### Java vs Python

Java:

```java
int experience = 9;
String name = "Mini";
boolean isLearningAI = true;
```

Python:

```python
experience = 9
name = "Mini"
is_learning_ai = True
```

Python determines the type at runtime.

---

## 2. Python is dynamically typed

The same variable name can refer to objects of different types at different times.

```python
x = 10
print(type(x))

x = "Python"
print(type(x))

x = 3.14
print(type(x))
```

Output:

```text
<class 'int'>
<class 'str'>
<class 'float'>
```

Python is **dynamically typed**, but it is not untyped.

The object has a type, and Python determines that type at runtime.

---

## 3. Common Python data types

| Type       | Example          | Meaning        |
| ---------- | ---------------- | -------------- |
| `str`      | `"Python"`       | Text           |
| `int`      | `10`             | Integer        |
| `float`    | `3.14`           | Decimal number |
| `bool`     | `True` / `False` | Boolean        |
| `NoneType` | `None`           | No value       |

Check the type using:

```python
x = 10
print(type(x))
```

---

## 4. Variables are references to objects

Consider:

```python
experience = 9
```

A useful mental model is:

```text
experience ───────→ 9
```

The name `experience` refers to an object containing the value `9`.

If we do:

```python
experience = 10
```

the name now refers to the new value:

```text
experience ───────→ 10
```

This object/reference model becomes particularly important when working with **lists, dictionaries, functions, classes, and mutable objects**.

---

# Strings

## 5. What is a string?

A string (`str`) represents text.

```python
name = "Mini"
company = 'Walmart'
```

Both single and double quotes can be used.

```python
name1 = "Mini"
name2 = 'Mini'
```

---

## 6. Multi-line strings

Triple quotes can be used for multi-line strings.

```python
prompt = """
You are an AI assistant.
Answer the user's question clearly.
"""
```

This is especially useful when creating **LLM prompts**.

---

## 7. String concatenation

Strings can be joined using `+`.

```python
first_name = "Mini"
last_name = "Agrawal"

full_name = first_name + " " + last_name

print(full_name)
```

Output:

```text
Mini Agrawal
```

However, for inserting variables into text, **f-strings are usually cleaner**.

---

## 8. f-strings ⭐

An f-string allows Python expressions/variables to be inserted directly into a string.

```python
name = "Mini"
experience = 9

message = f"My name is {name} and I have {experience} years of experience."

print(message)
```

Output:

```text
My name is Mini and I have 9 years of experience.
```

Syntax:

```python
f"some text {variable}"
```

### AI example

```python
user_question = "What is semantic search?"

prompt = f"""
You are an AI teacher.

Explain the following concept to a software engineer
who knows Java but is new to AI.

Concept: {user_question}

Use a simple example.
"""
```

f-strings are very useful when dynamically constructing **prompts, API messages, logs, and configuration text**.

---

# String Operations

## 9. String length

Use `len()` to get the number of characters.

```python
text = "Hello Python"

print(len(text))
```

Spaces are also counted as characters.

---

## 10. Useful string methods

```python
text = "Hello Python"

print(text.upper())
print(text.lower())
print(text.title())
```

Output:

```text
HELLO PYTHON
hello python
Hello Python
```

### `strip()`

Removes whitespace from the beginning and end.

```python
text = "   Hello Python   "

print(text.strip())
```

Result:

```text
Hello Python
```

This is useful for cleaning user input before processing it.

---

## 11. Searching inside strings

Use `in` to check whether a substring exists.

```python
text = "I love Python"

print("Python" in text)
```

Output:

```text
True
```

```python
print("Java" in text)
```

Output:

```text
False
```

This can be useful when performing simple text processing.

---

# String Indexing

## 12. Indexing starts at 0

Consider:

```python
text = "Python"
```

The indexes are:

```text
 P    y    t    h    o    n
 0    1    2    3    4    5
```

Access an individual character:

```python
print(text[0])
```

Output:

```text
P
```

```python
print(text[2])
```

Output:

```text
t
```

Python uses **zero-based indexing**.

---

## 13. Negative indexing

Python also allows indexing from the end.

```text
 P    y    t    h    o    n
 0    1    2    3    4    5
-6   -5   -4   -3   -2   -1
```

Therefore:

```python
print(text[-1])
```

Output:

```text
n
```

```python
print(text[-2])
```

Output:

```text
o
```

---

# String Slicing ⭐⭐⭐

## 14. Basic slicing

Syntax:

```python
text[start:end]
```

Important rule:

> **Start is included, end is excluded.**

Example:

```python
text = "Python"

print(text[0:2])
```

Result:

```text
Py
```

Index `0` is included, but index `2` is excluded.

---

## 15. Useful slicing patterns

```python
text = "Python"

print(text[:3])
print(text[3:])
print(text[-5:])
print(text[:-2])
```

Meaning:

```text
text[:3]     → first 3 characters
text[3:]     → from index 3 to the end
text[-5:]    → last 5 characters
text[:-2]    → everything except the last 2 characters
```

### Important example

To get the last 5 characters:

```python
text[-5:]
```

Do NOT use:

```python
text[-5:-1]
```

because the ending index `-1` is excluded.

---

## 16. Slicing with a step

Syntax:

```python
text[start:end:step]
```

Example:

```python
text = "Python"

print(text[::2])
```

This takes every second character.

---

## 17. Reverse a string

A common Python shortcut:

```python
text = "Python"

print(text[::-1])
```

Output:

```text
nohtyP
```

The `-1` step means move backwards.

---

# Strings are immutable

## 18. Strings cannot be changed in-place

This is invalid:

```python
text = "Python"

text[0] = "J"
```

Strings are **immutable**.

Instead, create a new string:

```python
text = "Python"

text = "J" + text[1:]

print(text)
```

Output:

```text
Jython
```

Understanding **mutable vs immutable** objects will become important when we learn lists and dictionaries.

---

# AI/ML Connection

Strings are fundamental to AI applications.

A typical LLM application may look like:

```text
User question
      ↓
Python string
      ↓
Clean / process text
      ↓
Create prompt
      ↓
LLM API
      ↓
LLM response
      ↓
Python string
      ↓
Display answer
```

Example:

```python
user_question = "   What is semantic search?   "

clean_question = user_question.strip()

prompt = f"""
Explain this concept to a software engineer:

{clean_question}
"""
```

The concepts learned in this lesson are therefore directly relevant to:

* LLM prompts
* RAG
* document processing
* text preprocessing
* API requests
* agent instructions
* chatbot applications

---

# Quick Reference

```python
# Variable
name = "Mini"

# Type
type(name)

# Length
len(name)

# String methods
name.upper()
name.lower()
name.strip()
name.title()

# Check substring
"Mini" in name

# Indexing
name[0]
name[-1]

# Slicing
name[:3]
name[3:]
name[-5:]

# Reverse
name[::-1]

# f-string
f"My name is {name}"
```

## Key concepts to remember

1. Python variables do not require explicit type declarations.
2. Python is dynamically typed.
3. Variables are names/references to objects.
4. Strings have type `str`.
5. Python uses zero-based indexing.
6. Negative indexes count from the end.
7. Slicing uses `[start:end]`.
8. The start index is included; the end index is excluded.
9. `text[-5:]` gives the last five characters.
10. Strings are immutable.
11. f-strings are extremely useful for dynamic text and LLM prompts.
12. Strings are one of the fundamental building blocks of AI applications.
