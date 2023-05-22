# GIT Commit message conventions


Consider using the following pattern and ask yourself the corresponding questions: [scope][typePrefix][baseName][qualifier][typeSuffix].

## Scope:

- What is the visibility or accessibility of this variable? (e.g., private, public, protected, internal, package-private)
- Is this variable specific to any programming language features or conventions? (e.g., double underscore prefix in Python, dollar sign in jQuery, '@' for instance variables in Ruby)
- Is this variable part of a framework or library that requires a specific naming pattern? (e.g., Angular's 'ng' prefix for directives, React's 'use' prefix for hooks)

## TypePrefix

- Is this variable a boolean or a function that returns a boolean? (e.g., is, has, contains, are, integrates)
- Does the variable represent a state, condition, or action that can be described with words like "is," "has," "contains," or "integrates"? (e.g., isEnabled, hasAccess, containsItem)
- Is this a function responsible for getting, setting, fetching, or updating data? (e.g., get, set, fetch, update, retrieve, store, save)

## BaseName:
- What is the primary purpose of this variable? (e.g., user, distance, payment, errorMessage)
- Can I describe the variable's role in the code with a clear, concise word or phrase? (e.g., registrationStatus, totalPrice, elapsedTime)

## Qualifier:
- Are there any additional details or context that would help distinguish this variable from others with a similar purpose? (e.g., firstName, lastName, phoneNumber)
- Does the variable have specific units or properties that should be included in the name, such as "InMeters" or "InSeconds"? (e.g., distanceInMiles, timeInSeconds)
- Is there a specific state or condition that this variable represents, such as "Valid" or "Removable"? (e.g., isValidEmail, isRemovableItem)

## TypeSuffix:
- What is the fundamental purpose or structure of this variable? (e.g., Count, Index, Sum, Average, List, Map, Array, Set, Queue)
- Can the variable's role be clarified by adding a suffix for the structure like "Count," "Index," "Sum," "Average," "List," or "Map"? (e.g., itemCount, currentIndex, totalPriceSum, ratingAverage, userList, settingsMap)


## Examples:
**fetchProductById**:
- scope: “” (Public methods dont have a specific prefix in most languages)
- typePrefix: fetch (function)
- baseName: Product
- qualifier: ById

**updateEmailPreference**:
- scope: "" (public)
- typePrefix: update (function)
- baseName: Email
- qualifier: Preference

**getUserByEmail**:
- typePrefix: get (function)
- baseName: User
- qualifier: ByEmail

~~getUserLoggedIn~~ **getLoggedInUser** <span style="color: #FF0000">(swap the base name and qualifier in order to give the variable a more appropriate and meaningful name)</span>
- typePrefix: get (function)
- qualifier: LoggedIn
- baseName: User

