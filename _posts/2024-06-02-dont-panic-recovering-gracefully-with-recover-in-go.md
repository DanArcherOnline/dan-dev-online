---
date: 2024-05-01 03:35:53
layout: post
title: Don't Panic! Recovering Gracefully with recover in Go
description: What Golang's recover is and how to use it.
image: /assets/img/uploads/panic_gopher.jpeg
category: dev
tags:
  - go
  - golang
author: Dan
paginate: false
---
[t﻿est](http://www.test.com)

Ever been coding along, nice and relaxed, when suddenly your program throws a wobbly and crashes? Maybe a file wouldn't open, or something went funky with an external resource. Well, fear not! Go has a built-in feature called `recover()` that can help you **recover** from those panics.

Now, before you go all superhero on panics, it's important to remember that Go generally prefers handling errors with returned error values. `recover()` is more like having a fireman's net to catch you if you do take a tumble.

Here's the gist of how `recover()` works:

1. **Uh oh, Panic!** - If your program encounters a `panic(value)` statement, things are about to go south. The program throws its hands up and starts shutting down.
2. **Enter Defer** - The `defer` statement lets you schedule some code to run later, even if the surrounding function throws a tantrum. It's like saying, "Hey, gotta do this no matter what!"
3. **`recover()` to the Rescue!** - If you put `recover()` inside a `defer` function, it acts like a catcher's mitt for panics. It grabs the value passed to `panic` (the error message) and gives you a second chance.

**Alright, enough talk, let's see it in action!**

Imagine you're building a super cool server application that reads data from files. Opening a file can sometimes be tricky, and if it goes wrong, you don't want your whole server to crash. Here's how we can use `recover()` to catch those file-related panics:

```go
package main

import (
  "fmt"
  "io/ioutil"
)

// Our own custom error type for data woes
type DataAccessError struct {
  error
}

// OpenFileWithRecover - Plays it cool even if things get panicky
func OpenFileWithRecover(filename string) (*ioutil.File, error) {
  defer func() {
    if err := recover(); err != nil {
      fmt.Printf("Phew, caught some panic while opening that file: %v\n", err)
      return // Let's just bounce out of here
    }
  }()

  // Attempt to open the file, fingers crossed!
  file, err := ioutil.Open(filename)
  if err != nil {
    // Wrap the error in our snazzy DataAccessError
    return nil, DataAccessError{err}
  }
  return file, nil
}

func main() {
  // Open a file (maybe it exists, maybe it doesn't...)
  file, err := OpenFileWithRecover("super_secret_data.txt")
  if err != nil {
    // Check what kind of error we got
    if _, ok := err.(DataAccessError); ok {
      fmt.Println("Looks like we had some trouble accessing data:", err.Error())
    } else {
      fmt.Println("Whoa, something unexpected went wrong:", err.Error())
    }
    return
  }
  // Do awesome things with the file (not shown here for brevity)
  defer file.Close()
  fmt.Println("File opened successfully! ")
}
```

In this example:

* We created a `DataAccessError` to keep data-related errors organized.
* The `OpenFileWithRecover` function uses `defer` and `recover()` to catch panics during file opening.
* The `defer` function ensures the file gets closed even if there's a panic.
* `recover()` logs the panic message for debugging but lets the program flow normally.
* In `main`, we handle the returned error. If it's a `DataAccessError`, we know it's a data issue. Otherwise, it's something else entirely.

**Remember:**

* `recover()` is a safety net, not your first line of defense. Proper error handling with returned values is still your best friend.
* Use `recover()` judiciously and only in specific situations where catching a panic makes sense.

So, the next time your program throws a wobbly, you'll be equipped with `recover()` to catch it and keep things running smoothly.