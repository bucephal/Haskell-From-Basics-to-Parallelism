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
```

The name of a function like "identity" must start with a lower case letter. Then comes its parameters' list followed by an "=" and an expression for its value or result. 

## Multiple parameters

Strictly speaking, a function has only one parameter. It may be multi-dimensional parameter (tuple) but it is only one "thing". In Haskell, parameters are simply separated by white spaces. There is a reason for this as we will see in the section about "Currying".

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
The parameter ```y``` of the function ```f``` is not free anymore in function ```g```. It has been binded to ```2```, leaving the parameter ```x``` free. That's one way to make new functions out of existing ones. The function ```g``` is called a **_closure_** of ```f```. In some sense, it _captured_ a ```2``` inside. It's a function with a parameter forever binded to a fix value. We will give another definition in section about currying.

We may push a little further and consider litterals, for example

## Lambda Functions

aaa

## A First Taste of Types

### Basic types

### Lists

### Tuples

### Functions

## Currying

aaa

## Functions' Body in Haskell

aaaa

(Next: Laziness)
(Next: Types)
(Then Context: Maybe and IO)
(Then functors, Applicatives and Monads)
(IO Revisited)
(Then introduction to the problem we will tackle to test parallelism: Neuron nets both training and using)
(Then the par and seq primitives)
