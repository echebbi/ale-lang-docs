---
title: "Language overview"
weight: 3
---

ALE is an interpreted, object-oriented and statically typed language. It shares a lot of its syntax with the [Acceleo Query Language (AQL)](https://www.eclipse.org/acceleo/documentation/) that it actually uses under the hood.

{{% notice tip %}}
A comprehensive guide of ALE's syntax can be found in the [Reference chapter]({{< ref "reference/syntax.md" >}}).
{{% /notice %}}

## Object-Oriented

#### Classes

In ALE, classes can be defined with the `class` keyword:

```
class Sun {

}
```

A corresponding `EClass` is created at runtime by ALE's interpreter. The `open` keyword must be used to refer to an `EClass` that already exist in the Ecore model:

```
open class ENamedElement {

}
```

A class can be instantiated with the `create()` service:

```
HelloWorld hello := helloworld::HelloWorld.create();
```

#### Methods

Methods are declared with the `def` keyword:

```
open class Sun {
    def void shine() {

    }
}
```

To override an `EOperation` defined in an Ecore model the `override` keyword must be used instead:

```
open class Sun {
    override int radius() {
        result := 696340;
    }
}
```

In ALE there is no `return` keyword. Instead, each method has a special `result` variable that represents its return value. `:=` is the affectation operator whereas `=` is used to check equality.

The `self` keyword is used to reference the current object:

```
open class User {
    override String getFullName() {
        result := self.firstname + ' ' + self.lastname;
    }
}
```

#### Attributes

Attributes can be declared within a class as follows:

```
class User {

    int age;
    String name := 'Unknown';

}
```

The following table shows all the built-in types:

| Type       | Description                              | Instantiation                                         |
| ---------- | ---------------------------------------- | ----------------------------------------------------- |
| Integer    | A number without decimal part            | `int a := 12`                                         |
| Real       | A number with decimal part               | `double r := 23.5`                                    |
| String     | A sequence of characters                 | `String str := 'Hello World!'`                        |
| Boolean    | Either true of false                     | `boolean b := true`                                   |
| Sequence   | An ordered collection of elements        | `Sequence(Integer) numbers = Sequence{1, 2, 3}`       |
| OrderedSet | An ordered collection of unique elements | `OrderedSet(String) users = OrderedSet{'Foo', 'Bar'}` |

## Conclusion

Now that we covered the basics of ALE you're ready to go further with the [MiniFsm tutorial]({{< ref "tutorials/mini-fsm" >}}).

