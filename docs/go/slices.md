## Go slices 

- used to store values of saem data type.
- flixible than arrays. i.e. length of an array can grow or shrink


## declare a slice:
```
slice_name := []datatype{values}
letters := []string{"a", "b", "c", "d"}
numbers := []int{1, 3, 3, 4, 5}
```

## create slice using ```make``` func:

declaring slice using ```make```:
```
slice_name := make([]type, length, capacity)
```
- capacity equal to length if not defined
example:
```
package main

import (
	"fmt"
)

func main() {
	testclice := make([]int, 0)
	fmt.Printf("length = %d\n", len(testclice))
	fmt.Printf("capacity = %d\n", cap(testclice))
	testclice = append(testclice, 1, 2, 3, 4, 5)
	fmt.Println(testclice)
	fmt.Printf("length after append = %d\n", len(testclice))
	fmt.Printf("capacity after append = %d\n", cap(testclice))
	
	fmt.Println("----------------------------")
	
	testclice1 := make([]int, 2, 3)
	fmt.Printf("length = %d\n", len(testclice1))
	fmt.Printf("capacity = %d\n", cap(testclice1))
	testclice1 = append(testclice1, 1, 2, 3 ,4 , 5 )
	fmt.Println(testclice1)
	fmt.Printf("length after append = %d\n", len(testclice1))
	fmt.Printf("capacity after append = %d\n", cap(testclice1))
}
```
output:
```
length = 0
capacity = 0
[1 2 3 4 5]
length after append = 5
capacity after append = 6
----------------------------
length = 2
capacity = 3
[0 0 1 2 3 4 5]
length after append = 7
capacity after append = 8
```




## creating a slice from an array:
```
var myarray = [length]datatype{values} // An array
myslice := myarray[start:end] // A slice made from the array
```
example:
```
package main

import (
	"fmt"
)

func main() {
	
	testarray := [5]int{1, 2, 3, 4, 5}
	testslice := testarray[3:5]
	fmt.Printf("length = %d\n", len(testslice))
	fmt.Printf("capacity = %d\n", cap(testslice))
	fmt.Println(testslice)
	
}
```

output:
```
length = 2
capacity = 2
[4 5]
```



