## Go slices 

- used to store values of same data type.
- flixible than arrays. i.e. length of an array can grow or shrink


## declare a slice:
```
slice_name := []datatype{values}
slice_name := []datatype{}  // here length is 0 and capacity is 0 and empty
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
usage:
```
var testarray = [length]datatype{values} 
myslice := testarray[start:end]
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

    fmt.Println("----------------------------")

    y_array := [6]byte{'G', 'o', 'l', 'a', 'n', 'g'}
	fmt.Println(y_array)
	y_slice := y_array[3:5]
	fmt.Println(y_slice)
	
}
```

output:
```
length = 2
capacity = 2
[4 5]
------------------
[71 111 108 97 110 103]
[97 110]
```

## appending to slice
usahe:
```
c := append(slice1, slice2...)        # merging 2 slices
c := append(slice1, "item1", "item2" )  # adding items to slice
```

example:
```
package main

import (
	"fmt"
)

func main() {

	a := []string{"John", "Paul"}
	b := []string{"George", "Ringo", "Pete"}
	a = append(a, b...) // equivalent to "append(a, b[0], b[1], b[2])"
	fmt.Println(a)
	a = append(a, "something")
	fmt.Println(a)
}
```

output:
```
[John Paul George Ringo Pete]
[John Paul George Ringo Pete something]
```

# get and change a element from slice
usage:
```
slice[index] = "new_value"
```
example:
```
package main

import (
	"fmt"
)

func main() {

	b := []string{"George", "Ringo", "Pete"}
	fmt.Println(b)
	b[0] = "Tom"
	fmt.Println(b)

}
```

output:
```
[George Ringo Pete]
[Tom Ringo Pete]
```

## ```copy``` function
usage:
```
copy(dest, src)
```

as per  https://go.dev/blog/slices-intro
- re-slicing a slice doesn’t make a copy of the underlying array. The full array will be kept in memory until it is no longer referenced. Occasionally this can cause the program to hold all the data in memory when only a small piece of it is needed.
effective:
```
var digitRegexp = regexp.MustCompile("[0-9]+")

func FindDigits(filename string) []byte {
    b, _ := ioutil.ReadFile(filename)
    return digitRegexp.Find(b)
}
```

effective:
```
func CopyDigits(filename string) []byte {
    b, _ := ioutil.ReadFile(filename)
    b = digitRegexp.Find(b)
    c := make([]byte, len(b))
    copy(c, b)
    return c
}
```

example:
```
package main
import ("fmt")

func main() {
  main_slice := []int{1,2,3,4,5,6,7,8,9,10}
  fmt.Printf("main_slice = %v\n", main_slice)
  fmt.Printf("main_slice length= %v\n", len(main_slice))
  fmt.Printf("main_slice capacity = %v\n", cap(main_slice))

  
  sub_slice := main_slice[:len(main_slice)-5]
  fmt.Printf("sub_slice = %v\n",sub_slice)
  fmt.Printf("sub_slice length = %d\n", len(sub_slice))
  fmt.Printf("sub_slice capacity = %d\n", cap(sub_slice))
  
  // copy
  new_slice := make([]int, len(sub_slice))
  copy(new_slice, sub_slice)

  fmt.Printf("new_slice = %v\n",new_slice)
  fmt.Printf("new_slice length = %d\n", len(new_slice))
  fmt.Printf("new_slice capacity = %d\n", cap(new_slice))
}
```

output:
```
main_slice = [1 2 3 4 5 6 7 8 9 10]
main_slice length= 10
main_slice capacity = 10
sub_slice = [1 2 3 4 5]
sub_slice length = 5
sub_slice capacity = 10
new_slice = [1 2 3 4 5]
new_slice length = 5
new_slice capacity = 5
```

## loop through
example:
```
package main
import ("fmt")

func main() {

  arr6 := []string{"tom", "dom"}
  
  for i, s := range arr6 {
    fmt.Println(i, s)
  }
  
  for _, s := range arr6 {
    fmt.Println(s)
  }
  
   
}
```

output:
```
0 tom
1 dom
tom
dom
```