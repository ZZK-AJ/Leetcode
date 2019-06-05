## 冒泡排序

把一个元素，通过不断地比较，把大的或者小的排到最上面

```go
package main

import "fmt"

func bsort(a []int) {
	// 冒泡排序
	for i := 0; i < len(a); i++ {	// i,j 的循环，i 负责每一次冒泡，排好 i 个元素
		for j := 1; j < len(a)-i; j++ {		// 这里 j < len(a)-i 因为上面的已经排好了
			if a[j] < a[j-1] {		// 假如上面的数小于上面的，就交换位置，把大的放上面
				a[j], a[j-1] = a[j-1], a[j]
			}
		}
	}
}

func main() {
	b := [...]int{8, 7, 5, 4, 3, 10, 15}	// 定义一个数组
	bsort(b[:])
	fmt.Println(b)
}
```



## 选择排序

每一次循环，选择出最小的，然后排好

```go
package main

import "fmt"

func ssort(a []int) {
	// 选择排序
	for i := 0; i < len(a); i++ {
		var min int = i		// 设定一个最小的标记 i，每次循环都赋值为 i 为初始值
		for j := i + 1; j < len(a); j++ {	// 循环 j，进行一次次的迭代比较
			if a[min] > a[j] {		// 每一次比较都是与 min 比较，假如小的话，就赋给 min
				min = j
			}
		}
		a[i], a[min] = a[min], a[i]		// 最后肯定是 min 是最小的，然后赋给这一次迭代的 a[i]
	}
}

func main() {
	b := [...]int{8, 7, 5, 4, 3, 10, 15}
	ssort(b[:])
	fmt.Println(b)
}
```





## 插入排序

把一个迭代出的元素和排好序的序列比较，放到合适的位置(就像打牌一样)

```go
package main

import "fmt"

func ssort(a []int) {
	// 选择排序
	for i := 0; i < len(a); i++ {
		var min int = i		// 设定一个最小的标记 i，每次循环都赋值为 i 为初始值
		for j := i + 1; j < len(a); j++ {	// 循环 j，进行一次次的迭代比较
			if a[min] > a[j] {		// 每一次比较都是与 min 比较，假如小的话，就赋给 min
				min = j
			}
		}
		a[i], a[min] = a[min], a[i]		// 最后肯定是 min 是最小的，然后赋给这一次迭代的 a[i]
	}
}

func main() {
	b := [...]int{8, 7, 5, 4, 3, 10, 15}
	ssort(b[:])
	fmt.Println(b)
}
```



## 快速排序

选取基准元素，把每一个不断和基准比较，分为 left 和 right ，然后对于 left 和 right，继续进行递归调用。最后就能排好。

```go
package main

import "fmt"

func isort(a []int) {
	// 插入排序，和打牌一样，插入到有序的序列里面
	for i := 1; i < len(a); i++ {
		for j := i; j >0; j-- {	//假设第一个是有序的，从i后面开始，要插入到有序的序列[0-i]里面
			if a[j] > a[j-1] {
				break
			}
			a[j], a[j-1] = a[j-1], a[j]
		}
	}
}

func main() {
	b := [...]int{8, 7, 5, 4, 3, 10, 15}
	isort(b[:])
	fmt.Println(b)
}
```











