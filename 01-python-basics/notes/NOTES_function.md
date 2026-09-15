# Lesson 6 — Functions

## 1. Overview

A function is a reusable block of code.

Python functions are conceptually similar to Java methods, but Python has:

* Less syntax
* Dynamic typing
* Optional type hints
* Default parameters
* Keyword arguments
* `*args`
* `**kwargs`
* Multiple return values

Functions are fundamental to:

* Backend APIs
* Data processing
* ML pipelines
* LLM applications
* RAG pipelines
* Tool calling
* AI agents

---

# 2. Basic Function

```python
def say_hello():
    print("Hello")
```

Call the function:

```python
say_hello()
```

General structure:

```python
def function_name():
    # code
```

Python requires:

* `def`
* function name
* `()`
* `:`
* indentation

---

# 3. Function Parameters

```python
def greet(name):
    print("Hello", name)
```

Call:

```python
greet("Mini")
```

Terminology:

```text
name
 ↓
parameter

"Mini"
 ↓
argument
```

### Java comparison

Python:

```python
def greet(name):
    print("Hello", name)
```

Java:

```java
void greet(String name) {
    System.out.println("Hello " + name);
}
```

---

# 4. Multiple Parameters

```python
def add(a, b):
    print(a + b)
```

Call:

```python
add(10, 20)
```

---

# 5. `return`

`return` sends a value back to the caller.

```python
def add(a, b):
    return a + b
```

Now:

```python
result = add(10, 20)

print(result)
```

Output:

```text
30
```

Mental model:

```text
function
   ↓
input
   ↓
processing
   ↓
return output
```

---

# 6. `print()` vs `return`

## `print()`

```python
def add(a, b):
    print(a + b)
```

This displays the value.

## `return`

```python
def add(a, b):
    return a + b
```

This gives the value back to the caller.

Therefore:

```python
result = add(10, 20)
```

only works meaningfully when the function returns a value.

### Important rule

Use `return` when the result needs to be:

* stored
* reused
* passed to another function
* tested
* processed further

---

# 7. Returning Multiple Values

Python can return multiple values conveniently.

```python
def get_user():
    return "Mini", 31
```

Then:

```python
name, age = get_user()
```

This works through tuple unpacking.

Conceptually:

```text
return ("Mini", 31)
        ↓
name, age
```

---

# 8. Default Parameters

A parameter can have a default value.

```python
def greet(name="Guest"):
    print("Hello", name)
```

Calling:

```python
greet()
```

produces:

```text
Hello Guest
```

Calling:

```python
greet("Mini")
```

produces:

```text
Hello Mini
```

Default parameters are useful for optional configuration.

---

# 9. Keyword Arguments

Parameters can be specified by name.

```python
def create_user(name, age):
    return {
        "name": name,
        "age": age
    }
```

Positional arguments:

```python
create_user("Mini", 31)
```

Keyword arguments:

```python
create_user(name="Mini", age=31)
```

Keyword arguments can also change the order:

```python
create_user(age=31, name="Mini")
```

This makes function calls more readable.

---

# 10. Why Keyword Arguments Matter in AI

AI libraries often have many configuration parameters.

Example:

```python
generate_response(
    model="some-model",
    temperature=0.2,
    max_tokens=500
)
```

This is easier to understand than:

```python
generate_response("some-model", 0.2, 500)
```

Keyword arguments are therefore very common in AI and Python libraries.

---

# 11. Type Hints

Python allows optional type hints.

```python
def add(a: int, b: int) -> int:
    return a + b
```

Meaning:

```text
a       → expected int
b       → expected int
return  → expected int
```

Another example:

```python
def greet(name: str) -> str:
    return f"Hello {name}"
```

Type hints improve:

* Readability
* IDE support
* Static analysis
* Documentation
* Maintainability

---

# 12. Type Hints Are Not Java-Style Enforcement

Python type hints generally don't enforce the type at runtime.

For example:

```python
def add(a: int, b: int) -> int:
    return a + b
```

The type annotation doesn't itself make Python behave like Java's compile-time type checking.

Python remains dynamically typed.

Later, tools such as **Pydantic** can provide runtime validation.

---

# 13. Functions Returning Dictionaries

Very common in backend and AI applications.

```python
def create_response(answer, score):
    return {
        "answer": answer,
        "score": score
    }
```

Use:

```python
response = create_response(
    "RAG retrieves relevant context.",
    0.95
)
```

Result:

```python
{
    "answer": "RAG retrieves relevant context.",
    "score": 0.95
}
```

---

# 14. Functions + Lists

Functions can process collections.

```python
def get_titles(documents):
    titles = []

    for document in documents:
        titles.append(document["title"])

    return titles
```

Example:

```python
documents = [
    {"title": "Python", "score": 0.91},
    {"title": "RAG", "score": 0.95}
]

titles = get_titles(documents)

print(titles)
```

Result:

```text
['Python', 'RAG']
```

---

# 15. Functions + Conditions

Functions can encapsulate decision logic.

```python
def classify_score(score):
    if score >= 0.9:
        return "high"
    elif score >= 0.7:
        return "medium"
    else:
        return "low"
```

Example:

```python
classify_score(0.95)
```

returns:

```text
high
```

---

# 16. Functions + Loops

Functions can encapsulate processing workflows.

```python
def get_relevant_documents(documents, threshold):
    results = []

    for document in documents:
        if document["score"] >= threshold:
            results.append(document)

    return results
```

Call:

```python
relevant = get_relevant_documents(documents, 0.9)
```

This pattern is directly applicable to RAG systems.

---

# 17. Default Parameter in AI Processing

```python
def filter_documents(documents, threshold=0.8):
    results = []

    for document in documents:
        if document["score"] >= threshold:
            results.append(document)

    return results
```

The default threshold is `0.8`.

Use default:

```python
filter_documents(documents)
```

Override:

```python
filter_documents(documents, threshold=0.9)
```

---

# 18. `*args`

`*args` allows a function to accept a variable number of positional arguments.

```python
def add_all(*numbers):
    return sum(numbers)
```

Examples:

```python
add_all(1, 2)
```

```python
add_all(1, 2, 3, 4)
```

Inside the function:

```python
numbers
```

is a **tuple**.

Example:

```python
def show(*args):
    print(args)

show(1, 2, 3)
```

Output:

```text
(1, 2, 3)
```

### Mental model

```text
*args
   ↓
tuple
```

---

# 19. `**kwargs`

`**kwargs` allows a function to accept a variable number of keyword arguments.

```python
def show_config(**kwargs):
    print(kwargs)
```

Call:

```python
show_config(
    model="gpt",
    temperature=0.2,
    max_tokens=500
)
```

Inside the function, `kwargs` is a dictionary:

```python
{
    "model": "gpt",
    "temperature": 0.2,
    "max_tokens": 500
}
```

### Mental model

```text
**kwargs
   ↓
dictionary
```

---

# 20. `*args` vs `**kwargs`

Remember:

```text
*args
 ↓
variable positional arguments
 ↓
tuple
```

```text
**kwargs
 ↓
variable keyword arguments
 ↓
dictionary
```

Example:

```python
def inspect_data(*args, **kwargs):
    print(args)
    print(kwargs)
```

Call:

```python
inspect_data(
    "document1",
    "document2",
    threshold=0.9,
    model="gpt"
)
```

Conceptually:

```text
args
→ ("document1", "document2")

kwargs
→ {
     "threshold": 0.9,
     "model": "gpt"
   }
```

Don't automatically use `*args` and `**kwargs` everywhere. Explicit parameters are generally clearer when the function's inputs are known.

---

# 21. Scope

Variables created inside a function are normally local to that function.

```python
def test():
    x = 10
    print(x)
```

`x` belongs to the function's local scope.

This won't work outside the function:

```python
print(x)
```

because `x` was created inside `test()`.

---

# 22. Global Variables

Example:

```python
model = "gpt"

def show_model():
    print(model)

show_model()
```

The function can read the global variable.

However, avoid excessive use of global state.

Prefer:

```python
def show_model(model):
    print(model)
```

Passing dependencies explicitly generally makes code:

* Easier to understand
* Easier to test
* Easier to reuse

---

# 23. AI Example — Building a Prompt

A function can encapsulate prompt construction.

```python
def build_prompt(question, context):
    prompt = f"""
Answer the question using the provided context.

Context:
{context}

Question:
{question}
"""
    return prompt
```

Use:

```python
context = "RAG combines retrieval with generation."
question = "What is RAG?"

prompt = build_prompt(question, context)

print(prompt)
```

Conceptually:

```text
Question + Context
       ↓
build_prompt()
       ↓
Prompt
       ↓
LLM
       ↓
Answer
```

---

# 24. AI Example — RAG Filtering

```python
def filter_documents(documents, threshold=0.8):
    results = []

    for document in documents:
        if document["score"] >= threshold:
            results.append(document)

    return results
```

Conceptually:

```text
Retrieved documents
        ↓
filter_documents()
        ↓
Relevant documents
        ↓
Prompt construction
        ↓
LLM
```

This is the beginning of a RAG pipeline.

---

# 25. Python Function Mental Model for AI

A typical AI pipeline can be decomposed into functions:

```text
load_documents()
       ↓
split_documents()
       ↓
create_embeddings()
       ↓
retrieve_documents()
       ↓
filter_documents()
       ↓
build_prompt()
       ↓
call_llm()
       ↓
parse_response()
```

Each function should ideally have a clear responsibility.

This leads toward the software-engineering principle:

> **Keep functions focused on one responsibility.**

---

# 26. Java → Python Mental Translation

| Java                | Python                                                     |
| ------------------- | ---------------------------------------------------------- |
| Method              | Function                                                   |
| `void`              | No explicit return annotation / function may return `None` |
| `return`            | `return`                                                   |
| Method parameters   | Function parameters                                        |
| Overloading         | Not normally done in the same way                          |
| `Map`               | `dict`                                                     |
| `List`              | `list`                                                     |
| `Object... args`    | `*args`                                                    |
| Named configuration | Keyword arguments / `**kwargs`                             |
| Type declaration    | Optional type hints                                        |

---

# 27. Important Python Syntax to Remember

Basic:

```python
def function_name():
    ...
```

Parameter:

```python
def function_name(value):
    ...
```

Return:

```python
def function_name(value):
    return value
```

Default:

```python
def function_name(value=10):
    ...
```

Type hints:

```python
def function_name(value: int) -> int:
    ...
```

Variable arguments:

```python
def function_name(*args):
    ...
```

Variable keyword arguments:

```python
def function_name(**kwargs):
    ...
```

---

# 28. Key Takeaways

The most important concepts from this lesson:

### 1. Functions

```python
def function():
    ...
```

### 2. Parameters

```python
def function(value):
    ...
```

### 3. Return

```python
return result
```

### 4. Default parameters

```python
def function(value=10):
    ...
```

### 5. Keyword arguments

```python
function(value=10)
```

### 6. Type hints

```python
def add(a: int, b: int) -> int:
    return a + b
```

### 7. Variable arguments

```python
*args
```

→ tuple

```python
**kwargs
```

→ dictionary

### 8. AI relevance

Functions will encapsulate:

```text
data processing
retrieval
embedding generation
prompt construction
LLM calls
tool execution
response parsing
agent logic
```

---

# Lesson 6 Complete

At this point, the core Python fundamentals covered are:

```text
Variables & Types
        ↓
Strings
        ↓
Lists
        ↓
Dictionaries / Tuples / Sets
        ↓
Conditions & Loops
        ↓
Functions
```

The next lesson will be **List/Dictionary Comprehensions + Lambda + `map()` + `filter()`**.

This is where Python starts feeling significantly different from Java, and these constructs appear frequently in data-processing and AI code.
