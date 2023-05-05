---
layout: post
title: "Basic Introduction to Haskell 2. Defining Functions"
date: 2023-05-01
Categories: Haskell Functional-Programming referential-transparency declarative-language imperative-language pure-functional-language
---

![Function Closed Machine](https://bucephal.github.io/learn_Haskell/docs/assets/images/humpty_dumpty.jpg)

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

## Multiple parameters

Strictly speaking, a function has only one parameter. It may be a multi-dimensional parameter (a tuple) but it is only one "thing". But for practical purposes, it is possible to think about it as multiple parameters. In Haskell, parameters are simply separated by white spaces. There is a reason for this and its related to the fact that Haskell really doesn't accept more than one parameter as we will see in the section about "Currying".

```Haskell
f x y = x + y
f 2 3
5
```

The ```f``` can be seen as a function with two parameters ```x``` and ```y```.

## Partial applications and closures

It is possible to partially apply the function.

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

If you want to know when the "λ" is coming from, see the first section of the first post of this serie. Most programming languages have a notion of "anonymous function", i.e. a function without a name. Everywhere we call this a "_lambda function_". Likewise, in Haskell, a lambda function is a function with no name. This is useful because functions in Haskell are _first-class citizens_. A function may return another function as value or accept another function for parameter. To be "pure" we shouldn't say "return" because functions in pure FP don't _do_ things, like returning a value, functions are only _definitions_. There is a notion of "returning" something in Haskell, but it makes sense only in the context of IO (or something with a state). So to be "pure", we'll say that an anonymous function is useful because functions are defined with functions. This will be obvious after we see "higher order functions" and currying.


So here's an example of a lambda function in Haskell. without a name in Haskell is 



## A First Taste of Types

### Basic types

### Lists

### Tuples

### Functions

## Currying

### Function application binds first

### Operators and sections

### Partial application and closures revisited

### Everything is function

If we define litteral as closures on function (see previous section) and if we define multiple parameters in its curried form, then it is awlays the case that a functions accepts one and only parameter which must be a function and its definition necessarily reduces to one and only one thing which is also function. Therefore a function applies a function to produce yet a function. So there is nothing "really" special about higher order functions. 

## Functions' Body in Haskell

aaaa

## Recursivity

aaaa

## Higher Order Functions

aaaa

(Next: Laziness)
(Next: Types)
(Then Context: Maybe and IO)
(Then functors, Applicatives and Monads)
(IO Revisited)
(Then introduction to the problem we will tackle to test parallelism: Neuron nets both training and using)
(Then the par and seq primitives)
