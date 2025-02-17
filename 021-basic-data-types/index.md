# Basic data types


Basic data types

<!--more-->

**Tuples**
- Tuple is one of 4 built-in data types in Python used to store collections of data, the other 3 are List, Set, and Dictionary, all with different qualities and usage.
- A tuple is a collection which is ordered and **unchangeable**.
- A tuple can contain different data types
- Can access items by index: `mytuple[0], mytuple[1]`
- Allow duplicate-values
- Tuple len: `len(mytuple)`
- Example:
  ```python
  thistuple = ("apple", "banana", "cherry")
  print(thistuple)

  thistuple = ("apple",) #! Have , at the end of list
  print(thistuple)

  thistuple = (1, "two", 3) # Multiple type-items
  print(thistuple)

  # Use constructor
  thistuple = tuple(("apple", "banana", "cherry")) # note the double round-brackets
  print(thistuple)
  ```
