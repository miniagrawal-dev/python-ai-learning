# Lesson 11 — Classes & OOP in Python

## 1. What is a Class?

A class is a blueprint for creating objects.

Python:

```python
class User:
    def __init__(self, name):
        self.name = name
```

Create an object:

```python
user = User("Mini")

print(user.name)
```

Output:

```text
Mini
```

Unlike Java, Python does not use `new`:

```text
Java   → new User(...)
Python → User(...)
```

---

# 2. `__init__`

`__init__` is Python's initializer method.

```python
class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

Create:

```python
user = User("Mini", 31)

print(user.name)
print(user.age)
```

`__init__` runs automatically when an object is created.

Mental model:

```text
User(...)
   ↓
__init__()
   ↓
object initialized
```

---

# 3. `self`

`self` refers to the current object.

```python
class User:
    def __init__(self, name):
        self.name = name

    def introduce(self):
        print(f"My name is {self.name}")
```

Usage:

```python
user = User("Mini")
user.introduce()
```

Java uses:

```java
this.name
```

Python uses:

```python
self.name
```

Mental model:

```text
Java   → this
Python → self
```

`self` must explicitly appear in instance method definitions.

---

# 4. Instance Methods

Example:

```python
class User:
    def __init__(self, name):
        self.name = name

    def greet(self):
        return f"Hello, {self.name}"
```

Usage:

```python
user = User("Mini")

print(user.greet())
```

Output:

```text
Hello, Mini
```

Python automatically passes the object as `self` when calling:

```python
user.greet()
```

You don't explicitly pass `self`.

---

# 5. Object State and Behavior

An object can contain:

* State → attributes
* Behavior → methods

Example:

```python
class AIModel:
    def __init__(self, name, temperature):
        self.name = name
        self.temperature = temperature

    def generate(self, prompt):
        return f"{self.name} generated: {prompt}"
```

Mental model:

```text
AIModel
 ├── State
 │    ├── name
 │    └── temperature
 │
 └── Behavior
      └── generate()
```

This pattern appears frequently in AI libraries.

---

# 6. Class Attributes

A class attribute is shared by instances unless overridden.

```python
class AIModel:
    provider = "OpenAI"

    def __init__(self, name):
        self.name = name
```

Usage:

```python
model1 = AIModel("model-a")
model2 = AIModel("model-b")

print(model1.provider)
print(model2.provider)
```

Both access:

```text
OpenAI
```

Here:

```text
provider → class attribute
name     → instance attribute
```

---

# 7. Instance vs Class Attributes

Example:

```python
class AIModel:
    provider = "OpenAI"

    def __init__(self, name):
        self.name = name
```

Conceptually:

```text
Class:
    provider = OpenAI

Object 1:
    name = model-a

Object 2:
    name = model-b
```

Instance attributes belong to individual objects.

Class attributes belong to the class and can be shared.

---

# 8. Dunder Methods

Methods with double underscores are called **dunder methods**.

Examples:

```python
__init__
__str__
__repr__
```

They provide special behavior to Python objects.

---

# 9. `__str__`

`__str__` controls the user-friendly string representation of an object.

```python
class User:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"User(name={self.name})"
```

Now:

```python
user = User("Mini")

print(user)
```

Output:

```text
User(name=Mini)
```

---

# 10. `__repr__`

`__repr__` is generally intended to provide a useful representation for developers/debugging.

```python
class User:
    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return f"User(name='{self.name}')"
```

You will encounter `__repr__` frequently in Python libraries.

---

# 11. Inheritance

Python supports inheritance.

Parent:

```python
class Animal:
    def speak(self):
        print("Animal speaks")
```

Child:

```python
class Dog(Animal):
    def bark(self):
        print("Dog barks")
```

Usage:

```python
dog = Dog()

dog.speak()
dog.bark()
```

Output:

```text
Animal speaks
Dog barks
```

Java:

```java
class Dog extends Animal
```

Python:

```python
class Dog(Animal):
```

---

# 12. Method Overriding

A child class can override a parent method.

```python
class Animal:
    def speak(self):
        print("Animal speaks")


class Dog(Animal):
    def speak(self):
        print("Dog barks")
```

Usage:

```python
dog = Dog()
dog.speak()
```

Output:

```text
Dog barks
```

---

# 13. `super()`

`super()` allows a child class to call parent functionality.

```python
class Animal:
    def __init__(self, name):
        self.name = name


class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed
```

Usage:

```python
dog = Dog("Bruno", "Labrador")

print(dog.name)
print(dog.breed)
```

Similar Java concept:

```java
super(name);
```

---

# 14. Encapsulation in Python

Python does not enforce private fields in the same way as Java.

Java:

```java
private String name;
```

Python convention:

```python
self._name
```

A leading underscore communicates:

> This attribute is intended for internal use.

It is a convention rather than strict access control.

---

# 15. Double Underscore Attributes

Python also supports:

```python
self.__password
```

This triggers **name mangling**.

It should not be considered exactly equivalent to Java's `private`.

Python generally relies more heavily on conventions.

---

# 16. `@property`

`@property` allows a method to be accessed like an attribute.

```python
class User:
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name
```

Usage:

```python
user = User("Mini")

print(user.name)
```

Instead of:

```python
user.name()
```

Properties are useful when you want controlled or computed attribute access.

---

# 17. Static Methods

Python supports static methods using `@staticmethod`.

```python
class MathUtils:

    @staticmethod
    def add(a, b):
        return a + b
```

Usage:

```python
result = MathUtils.add(10, 20)

print(result)
```

No object is required.

Java has the equivalent concept:

```java
static int add(int a, int b)
```

---

# 18. Class Methods

Python supports class methods using `@classmethod`.

```python
class AIModel:

    provider = "OpenAI"

    @classmethod
    def get_provider(cls):
        return cls.provider
```

Usage:

```python
print(AIModel.get_provider())
```

Output:

```text
OpenAI
```

Important distinction:

```text
self → instance
cls  → class
```

---

# 19. Dataclasses — Preview

Python provides dataclasses for classes primarily used to hold data.

```python
from dataclasses import dataclass

@dataclass
class User:
    name: str
    age: int
```

Usage:

```python
user = User("Mini", 31)

print(user)
```

Dataclasses automatically provide useful functionality such as an initializer and representation.

Dataclasses will be covered in detail in a later lesson.

---

# 20. AI Example — Retriever Class

A simple document retriever can be represented as a class:

```python
class Retriever:

    def __init__(self, documents):
        self.documents = documents

    def search(self, query):
        results = []

        for document in self.documents:
            if query.lower() in document.lower():
                results.append(document)

        return results
```

Create the retriever:

```python
documents = [
    "Python is useful for AI",
    "Kafka is a messaging system",
    "RAG uses document retrieval"
]

retriever = Retriever(documents)
```

Search:

```python
results = retriever.search("Python")

print(results)
```

Output:

```text
['Python is useful for AI']
```

Object structure:

```text
Retriever
   │
   ├── documents  ← state
   │
   └── search()   ← behavior
```

This is a simple version of the abstractions used in real retrieval libraries.

---

# 21. AI Example — LLM Client

A simple LLM client might look like:

```python
class LLMClient:

    def __init__(self, model, temperature):
        self.model = model
        self.temperature = temperature

    def generate(self, prompt):
        return f"Calling {self.model} with: {prompt}"
```

Usage:

```python
llm = LLMClient(
    model="my-model",
    temperature=0.2
)

response = llm.generate("Explain embeddings")

print(response)
```

Eventually, `generate()` could call an actual LLM API.

---

# 22. Why OOP Matters for AI

When using libraries such as:

```text
Pydantic
FastAPI
LangChain
LlamaIndex
Hugging Face
OpenAI SDK
```

you'll frequently see objects:

```python
model = ...
retriever = ...
client = ...
document = ...
embedding_model = ...
```

and method calls:

```python
model.invoke(...)
retriever.search(...)
client.responses.create(...)
```

Understanding classes helps you understand:

* What object was created?
* What state does it hold?
* What methods does it provide?
* What inputs do those methods expect?
* What does the object return?

This is much more useful than simply memorizing library syntax.

---

# 23. Python vs Java — Quick Comparison

| Java                   | Python                               |
| ---------------------- | ------------------------------------ |
| `new User()`           | `User()`                             |
| `this.name`            | `self.name`                          |
| `extends`              | `class Child(Parent)`                |
| `super()`              | `super()`                            |
| `private`              | Convention such as `_name`           |
| Getters/setters        | `@property`                          |
| Interfaces             | ABC / Protocol                       |
| POJOs                  | Dataclasses / Pydantic               |
| Explicit types usually | Dynamic typing + optional type hints |
| Constructor            | `__init__`                           |

Don't try to write Python OOP exactly like Java OOP.

Python has its own conventions and idioms.

---

# 24. AI Engineering Mental Model

Think of an AI component as an object containing state and behavior.

```text
                    Object
                       │
             ┌─────────┴─────────┐
             │                   │
           State              Behavior
             │                   │
      model/config/data       methods
             │                   │
             └─────────┬─────────┘
                       ↓
                 AI operation
```

For example:

```text
Retriever
 ├── documents
 └── search()

LLMClient
 ├── model
 ├── temperature
 └── generate()

EmbeddingModel
 ├── model
 └── embed()
```

This mental model will help you read real AI code later.

---

# 25. Key Takeaways

1. A class is a blueprint for creating objects.
2. Objects contain state and behavior.
3. `__init__` initializes an object.
4. `self` refers to the current instance.
5. Python doesn't use `new` when creating objects.
6. Instance attributes belong to individual objects.
7. Class attributes can be shared by instances.
8. Dunder methods provide special object behavior.
9. `__str__` provides a user-friendly string representation.
10. `__repr__` provides a useful developer representation.
11. Python supports inheritance and method overriding.
12. `super()` calls parent functionality.
13. Python relies more on conventions for encapsulation than Java.
14. `@property` provides attribute-like access to methods.
15. `@staticmethod` defines a method that doesn't need an instance.
16. `@classmethod` receives the class as `cls`.
17. Dataclasses provide a concise way to define data-oriented classes.
18. AI libraries heavily use objects, classes, and methods.
19. Understanding OOP helps you understand unfamiliar AI libraries instead of merely memorizing APIs.

---

# 26. Quick Reference

### Class

```python
class User:
    def __init__(self, name):
        self.name = name
```

### Object

```python
user = User("Mini")
```

### Instance method

```python
def greet(self):
    return "Hello"
```

### Inheritance

```python
class Dog(Animal):
    pass
```

### Parent method

```python
super().__init__(name)
```

### Property

```python
@property
def name(self):
    return self._name
```

### Static method

```python
@staticmethod
def add(a, b):
    return a + b
```

### Class method

```python
@classmethod
def create(cls):
    return cls()
```

---

# 27. Where This Fits in Your AI Learning Path

You now have:

```text
Variables
   ↓
Strings
   ↓
Lists
   ↓
Dictionaries / Tuples / Sets
   ↓
Conditions / Loops
   ↓
Functions
   ↓
Comprehensions / Lambda
   ↓
Modules / Packages
   ↓
Exceptions
   ↓
File I/O / JSON
   ↓
Classes / OOP        ← YOU ARE HERE
```

Next:

```text
Dataclasses
   ↓
Pydantic
   ↓
Iterators / Generators
   ↓
Decorators
   ↓
Context Managers
   ↓
Type Hints
   ↓
Async / Await
```

These Python concepts will form the foundation for the later **FastAPI → AI/ML → LLM → RAG → Agents → Production AI** stages.
