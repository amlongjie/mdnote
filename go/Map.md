# Map



## Definition

``` go
	m1 := map[string]string{
		"name": "mingming",
		"age":  "24",
	}

	m2 := make(map[string]int, 0) // empty map

	var m3 map[string]int // nil
	
	fmt.Println(m1, m2, m3) // map[name:mingming age:24] map[] map[]
```

虽然m3是nil,但是在go语言中,nil和empty map一样可以使用.不会出现问题



## Traversing Map

``` go
	for k, v := range m1 {
		fmt.Println(k, v)
	}

	for k := range m1 {
		fmt.Println(k)
	}

	for _,v := range m1 {
		fmt.Println(v)
	}
```



## Getting Values

``` go
	name := m1["name"]
	fmt.Println(name) // mingming

	wrongName := m1["name2"]
	fmt.Println(wrongName) // "" get the zero value

	if n, ok := m1["name"]; ok {
		fmt.Println(n)
	} else {
		fmt.Println("key does not exist")
	}
```

如果是没有的Key,会返回ZeroValue.字符串就是"".所以不能直接获取.而是要使用ok来判断是否存在.



## Delete value

``` go
delete(m1, "name")
```



## Annotation

1. slice,map,function不能作为Map的Key
2. 包含上述类型的Struct类型,也不能作为Key



