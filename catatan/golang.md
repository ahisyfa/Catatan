# Golang
## Introduction

## Create Project
- Project in GoLang called as a module
```
go mod init module-name
```

## Compile
```
go build
```

## Run 
```
go run hello-go.go
```

## Data type
### Number
- int8 
- int16
- int32
- int64

- uint8
- uint16
- uint32
- uint64
### Floating Point
- float32
- float64
- complex64
- complex128

### Alias
- byte -> unint8
- rune -> int32
- int -> minimal int32
- uint -> minimal uint32

### Boolean
- true
- false


### String
represented by keyword `string` 
```
fmt.Pritnln("Amin")
```
String function
- len("string")
- "syring"[number] -> get char at specific index

## Variable
- A place to store data
- Only for store specific data
- Keyword `var` 
```go
func main() {
   var name string
   name = "Amin"
   fmt.Println(name)

}
```

###  Declare Variable
- When we declare a variable, we must declare the data-type of the variable
- But, if we directly initiate the value of variable we NOT MUST declare the data-type
```go
func main() {
   var originalname string = "Amin"
   var name = "Amin"
   fmt.Println(name)
}
```

### Var Keyword
- var keyword is not mandatory when we direct initialize the value to variable
- we can use `:=` if we want not to use var
```go
func main() {
   name := "Amin"
   fmt.Println(name)
}
```

### Declare Multiple Variable
- Keywrod var()
```go
func main() {
   var(
     name = "Amin"
   )
   fmt.Println(name)
}
```

## Constant
- Keyword: `const`
```go
func main() {
   const name string = "Amin"
   const name2 = "Amin"
   fmt.Println(name)
   
   const (
     var1 = "apa"
     var2 = 124
   )
}
```

## Data-type Conversion
```go
func main() {
   var somevalueInt32 int32 = 12121
   var somevalueInt64 int64 = int64(somevalueInt32)
   
   var name = "Amin"
   var A = name[0]
   var aString = string(A)
}
```

## Type Declarations
- Type Declarations is the ability to recreate new data-type from existing data-type
- Type Declarations usually used to create alias for existing data-type for purpose easy to understand
```go
func main() {
   type NoKtp string
   
   var ktpAmin NoKtp = "ABCD"
}
```

## Mathematical Operation
- +
- -
- *
- /
- %
### Augmented Assignment
```go 
func main() {
   var a = 10
   a+=10
   
   fmt.Println(a)
}
```

### Unary operation 
```go 
++
--
-
+
!
```

### Comparison Operator  
```go 
>
<
>=
<=
==
!=
```
### Boolean Operation
```go 
&&
||
```


## Array
- Kumpulan data dengan type yang sama
- Saat membuat array kita perlu menentukan jumlah yang bisa ditampung
- Daya tampung tidak bisa bertambah setelah dibuat
```go
func main() {
   var name [3]string
   name[0] = "Ahmad"
   name[1] = "Isyfalana"
   name[2] = "Amin"   
   
   fmt.Println(name)
   // OR 
   var values = [3]int{
      10,
      20,
      30, // Must end with ,
   } 
   fmt.Println(values)

   var values1 = [3]int{10,20,30} 
   fmt.Println(values1)
   
   // Dynamic length with three dot
   var values2 = [...]int{10,20,30} 
   fmt.Println(values2)
      
   var otherValues = [3]int{}
   fmt.Println(otherValues)
   
   // Array Function
   len(otherValues) // get array length
   otherValues[0]  // get value at some index
   otherValues[0] = -11 // change the value at some index
}
```

## Slice
- Data-type Slice adalah potongan dari array
- Slice mirip dengan Array, yang memdedakan adalah ukuran slice bisa berubah
- Slice dan array selalu terkoneksi, dimana slice adalah data yang mengakses sebagian atau seluruh data di Array
- Tipe data Slice memiliki 3 data: pointer, length dan capacity
- Pointer -> penujuk data pertama di array pada slice
- length -> panjang dari slice
- capacity -> kapasitas dari slice, length tidak boleh lebih dari capcity
### Create Slice From Array
```go
array[low:high] 
array[low:]
array[:high]
array[:]
```
![[Pasted image 20250827222550.png]]
```go
package main
import "fmt"

func main() {
	moonth := [...]string{
	"0-januari",
	"1-februari",
	"2-maret",
	"3-april",
	"4-mei",
	"5-juni",
	"6-juli",
	"7-agustus",
	"8-september",
	"9-oktober",
	"10-nopember",
	"11-desember",
	}
	
	slice1 := moonth[4:7]
	fmt.Println(slice1)
	
	var slice2 []string = moonth[1:7]
	fmt.Println(slice2)
	
	# Function Slice
	leng(slice2)
	cap(slice2)
	append(slice, data)
	make([]TypeData, length, capacity)
	copy(destination, source))
}
```
### Array vs Slice
```go
var someArray [3]string
var someSlice []string       // => has no initial length
```

## Map
```go
package main
import "fmt"

func main() {
	var person map[string]string
	person = map[string]string{
	"key1": "value1",
	}
	fmt.Println(person)
	fmt.Println(person["key1"])
	
	animal := make(map[string]string)
	fmt.Println(animal)
	
	animal["cat"] = "kucing"
	fmt.Println(animal)
	
	delete(animal, "cat")
	fmt.Println(animal)
}
```

## Branching
### If
```go
func main() {
	name := "Udin"

	if name == "Amin" {
		fmt.Println("Hello Amin")
	} else if name == "Udin" {
		fmt.Println("Hai Udin")
	} else {
		fmt.Println("Hai")
	}
}
```

### If with Short Statement
```go
func main() {
	name := "Udin"

	if length :=len(name); length > 5 {
		fmt.Println("Long name")
	} else {
		fmt.Println("ShortName")
	}
}
```

### Switch
```go
package main

import "fmt"

func main() {
	name := "Udina"

	switch name {
	case "Udin":
		fmt.Println("Hello udin")
	case "Amin":
		fmt.Println("Hello amin")
	default:
		fmt.Println("Hello")
	}
	
	// With Short Statement
	switch length :=len(name); length < 5 {
	case true:
		fmt.Println("Short")
	case false:
		fmt.Println("Long")
	}
	
	// With no condition
	otherLength := len(name)
	switch {
	case otherLength < 5:
		fmt.Println("Short")
	case otherLength >= 5:
		fmt.Println("Long")
	}
}

```

## For Loop
```go
package main

import "fmt"

func main() {
	counter := 0

	for counter < 10 {
		fmt.Println("Loop1", counter)
		counter++
	}

	// With Statement
	for i := 0; i < 10; i++ {
		fmt.Println("Loop2", i)
	}

	// Normal loop
	names := []string{"Ahmad", "Isyfalana", "Amin"}
	for i := 0; i < len(names); i++ {
		fmt.Println("Loop3", names[i])
	}

	// With range
	for index, name := range names {
		fmt.Println("Loop-Range", "index", index, "=", name)
	}

	// With range - without index
	for _, name := range names {
		fmt.Println("Loop-Range-Without-Index", name)
	}
}

```

## Function
- Function is first class citizen in Go-Lang
- Function is a data-type also, so it can store in a variable
- Closure -> kemampuan sebuah function berinteraksi dengan data-data disekitarnya

```go
package main

import (
	"fmt"
)

type Filter func(string) string
type Blacklist func(string) bool

func main() {
	// Function without parameter and return value
	sayHello()

	// Function with parameter
	sayName("Amin")

	// Function with return value
	fmt.Println(getGreeting("udin"))

	// Function with multiple return value
	firtName, lastName := getFullName()
	fmt.Println(firtName, lastName)

	// Function with multiple return value, skip read some value
	_, lastName2 := getFullName()
	fmt.Println(lastName2)

	// Variadic function
	fmt.Println(sumAll(1, 2, 3))

	// Variadic function with slice as argument
	numbers := []int{1, 2, 3, 4, 5}
	fmt.Println(sumAll(numbers...))

	// Function as a value
	sayGreeting := getGreeting
	fmt.Println(sayGreeting("sayGreeting"))

	// Function as parameter
	fmt.Println(getGreetingWithFiler("babi", nameFilter))
	fmt.Println(getGreetingWithFiler("baba", nameFilter))

	// Function as parameter replaced with alias/ declaratin data-type
	fmt.Println(getGreetingWithFilerArgumentAlias("babi", nameFilter))

	// Anonymous function
	checkUserStatus("Udin", func(name string) bool {
		if name == "Udin" || name == "Anto" {
			return true
		}

		return false
	})
}

func sayHello() {
	fmt.Println("Hello World!")
}

func sayName(name string) {
	fmt.Println("Hello", name, "!")
}

func getGreeting(name string) string {
	return "Hai " + name + "!"
}

func getFullName() (string, string) {
	return "Ahmad", "Amin"
}

func sumAll(numbers ...int) int {
	total := 0
	for _, value := range numbers {
		total += value
	}

	return total
}

func getGreetingWithFiler(name string, filter func(string) string) string {
	return "Hallo " + filter(name)
}

func getGreetingWithFilerArgumentAlias(name string, filter Filter) string {
	return "Hallo " + filter(name)
}

func nameFilter(name string) string {
	if name == "babi" || name == "anjing" {
		return "****"
	}

	return name
}

func checkUserStatus(name string, blacklist Blacklist) {
	if blacklist(name) {
		fmt.Println("You are in blacklist!")
	} else {
		fmt.Println("Hallo", name, "you are still active.")
	}
}

```