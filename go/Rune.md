# String & Rune



## 定义

rune相当于go的char



##String的遍历 

### 普通遍历

``` go
	s := "我是中国人!!"

	for i, ch := range s {
		fmt.Printf("%d, %c\n", i, ch)
	}
```

遍历后会输出

```
0, 我
3, 是
6, 中
9, 国
12, 人
15, !
16, !
```

Go语言中的字符串使用Utf8编码.每个非英文占3字节.直接使用range遍历返回的是utf8编码的数字.所以下标就是我们看到的样子



### 字节数组遍历

```go
sb := []byte(s)

for len(sb) > 0 {
   r, size := utf8.DecodeRune(sb)
   fmt.Printf("%c ", r)
   sb = sb[size:]
}
```

输出结果

``` go
我 是 中 国 人 ! ! 
```



## Rune数组遍历

``` go
	for i, ch := range []rune(s) {
		fmt.Printf("%d, %c \n", i, ch)
	}
```

输出结果

```
0, 我 
1, 是 
2, 中 
3, 国 
4, 人 
5, ! 
6, ! 
```

但是需要考虑.rune 是 int32的别名.所以在转成rune数组的时候,实际上是重新编码的过程.