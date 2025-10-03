# Building custom classes

Classes are the cornerstone of object-oriented programming (OOP) in Python. They provide a structured blueprint for creating objects, the fundamental building blocks of your applications. Imagine classes as molds for cookies. Each cookie (object) is unique, yet they all share the same basic shape and structure (class). With classes, you can define the properties (attributes) and behaviors (methods) that these objects will possess.

## Understanding object-oriented programming

Imagine building a virtual zoo. In an OOP world, each animal wouldn't be a mere collection of characteristics and actions. Instead, each animal would be represented as an object—a distinct instance of a class. A Lion class might have attributes like `name`, `species`, `age`, and `mane_color`. Its methods could include `roar()`, `hunt()`, and `sleep()`. Similarly, a Monkey class would have its own unique attributes and methods. 

These are the essential components of OOP.

### Encapsulation

Encapsulation in Python is achieved primarily through a convention rather than strict enforcement. It revolves around using a single underscore (_) prefix for attribute names to signal that they are intended for internal use within the class. While Python doesn't prevent direct access to these "private" attributes from outside the class, the underscore serves as a clear indication to other developers that these attributes should be treated as part of the class's internal implementation and not modified directly.

Let's see this in action with a `BankAccount` example:

```py
class BankAccount:
    def __init__(self, balance):
        self._balance = balance  # Private attribute

    def deposit(self, amount):
        self._balance += amount

    def get_balance(self):
        return self._balance
```

In this example, the `_balance` attribute is marked as private. While you could technically access and modify it directly from outside the class (for example., `my_account._balance = 1000`), doing so would violate the principle of encapsulation. The class provides the `deposit()` and `get_balance()` methods as the proper interface for interacting with the account's balance.

### Abstraction

Abstraction empowers you to concentrate on the core functionality of an object without getting entangled in the intricacies of its implementation. Python's abc module (Abstract Base Classes) takes this a step further by enabling you to define abstract base classes. These classes serve as blueprints for other classes, outlining essential methods that concrete subclasses must implement.

```py
from abc import ABC, abstractmethod

class Animal(ABC):  # Abstract base class
    @abstractmethod
    def make_sound(self):
        pass

class Dog(Animal):  # Concrete subclass
    def make_sound(self):
        return "Bark!"
```

In this example, `Animal` is an abstract base class. It declares an abstract method `make_sound()`, which doesn't have a concrete implementation. Any class inheriting from `Animal` (like `Dog`) must provide its own implementation of `make_sound()`.
