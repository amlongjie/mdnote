# Slice

## 定义

``` go
arr := [...]int{0, 1, 2, 3, 4, 5, 6, 7}
s1 := arr[2:6]
s2 := arr[:6] 
s3 := arr[2:] 
s4 := arr[:] 
```

Slice本身没有数据,是对底层数组的一个View(视图)

所以无论在数组里改值还是在切面里修改,都会引起两方的改变.



## ReSlice

基本ReSlice

``` go
arr := [...]int{0, 1, 2, 3, 4, 5, 6, 7}
s1 := arr[:5] //01234
s1 := s1[2:]//234
```

复杂ReSlice

```go
arr := [...]int{0, 1, 2, 3, 4, 5, 6, 7}
s1 := arr[2:6] //2,3,4,5
s1 := s1[3:5] //5,6
```



![image-20180514080931073](/var/folders/zt/jwhtltr93l3chbt3510268nc0000gn/T/abnerworks.Typora/image-20180514080931073.png)



## Slice的实现

![image-20180514081014714](/var/folders/zt/jwhtltr93l3chbt3510268nc0000gn/T/abnerworks.Typora/image-20180514081014714.png)

1. Slice可以向后扩展,但是不可以向前扩展
2. s[i]不可以超越len(s),向后扩展不可以超过cap(s)



获取Slice的相关属性

```Go
arr := [...]int{0, 1, 2, 3, 4, 5, 6, 7}
s1 := arr[:5] //01234
l := len(s1)
c := cap(s1)
```



## 操作Slice

## 创建Slice

```go
var s []int //Zero value for slice is nil
s1 := []int{2,3,4,8}
s2 := make([]int, 16, 16)
```



### 添加

``` go
	arr := [...]int{0, 1, 2, 3, 4, 5, 6, 7}
	s1 := arr[0:7]
	fmt.Println(arr) //0,1,2,3,4,5,6,7
	fmt.Println(s1) // 0,1,2,3,4,5,6

	s1 = append(s1, 8) 
	fmt.Println(arr) //0,1,2,3,4,5,6,8
	fmt.Println(s1) //0,1,2,3,4,5,6,8

	s1 = append(s1, 9)  
	fmt.Println(arr) //0,1,2,3,4,5,6,8
	fmt.Println(s1) //0,1,2,3,4,5,6,8,9 ==> 已经view一个新的arr了
```

1. 添加元素的时候如果超过cap,系统会重新分配更大的底层数组.
2. 由于是值传递,所以append必须用值接收 => s = append(s, val)
3. **cap扩容的时候,每次都扩充为原来的2倍**



## Copy Slice

```Go
arr := [...]int{0, 1, 2, 3, 4, 5, 6}
s1 := arr[0:6]
fmt.Println(s1)
s2 := make([]int, 4, 4)
s2[0] = 10
copy(s2, s1)
fmt.Println(s2)
```

复制的时候会覆盖S2原来的值



## Delete From Slice

``` go
	arr := [...]int{0, 1, 2, 3, 4, 5, 6}
	s1 := arr[0:6]
	fmt.Println(s1)

	s1 = append(s1[:3], s1[4:]...) // 删除下标为3的元素
	fmt.Println(s1)
```

