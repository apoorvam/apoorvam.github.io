---
layout: post
title:  "Golang: Setting up Go Dev Environment"
summary: Want to setup golang in your box? What is GOPATH? This post explains how to setup Golang development environment in detail...
date:   2015-07-26 15:04:49 +0530
categories: golang setup
---
![Gopher](https://blog.golang.org/gopher/header.jpg "gopher")

This is a gopher!! Isn't it a rodent? Well, in this context it is also a mascot for Go project. Read [More](https://blog.golang.org/gopher).

Setting Golang Dev Environment

Before starting to write any code or projects in golang, an important aspect is to set up the Golang Dev Environment in your box. I started using golang for the project [Gauge](http://getgauge.io) before which I had to set my dev environment.

For beginners, a Tour of golang and Go Playground are good platforms to learn the concepts and practice them without installing Go on your machine.

Installing and Setting Go environment
The Go binaries can be downloaded from Golang [Downloads page](https://golang.org/dl/) by choosing suitable OS and architecture. A key aspect in setting up Golang environment is to set the GOPATH environment variable. In my view, this is a way to set the workspace for all your projects. This workspace will have all the projects, its dependencies, packages etc.

GOROOT is the location of Go installation. This should be added to PATH variable which looks like:

```sh
export GOROOT= /usr/local/Cellar/go/1.4.2/libexec
export PATH=$PATH:$GOROOT

export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH
```

In my case, $HOME/go is the directory set as GOPATH. According to standard Golang conventions, it should contain 3 directories as:

```sh
go
  -bin
  -pkg
  -src
```

Within the workspace, the `src` directory holds all the source code, pkg holds the compiled bits, and bin directory holds all the executables. As bin holds all the executables, this should be added to PATH as well.

```
export PATH=$PATH:$GOPATH/bin
```

Testing your Installation
A simple go program can be built and tested to check the correctness of our installation.

A file named `test.go` can be created with program written as:

```go
package main

import "fmt"

func main(){
	fmt.Printf("Testing go installation. It works!!\n")
}
```

To run this:

```sh
$ go run test.go
Testing go installation. It works!!
```

If the message is printed as shown, then the Go installation is working properly.

Hopefully, this was helpful! :)
