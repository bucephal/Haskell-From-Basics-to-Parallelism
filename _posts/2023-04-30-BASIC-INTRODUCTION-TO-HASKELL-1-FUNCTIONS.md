---
layout: post
title: "Basic Introduction to Haskell 1. Functions"
date: 2023-04-30
Categories: Haskell Functional-Programming referential-transparency declarative-language imperative-language pure-functional-language
---
![Function Closed Machine](https://bucephal.github.io/learn_Haskell/docs/assets/images/Function_machine2.svg)

# Well... Functions!

A function is a kind of machine that takes one or more parameters and produces a result, one result, only one result, and always one result. As you can see in the image above, a function is represented as a box with only one entry. This means that a function can't be influenced by anything other than the designed entry door. There can be more than one entry, but no backdoor. Therefore, for a given parameter, the function must always produce the _same_ result, since there can't be any source of effect other than its declared parameters. This important property is named **_referential transparency_**. A function is pure internal logic. A closed box. What it means to be pure logic may be nothing more than a fantasy of early 20<sup>th</sup> century mathematicians. But that is a question for the philosophers to answer. As far as we are concerned, it simply means that if you give the machine the same input, it will produce the same output. Every time.

Also, as in mathematics, a function produces only one result (in its _image_ set), no more and no less, for each of its different possible parameters (its _domain_ set). It's the only way to make a function completely deterministic. If the image set is infinite, then the function can _not_ be proved to be deterministic by extension (i.e. by showing all possible input-output pairs). It will be deterministic only in terms of its internal logic. This allows us to predict a result even on parameters we have never seen before. If you think about it, it doesn't make much sense for a function to produce more than one thing. If it is to be deterministic, it must always produce the same thing and from this point of view, the thing produced is _one_ thing. It may be a tuple, but it is to be considered as _one_ result, i.e. what is produced the machine.

A function can only be defined. It is not a process. It's only a logic. And as in mathematics, there may be logical derivations but the derivations ate only to be justified by definitions. It is the main difference between a **_declarative language_** like _Haskell_ and an **_imperative_** one like _C_. In haskell you don't tell the machine "do this", "then do that". You simply declare the meaning of functions, i.e. what they should produce with their given parameters.
Here's an example of a function definition in Haskell.

```haskell
f x = x * x
f 4
16
```

Functions in Haskell can only be defined and nothing else can be said about them. You simply define it, i.e. give it a meaning, nothing more. What steps the computer actually takes to calculate the result according to its parameters is not our concern. We only care about what it means to be the function (say) _f_, and this meaning is nothing but what should be the output for all its possible inputs.

If this property of referential transparency is respected all the way throughout the language then the language is said to be **_pure_**. You might wonder what the point of having a genuine pure language is, since it rules out any form of I/O. As a matter of fact I/O can't guarantee the same result all the time. So it would seem that a pure FP (Functional Programming) language is useless. No matter how smart it may be inside, if you can't communicate with it... no one really knows!

Have no fear, this problem has been taken care of. But we won't be able to explain it all we see those (in)famous **_monads_** (Nevertheless, we will be using I/O constructs throughout, but the actual explanations will come at a later stage.)

According to Simon Peyton-Jones, the main person behind Haskell, the language is actually useless. The more pure it is, the less useful it will be. The first versions of Haskell had no form of I/O, but after a while it became embarrassing... 

# The Order of Evaluation is Irrelevant

A function in Haskell is defined in such a way that their order of evaluation is immaterial. That means that no matter in what order the expressions are evaluated, the result will be the same.
This property of functions in Haskell comes from their purity. Most imperative languages can't insure this. For example, in _C_:

```C
int n = 1;
n = n * ++n;
// Here n is 2
```

```C
int n = 1;
n = ++n * n
// Here n is 4
```

Although the multiplication is commutative both in the _C_ language and in mathematics, and although we have the exact same operands (```++n``` and ```n```), still we don't have the same results.
This is due to side-effects. In _C_, ```n``` is not only a name, it's a variable, i.e. an area into the actual computer memory (let's say a "bucket"). 

In the first case, these steps are undertaken:
1. Evaluate ```n``` : Go take what's in the ```n``` bucket (i.e. 1 to begin with);
2. Evaluate ```++n``` : This does three things:
    2.1. Go take what's in the ```n``` bucket (i.e. 1 again);
    2.2. Increment that value so that it becomes 2.
    2.1. Put the new value (2) into the same bucket.
3. Evaluate 1 * 2: which results is 2.
4. Put back the new value 2 into the bucket.

In the second case, these steps are undertaken:
1. Evaluate ```++n``` : This does three things:
    1.1. Go take what's in the ```n``` bucket (i.e. 1 to begin with);
    1.2. Increment that value so that it becomes 2.
    1.3. Put the new value (2) into the same bucket.
2. Evaluate ```n``` : Go take what's in the ```n``` bucket (i.e. 2);
3. Evaluate 2 * 2: which result is 4.
4. Put back the new value 4 into the bucket.

The origin of sin is referencing something that changes. In Haskell, nothing change and therefore expression may be evaluated in any order.
This small _C_ example code can't be replicated in Haskell. We would rather get something like this.

```Haskell
n = 1
(n+1) * n
-- Here n is still 1. It can't change.
-- And the result of the above expression is 2.
```

```Haskell
n = 1
n * (n+1)
-- Here n is still 1. It can't change.
-- And the result of the above expression is 2.
```

In Haskell, ```n``` doesn't name something in the outside world (outside the language). It only bears the meaning of its _definition_ (```n = 1```) and nothing else.


