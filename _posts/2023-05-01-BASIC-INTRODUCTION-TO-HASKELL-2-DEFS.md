---
layout: post
title: "2. Haskell Basics"
date: 2023-05-01
Categories: Haskell Functional-Programming referential-transparency declarative-language imperative-language pure-functional-language
---

![Function Closed Machine](https://bucephal.github.io/Haskell-From-Basics-to-Parallelism/docs/assets/images/humpty_dumpty.jpg)

>“The question is,” said Alice, “whether you can make words mean so many different things.”
>
>“The question is,” said Humpty Dumpty, “which is to be master — that’s all.”
>
>_Through the Looking Glass_, Lewis Carroll

# Defining Functions

The identity function may be the simplest one. It taskes an “x” and simply returns that “x”.

```haskell
identity x = x
identity "hello"
"hello"

identity 2
2
```

The name of a function like "identity" must start with a lower case letter. Then comes its parameters' list followed by an "=" and an expression for its value or result. 

## Function parameters

Strictly speaking, a function has only one parameter. It may be a multi-dimensional parameter (a tuple) but it is only one "thing". But for practical purposes, it is possible to think about it as multiple parameters. In Haskell, parameters are simply separated by white spaces. There is a reason for this and its related to the fact that Haskell really doesn't accept more than one parameter as we will see in the section about "Currying".

```Haskell
f x y = x + y
f 2 3
5
```

The ```f``` can be seen as a function with two parameters ```x``` and ```y```.

## Partial applications and closures

It is possible to partially apply a function.

```Haskell
f x y = x + y
g = f 2
g 3
5
```
The parameter ```y``` of the function ```f``` is not free anymore in function ```g```. It has been binded to ```2```, leaving the parameter ```x``` free. That's one way to make new functions out of existing ones. The function ```g``` is called a **_closure_** of ```f```. In some sense, it _captured_ a ```2``` inside. It's simply a function with a parameter forever binded to a fix value. We will give another definition in the section about currying.

We may push a little further and consider litterals (like 2, "hello", 'L', etc.) as closures on the identity function. At the beginning of this post, we defined that function.

We may say that ```2``` _is_ a closure on the function ```identity``` binded to ```2```...

## Lambda Functions

Most programming languages have a notion of "anonymous function", i.e. a function without a name. The concept of an anonymous function comes from FP. Likewise, in Haskell, a lambda function is a function with no name.

Why is it useful? It is useful in a language where functions are to be considered as _first-class citizens_. For example, a function may return another function as value or accept another function for parameter. 

Note that to be "pure" we shouldn't say "return" because functions in pure FP don't _do_ things, like returning a value. Functions are nothing more than _definitions_ in pure FP. If there _is_ a notion of "returning" something in Haskell, it only makes sense in the context of IO (or something with a state). So to be "pure", we'll say that an anonymous function is useful because functions are defined with functions. This will become obvious as we proceed.

So here's an example of a lambda function in Haskell. 

```Haskell
f = \x y -> x + y
f 2 3
5
```

## A First Taste of Types

Types don't absolutely need to be specified in Haskell. For proof, we already defined a few functions without specifying any type. They are _statically_ inferred when not specified according to its usage. This is not to be compared with dynamic typing as is done in _Python_. In Python, the type of a variable, of a tuple, of a list or a function (etc.) is determined at runtime according to its usage. The name of variable for example may change both its value and its type in the same scope. In Haskell, the type of a function is determined statically (at compile-time) and _must_ be coherent through the program specification. Nothing ever change in Haskell once defined. The type system superposes itself over the rest of the language to help in checking its correctness.

The syntax to declare the type of something (anything) in Haskell is always the same: you have to provide its name, followed the symbol ```::```, and its actual type.

```Haskell
n :: Int
n = 3
```

The type of a function is defined with the arrow ```TypeParam -> TypeResult```.

```Haskell
ord :: Int -> Char
ord 1 = 'a'
ord 2 = 'b'
ord _ = '!'

my_letter = ord 2

:t my_letter
Char
```

Applying a one-parameter function or binding its parameter to a value means the same thing. After applying an ```Int``` to a function ```Int -> Char```, the result is very naturally a ```Char```.

Now, let's see a function with two parameters.

For example, the type of a function that  adds two integers will be ```Int -> Int -> Int```. The first time you see this, you deduce that the first two ```Int``` are for the parameters and the the last one is for the result. But it's kind of shocking to see no clear separation between the parameters and the "return" type. But then, considering that there can't be no more and no less but one result, you might think that indeed there is no need for anything more. Mmmmh, but there is more to think about. First let's see the example of ```add```.

```Haskell
add :: Int -> Int -> Int
add n m = n + m
add 2 3
5
```

When we binded the parameter of the ```ord``` function above, the ```Int ->``` disappeared and only ```Char``` remained. Let's now bind the first parameter of ```add```.

```Haskell
add :: Int -> Int -> Int

-- Binding the first parameter of add
-- gives the closure add'
add' = add 2

add' 3
5

:t add'
Int -> Int
```

Likewise, the first ```Int ->``` disappeared and only the right part remains, which is ```Int -> Int```. It's exactly the same operation of binding a parameter in both cases, ```ord``` and ```add```. But here, the remaining ```Int -> Int``` is itself the type of a function! 

Does it mean that ```add``` is a function that takes one parameter of type ```Int``` and "returns" another function of type ```Int -> Int``` that is a closure of itself? That's exactly it. This is what "Currying" is all about as we will see later.

### Basic types

### Polymorphic types

### Parametric types

### Lists

### Tuples

## Currying

### Function application binds first

### Operators and sections

### Partial application and closures revisited

### Everything is function

If we define litteral as closures on function (see previous section) and if we define multiple parameters in its curried form, then it is awlays the case that a functions accepts one and only parameter which must be a function and its definition necessarily reduces to one and only one thing which is also function. Therefore a function applies a function to produce yet a function. So there is nothing "really" special about higher order functions. 

## Functions' Body in Haskell

### Pattern matching
### Guards
### If Then Else Constructs
### Where Clauses

## Recursivity

aaaa

## Type Classes

aaa

## Higher Order Functions

aaaa

(Next: Laziness)
(Next: Introducing your Own Types)
(Then Context: Maybe and IO)
(Then functors, Applicatives and Monads)
(IO Revisited)
(Then introduction to the problem we will tackle to test parallelism: Neuron nets both training and using)
(Then the par and seq primitives)
