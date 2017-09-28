# Syntax for unified field and constructor declaration

* Proposal: [HXP-NNNN](NNNN-ctor-fields.md)
* Author: [Dan Korostelev](https://github.com/nadako)

## Introduction

Allow declaring class instance fields along with their assignments in the constructor in a single place without writing boilerplate code.

```haxe
class User {
  function new(final name:String, var age:Int) {}
}

// as a shortcut to

class User {
  final name:String;
  var age:Int;
  function new(name:String, age:Int) {
    this.name = name;
    this.age = age;
  }
}
```

## Motivation

It's a very common practice to pass arguments to the class constructor and then assign them to fields like in the example above. There are at least two large use-cases where this pattern is used a lot: data objects and OOP dependency injection.

To have this in current Haxe, a programmer has to do three things for each field: declare class field, declare constructor argument, assign field from constructor argument. This is boilerplate code that leaves space for mistakes, and since the amount of this boilerplate scales with the number of classes and fields in the code base, I think, this is something Haxe could make easier and safer by providing a way to achieve this with only one declaration in code.

## Detailed design

Similar feature is implemented differently in other languages, for example Kotlin and Scala merge constructor signature into the class definition, like this:

```scala
class User(name:String, var age:Int) {}
```

This is a nice syntax to declare the "primary constructor" together with fields, because it keeps field declarations near the class name. It looks better, because it suggests that fields are property of a class, not its constructor.

> Describe the proposed design in details the way language user can understand and compiler developer can implement. Show corner cases, provide usage examples, describe how this solution is better than current workarounds.

## Impact on existing code

What impact this change will have on existing code? Will it break compilation?
Will it compile, but break in run-time? How easy it is to migrate existing Haxe code?

## Drawbacks

Describe the drawbacks of the proposed design worth consideration. This doesn't include
breaking changes, since that's described in the previous section.

## Alternatives

What alternatives have you considered to address the same problem, why the proposed solution is better?

## Opening possibilities

Does this change make other future changes possible or easier? Leave this section out if the proposed change
is completely self-contained.

## Unresolved questions

Which parts of the design in question is still to be determined?
