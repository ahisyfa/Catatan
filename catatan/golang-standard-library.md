# Golang Standard Library

[Golang Standadr Library](https://pkg.go.dev/std)

## fmt
[fmt Documentation](https://pkg.go.dev/fmt)
```go
package main

import "fmt"

type Person struct {
	Name string
	Age  int
}

func main() {
	amin := Person{Name: "Amin", Age: 30}
	fmt.Printf("Person: %+v\n", amin)
	fmt.Printf("Person: %v\n", amin)

	fmt.Println("Hello, World!")
}
```

## error
[errors Documentation](https://pkg.go.dev/errors)

```go
package main

import (
	"errors"
)

var (
	ErrNotFoundError = errors.New("not found error")
	ValidationError  = errors.New("validation error")
)

func GetById(id string) (string, error) {
	if id == "" {
		return "", ValidationError
	} else if id != "123" {
		return "", ErrNotFoundError
	}

	return "Record 123", nil
}

func main() {
	_, err := GetById("123")

	if errors.Is(err, ValidationError) {
		println("Validation error occurred")
	} else if errors.Is(err, ErrNotFoundError) {
		println("Not found error occurred")
	} else if err != nil {
		println("Some other error occurred:", err.Error())
	} else {
		println("Record found successfully")
	}
}

```

## OS
[os Documentation](https://pkg.go.dev/os)

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	// Get command-line arguments
	args := os.Args
	for i, arg := range args {
		fmt.Printf("arg[%d]: %s\n", i, arg)
	}

	// Get Hostname
	hostname, err := os.Hostname()
	if err != nil {
		fmt.Println("Error getting hostname:", err)
	} else {
		fmt.Println("Hostname:", hostname)
	}
}

```

## flag
[flag Documentation](https://pkg.go.dev/flag)

```go
package main

import (
	"flag"
)

func main() {
	// Get command-line flags username
	username := flag.String("username", "guest", "Username for login")
	password := flag.String("password", "", "Password for login")
	hostname := flag.String("hostname", "localhost", "Hostname of the server")

	flag.Parse()

	println("Username:", *username)
	println("Password:", *password)
	println("Hostname:", *hostname)

}

/**
go run hello-flag.go -username Amin -password root1234 -hostname localhost

Output:
Username: Amin
Password: root1234
Hostname: localhost
*/
```

## strings
[strings Documentation](https://pkg.go.dev/strings)

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	fmt.Println(strings.Trim("  Hello, World!  ", " "))
	fmt.Println(strings.ToUpper("Hello, World!"))
	fmt.Println(strings.Contains("Hello, World!", "World"))
	fmt.Println(strings.Split("Hello, World!", " "))
	fmt.Println(strings.ReplaceAll("Hello, World!", "World", "Go"))
	fmt.Println(strings.HasPrefix("Hello, World!", "Hello"))
	fmt.Println(strings.HasSuffix("Hello, World!", "World!"))
	fmt.Println(strings.Index("Hello, World!", "World"))
	fmt.Println(strings.Repeat("Go! ", 3))
}

/**
Output:
Hello, World!
HELLO, WORLD!
true
[Hello, World!]
Hello, Go!
true
true
7
Go! Go! Go!
*/
```

## strconv
[strconv Documentation](https://pkg.go.dev/strconv)

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	boolean, err := strconv.ParseBool("true")
	if err != nil {
		fmt.Println("Error:", err.Error())
	} else {
		fmt.Println("Boolean:", boolean)
	}

	integer, err := strconv.Atoi("123")
	if err != nil {
		fmt.Println("Error:", err)
	} else {
		fmt.Println("Integer:", integer)
	}

	float, err := strconv.ParseFloat("3.14", 64)
	if err != nil {
		fmt.Println("Error:", err)
	} else {
		fmt.Println("Float:", float)
	}
}

/**
Output:
Boolean: true
Integer: 123
Float: 3.14
*/
```

## math
[math Documentation](https://pkg.go.dev/math)

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	fmt.Println(math.Ceil(3.14))
	fmt.Println(math.Floor(3.14))
	fmt.Println(math.Sqrt(16))
	fmt.Println(math.Pow(2, 3))
	fmt.Println(math.Max(10, 20))
	fmt.Println(math.Min(10, 20))
	fmt.Println(math.Abs(-5))
	fmt.Println(math.Round(3.56))
	fmt.Println(math.Log(2.718281828459045)) // Natural logarithm (base e)
	fmt.Println(math.Log10(100))             // Base-10 logarithm
	fmt.Println(math.Sin(math.Pi / 2))       // Sine of 90 degrees
	fmt.Println(math.Cos(0))                 // Cosine of 0 degrees
	fmt.Println(math.Tan(math.Pi / 4))       // Tangent of 45 degrees

}

/**
Output:
4
3
4
8
20
10
5
4
1
2
1
1
1
*/
```

## container/list
Double linkedlist in Golang

[container/list Documentation](https://pkg.go.dev/container/list)

```go
package main

import (
	"container/list"
	"fmt"
)

func main() {
	linkedListData := list.New()
	linkedListData.PushBack("Amin")
	linkedListData.PushBack(30)
	linkedListData.PushBack(3.14)
	linkedListData.PushBack(true)

	var head *list.Element = linkedListData.Front()
	fmt.Printf("head: %v\n", head.Value)

	var tail *list.Element = linkedListData.Back()
	fmt.Printf("tail: %v\n", tail.Value)

	fmt.Print("All elements in the linked list: ")

	for element := linkedListData.Front(); element != nil; element = element.Next() {
		fmt.Print(element.Value, " ")
	}

	fmt.Println()
}

/**
Output:
head: Amin
tail: true
All elements in the linked list: Amin 30 3.14 true 
*/

```

## container/ring
Circular List in Golang

[container/ring Documentation](https://pkg.go.dev/container/ring)
```go
package main

import (
	"container/ring"
	"fmt"
	"strconv"
)

func main() {
	circularList := ring.New(5) // Create a circular list with 5 elements

	for i := 0; i < circularList.Len(); i++ {
		circularList.Value = "Value " + strconv.FormatInt(int64(i+1), 10)

		circularList = circularList.Next()
	}

	fmt.Print("All elements in the circular list: ")
	circularList.Do(func(value interface{}) {
		fmt.Print(value, ", ")
	})

	fmt.Println()
}

/**
Output:
All elements in the circular list: Value 1, Value 2, Value 3, Value 4, Value 5,
*/

```

## sort
[sort Documentation](https://pkg.go.dev/sort)

```go
package main

import (
	"fmt"
	"sort"
)

type Person struct {
	Name string
	Age  int
}

type PersonSlice []Person

func (p PersonSlice) Len() int {
	return len(p)
}

func (p PersonSlice) Less(i, j int) bool {
	return p[i].Age < p[j].Age
}

func (p PersonSlice) Swap(i, j int) {
	p[i], p[j] = p[j], p[i]
}

func main() {
	persons := PersonSlice{
		{Name: "Alice", Age: 30},
		{Name: "Bob", Age: 25},
		{Name: "Charlie", Age: 35},
	}

	fmt.Println("Before sorting:")
	for _, person := range persons {
		fmt.Printf("%s: %d\n", person.Name, person.Age)
	}

	// Sort persons by age
	sort.Sort(persons) // Uncomment this line after importing "sort"

	fmt.Println("After sorting by age:")
	for _, person := range persons {
		fmt.Printf("%s: %d\n", person.Name, person.Age)
	}
}

```

## time
[time Documentation](https://pkg.go.dev/time)
```go
package main

import (
	"fmt"
	"time"
)

func main() {
	// Get current time
	now := time.Now()
	fmt.Println("Current Time:", now)
	fmt.Println("Current Time in Local:", now.Local())

	var utcTime time.Time = time.Date(2023, time.September, 5, 14, 30, 0, 0, time.UTC)
	fmt.Println("UTC Time:", utcTime)
	fmt.Println("UTC Time in Local:", utcTime.Local())

	// Format time
	formattedTime := now.Format("2006-01-02 15:04:05")
	fmt.Println("Formatted Time:", formattedTime)

	// Duration
	var duration1 time.Duration = 10 * time.Millisecond
	var duration2 time.Duration = 5 * time.Second
	totalDuration := duration1 + duration2

	fmt.Println("Total Duration:", totalDuration)
	fmt.Printf("Total Duration: %d\n", totalDuration)
}

/**
Output:
Current Time: 2025-09-09 22:18:23.445324261 +0700 WIB m=+0.000014471
Current Time in Local: 2025-09-09 22:18:23.445324261 +0700 WIB
UTC Time: 2023-09-05 14:30:00 +0000 UTC
UTC Time in Local: 2023-09-05 21:30:00 +0700 WIB
Formatted Time: 2025-09-09 22:18:23
Total Duration: 5.01s
Total Duration: 5010000000
*/

```





## packageName
[packageName Documentation](https://pkg.go.dev/packageName)
```go

```