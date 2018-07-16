# setup and tool chain

## GOPATH

Go resolves import statements using the GOPATH. If the var is not set, it attempts to resolve import statements from `$HOME/go`. 

`go env GOPATH` prints out the current GOPATH.

The `src`, `pkg`

## dep

The "official experiment" for dependency management in Go.

See [`package`](#Packages)

# Primitives, Concepts and Interesting Properties

## Blank Identifier

In Golang the underscore `_` character is a reserved identifier called the Blank Identifier. From the spec:

> The blank identifier may be used like any other identifier in a declaration, but it does not introduce a binding and thus is not declared. 

In practice, use of the blank identifier prevents declaring (binding, and thus adding to memory/GC overhead) variables that will not be used, but which must be included in a statement for syntax or readability.

```
// In this example we are printing all the environment variables available to the go process.
// The Blank Identifier is accepting (and discarding) the index of each item in the slice in the range.
// If we needed the index, we could substitute another identifier, provided the variable was used.

for _, e := range os.Environ() {
    pair := strings.Split(e, "=")
    fmt.Println(pair[0])
}
```

## Channels

Channels are typed "pipes" to pass data from one Go routine to another. Strictly speaking, this can occur in the absence of invoking the `go` command, though in practice go routines are the most common use pattern.



## Interfaces

An interface is a type that represents a  Method Set. Any type that has all the methods in the set is said to _implement_ the interface.

Interfaces are thus a way of constructing an abstraction out of what it does (methods) rather than what it has (data). One way to say this is that interfaces are abstractions of behavior.

Note that there is no `implements` keyword. The interface is simply the behaviors common to some set of structs. Rather than thinking about cars, motorcycles, and buses as objects that have wheels and seats, we instead are thinking about structs that accererate, brake, and load and unload some number (n) passengers.


Interfaces can be used as fields in structs.

## Goroutines

The syntax:

```
go functionOrMethod() 
```

Starts a concurrent thread in the same address space. When the function terminates, so does the goroutine, and the return values are discarded. 

Use [`channels`](#Channels) as pipes to connect goroutines.

## Main

Go expects that there will be one `main.go` file at the base of the file tree that establishes an executable.

This filetree may have many packages below its root that are imported into main or into other files as needed, and which may also be imported as a [`package`](#Package) from other programs.

In the main file, the package name *is* main, it contains only one file, and cannot be imported.

## Make

## Packages

The first statement in a Go source file must be:

```
package <name>
```

All files in a package must have the same package name. 

The package name must be the last element in the full import path.

For example, if we have:

```
github.com/user/utils
    foo/
        foo_a.go
        foo_b.go
        qux/
            qux.go
    bar/
        bar.go
```

Then `foo_a.go` and `foo_b.go` must both be of `package foo` and can be imported using:

```
import  "github.com/user/utils/foo"

```

Imagine that `foo_a.go` includes:

```
import  "github.com/user/utils/foo/qux"

```

This would then give us the option in another program to get at the "qux" package in two ways:

```
import  "github.com/user/utils/foo"
import  "gitbub.com/user/utils/foo/qux"

func main() {
        foo.Qux()   //  we have access to Qux *through* foo
        qux.Qux()   //  we can access Qux directly
}

```

# Pass by Value

Calling a function 


See [`main`](#Main)

## Structs

Typed collections of fields that group data into records.

Record data is mutable.

## Variadic Functions

A variadic function has the ability to accept any number of arguments (of the same type). It is also possible to pass a slice of arguments:

```
func sum(nums ...int) {
    total := 0
    for _, num := range nums {
        total += num
    }
    fmt.Println(total)
}

func main() {
    sum(1, 2)
    nums := []int{1, 2, 3, 4}
    sum(nums...)
}

```

# Standard Library (and drop in replacements of interest)

## flag 

Command-line flag parsing.

## pflag

Drop in replacement for flag that adds POSIX standards.

# The 'Expanded' Library

Widely adopted packages.

## Cobra

