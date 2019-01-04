---
layout: post
title: "GoTerminal: Go library to render progress on terminal"
permalink: go-terminal
date: 2018-01-04 14:26:02
comments: false
description: "GoTerminal: Go library to render progress on terminal"
keywords: "terminal, console, golang, progress, progressbar, rewrite, update text"
categories: go-library

tags: go-library, progressbar

---

[GoTerminal](https://github.com/apoorvam/goterminal) is an open source Golang package for updating progress in the console. It is a simple cross-platform package and can be used to render progress in command line applications. For example, to show download progress, show the progress bar for test execution etc. 

This can be visually rich and gives the user real-time feedback on background operations, without clumsy data. You can update text at any particular coordinate on screen easily using a `Writer` instance. This can also be integrated with [Go-Colortext](https://github.com/daviddengcn/go-colortext) package to add colours to console text.

## Installation

{% highlight go %}
  go get -u github.com/apoorvam/goterminal
{% endhighlight %}

## Usage

{% highlight go %}
    func main() {
    	// get an instance of writer
    	writer := goterminal.New()

    	for i := 0; i < 100; i = i + 10 {
    		// add your text to writer's buffer
    		fmt.Fprintf(writer, "Downloading (%d/100) bytes...\n", i)
    		// write to terminal
    		writer.Print()
    		time.Sleep(time.Millisecond * 200)

    		// clear the text written by the previous write, so that it can be re-written.
    		writer.Clear()
    	}

    	// reset the writer
    	writer.Reset()
    	fmt.Println("Download finished!")
    }
{% endhighlight %}

## Example 

![Download Progress](https://raw.githubusercontent.com/apoorvam/goterminal/master/doc/download_progress.gif)

Another example which uses the [go-colortext](github.com/daviddengcn/go-colortext) library to re-write text along with using colours. Here is an output of example:

![Colored terminal, updating text](https://raw.githubusercontent.com/apoorvam/goterminal/master/doc/color_terminal.gif)

Examples can be found [here](https://github.com/apoorvam/goterminal/tree/master/examples).

### More on usage

* Create a `Writer` instance.
* Add your text to writer's buffer and call `Print()` to print text on Terminal. This can be called any number of times.
* Call `Clear()` to move the cursor to the position where first `Print()` started so that it can be over-written.
* `Reset()` writer, so it clears its state for next Write.


Like it? [Let me know](https://twitter.com/ItsApoorvaHere).

Questions or issues using GoTerminal? Post an issue on [Github](https://github.com/apoorvam/goterminal/issues).

