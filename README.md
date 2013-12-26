Go JavaScript Bindings
======================

Highly experiemental, I'm not even sure these work currently. Original author is Robery Johnstone, and his mercurial repository can be found at https://bitbucket.org/rj/golang-javascriptcore/. I have updated the bindings to work with the latest changes to the reflect API, bits of it manually. The entire test suite minus one function (finally!) passes.

Update (2013/10/16): The test suite does not work at all, but it compiles again with go 1.0. Feel free to hack away at this if you think it might be useful :).

Update (2013/12/26): Thanks to @sqs, the test suite now passes. This library should still be considered "experimental", but should work.

### Install

	go get github.com/crazy2be/gojs

### Use:

	package main

	import (
		"github.com/crazy2be/gojs"
		"fmt"
	)

	func main() {
		ctx := gojs.NewContext()
		defer ctx.Release()

		ret, err := ctx.EvaluateScript("['hello', 'world'].join(' ')", nil, ".", 0)

		if err != nil {
			fmt.Println("Script had an error :(", ctx.ToStringOrDie(err))
			return
		}

		if ret == nil {
			fmt.Println("Nothing returned...")
			return
		}

		retstr := ctx.ToStringOrDie(ret)

		fmt.Println(retstr)
	}

TODOs
-----
(for anyone interested)

1. Get the test suite to pass ;)
2. Move as many functions as possible *off* of context. We should be able to make a nicely broken-down API where the conceptual weight is lower. For example, all of the functions that take `obj *Object` as the first parameter should really just be functions on `*Object` directly.
3. ???
4. PROFIT! (i.e. make something cool).

Documentation
-------------

There's not much documentation, because the original had no documentation. If I find a use for this beyond curiousity, I might add that as I go. Current documentation generated by godoc is available at http://gopkgdoc.appspot.com/pkg/github.com/crazy2be/gojs.
