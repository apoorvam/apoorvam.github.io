---
layout: post
title:  "Golang: JSON Marshalling empty slices as empty arrays instead of null"
summary: Here is how to get empty slices instead of a null value on marshalling a JSON in Golang.
date:   2017-01-19 07:44:00 +0530
categories: golang json marshal slice empty null
---

Recently I came across this gotcha in Golang while I was writing a plugin for [Gauge](http://getgauge.io) that generates JSON report.

Let me start with an example. Say I want to generate JSON by marshalling a type as follows:

```
type Person struct {
	Friends []string // Field should be exported
}
```
In this `Person` entity, the field `Friends` contains a list of friends represented as a slice of strings. This field could be returned as `null` from another service(Does that mean he has no friends? Ah no idea who this person is!).

I wrote the below code which marshals the input and was surprized to look at the output.

```
var f1 []string
json1, _ := json.Marshal(Person{f1})
fmt.Printf("%s\n", json1)
```
 
Output :
```
{"Friends":null}
```

This marks the field `Friends` as null whereas I was expecting it to have empty slice in JSON. 

The reason for this was the way I had initialized the slice. When I initialize the `f1` as `var f1 []string`, it is a nil pointer and when marshalled, it gives you null instead of [].

```
var x interface{}
x = 10
```

To fix this, I had to initialize the variable as `f2 := make([]string, 0)` and this gives you output as empty slice instead of null.

```
f2 := make([]string, 0)
json2, _ := json.Marshal(Person{f2})
fmt.Printf("%s\n", json2)
```

Output :
```
{"Friends":[]}
```

The same example can be seen [on the Go playground here](https://play.golang.org/p/Q4ibfpFpju).