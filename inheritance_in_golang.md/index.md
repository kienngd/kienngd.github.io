# Inheritance in GoLang


**Inheritance** is an important concept in OOP (Object-Oriented Programming). Since Golang does not support classes, there is **no inheritance concept in GoLang**. However, you can implement inheritance through **struct embedding**.

<!--more-->

In composition, base structs can be embedded into a child struct, and the methods of the base struct can be directly called on the child struct, as shown in the following example.

```go
package main

import "fmt"

func main() {
	fmt.Println("Demo inheritance in GoLang!")
	customer := Customer{
		Person: Person{
			name: "John Doe",
			age:  30,
		},
		email:  "john@gmail.com",
		is_vip: true,
	}
	customer.Person.DisplayInfo()
	customer.DisplayInfo()
}

// region Person functions
type Person struct {
	name string
	age  int
}

func (u Person) DisplayInfo() {
	fmt.Printf("Name: %s, Age: %d\n", u.name, u.age)
}

// endregion User functions

// region Customer functions
type Customer struct {
	Person
	email  string
	is_vip bool
}
```

You can embed as many base structs as you want
