+++
title = "Syntax"
weight = 2
+++

## Reserved keywords

The following table lists ALE's reserved keywords. They cannot be use to name attributes, classes or operations.

| Keyword                                         | Purpose                                                   |
| ----------------------------------------------- | --------------------------------------------------------- |
| behavior                                        | Defines the semantics' namespace                          |
| [class](#creating-a-new-class)                  | Declares a new class                                      |
| [def](#defining-operations)                     | Defines an operation                                      |
| [else](#condition-statement)                    | Declares a condition statement                            |
| [extends](#inheriting-open-classes)             | Declares a class' super class                             |
| false                                           | Represents a false expression                             |
| [for](#iteration-statement)                     | Iterates on a collection of items                         |
| [if](#condition-statement)                      | Declares a conditional statement                          |
| null                                            | Represents non-existing value                             |
| [open](#open-classes)                           | Enhances an existing class with new features              |
| [opposite](#declaring-bidirectional-references) | Indicates that a reference is bidirectional               |
| [override](#implementing-an-eoperation)         | Specifies the semantics of an existing operation          |
| self                                            | Represents the current instance                           |
| [switch](#switch-expressions) | Declares a switch expression
| true                                            | Represents a true expression                              |
| [unique](#declaring-a-set)                      | Indicates that a collection should not contain duplicates |
| [use](#calling-java-code)                       | Imports a Java service                                    |

{{% notice info %}} 
The word `result` is also reserved inside an operation. See [defining operations](#defining-operations) for further details.
{{% /notice %}}

## Built-in types

| Type       | Description                              | Instantiation                                         |
| ---------- | ---------------------------------------- | ----------------------------------------------------- |
| Integer    | A number without decimal part            | `int a := 12`                                         |
| Real       | A number with decimal part               | `double r := 23.5`                                    |
| String     | A sequence of characters                 | `String str := 'Hello World!'`                        |
| Boolean    | Either true of false                     | `boolean b := true`                                   |
| Sequence   | An ordered collection of elements        | `Sequence(Integer) numbers = Sequence{1, 2, 3}`       |
| OrderedSet | An ordered collection of unique elements | `OrderedSet(String) users = OrderedSet{'Foo', 'Bar'}` |

{{% notice tip %}}
Looking for types' default value? See [variable declaration](#variable-declaration).
{{% /notice %}}

## Operators

Operators on primitive types:

| Priority | Operator | Operand Types                       | Syntax                  | Semantic                                                  |
| :------: | :------: | ----------------------------------- | :---------------------: | --------------------------------------------------------- |
| 1        | +        | Numeric                             | `<op1>` + `<op2>`       | Add two numeric values                                    |
| 1        | -        | Numeric                             | `<op1>` - `<op2>`       | Substract two numeric values                              |
| 2        | *        | Numeric                             | `<op1>` * `<op2>`       | Multiply two numeric values                               |
| 2        | /        | Numeric                             | `<op1>` / `<op2>`       | Divide `<op1>` by `<op2>`                                 |
| 5        | +=       | Numeric (`<op1>` must be a l-value) | `<op1>` += `<op2>`      | Set `<op1>` to `<op1>` + `<op2>`                          |
| 5        | -=       | Numeric (`<op1>` must be a l-value) | `<op1>` -= `<op2>`      | Set `<op1>` to `<op1>` - `<op2>`                          |
| 5        | *=       | Numeric (`<op1>` must be a l-value) | `<op1>` *= `<op2>`      | Set `<op1>` to `<op1>` * `<op2>`                          |
| 5        | /=       | Numeric (`<op1>` must be a l-value) | `<op1>` /= `<op2>`      | Set `<op1>` to `<op1>` / `<op2>`                          |
| 3        | <        | Numeric                             | `<op1>` < `<op2>`       | True if `<op1>` is lower than `<op2>`                     |
| 3        | >        | Numeric                             | `<op1>` > `<op2>`       | True if `<op1>` is greater than `<op2>`                   |
| 3        | <=       | Numeric                             | `<op1>` <= `<op2>`      | True if `<op1>` is strictly lower than `<op2>`            |
| 3        | >=       | Numeric                             | `<op1>` >= `<op2>`      | True if `<op1>` is strictly greater than `<op2>`          |
| 1        | +        | String                              | `<op1>` + `<op2>`       | Concatenate two strings                                   |
| 2        | +=       | String (`<op1>` must be a l-value)  | `<op1>` += `<op2>`      | Set `<op1>` to `<op1>` + `<op2>`                          |
| 4        | not      | Boolean                             | not `<op>`              | True if `<op>` is false. False if `<op>` operand is true  |
| 4        | and      | Boolean                             | `<op1>` and `<op2>`     | True if both operands are evaluated to true               |
| 4        | or       | Boolean                             | `<op1>` or `<op2>`      | True if at least one of its operands is evaluated to true |
| 4        | xor      | Boolean                             | `<op1>` xor `<op2>`     | True if either `<op1>` or `<op2>` is true, but not both   |
| 4        | implies  | Boolean                             | `<op1>` implies `<op2>` | True if `<op1>` is false, equals to `<op2>` otherwise     |

Operators on collections:

| Priority | Operator | Syntax                           | Operand Types    | Semantic                                            |
| -------- | -------- | -------------------------------- | ---------------- | --------------------------------------------------- |
| ?        | in       | `<item>` in `<collection>`       | All, Collection  | Provide an iterator in [for loops](#loop-statement) |
| ?        | contains | `<collection>` contains `<item>` | ?                | True if `<item>` can be found in `<collection>`     |
| 5        | +=       | `<collection>` += `item`         | Collection(T), T | Add `<item>` to `<collection>`                      |
| 5        | -=       | `<collection>` -= `item`         | Collection(T), T | Remove `<item>` from `<collection>`                 |

Global operators:

| Priority | Operator | Operand Types                   | Syntax             | Semantic                                                        |
| -------- | -------- | ------------------------------- | ------------------ | --------------------------------------------------------------- |
| 3        | =        | All                             | `<op1>` = `<op2>`  | True if `<op1>` is equal to `<op2>` (using Java's `equals`)     |
| 3        | !=       | All                             | `<op1>` != `<op2>` | True if `<op1>` is not equal to `<op2>` (using Java's `equals`) |
| 3        | <>       | All                             | `<op1>` <> `<op2>` | True if `<op1>` is not equal to `<op2>` (using Java's `equals`) |
| 5        | :=       | All (`<op1>` must be a l-value) | `<op1>` := `<op2>` | Set `<op2>` as the value of `<op1>`                             |

{{% notice note %}} 
As stated in the [Expressions section](#expressions) ALE relies on the AQL interpreter. As a result, most of these keywords are actually AQL keywords.
{{% /notice %}}

Parenthesis `()` can be used to change the priority of evaluation:

```
2 + 3 * 5   = 17;     // true
(2 + 3) * 5 = 25;     // true
```

## Expressions

Expressions are anything that returns a value. For instance:

```
true                     // the boolean true
1 + 5                    // 6
isVerbose or isDebug     // conditional boolean
```

{{% notice info %}} 
Expressions are evaluated thanks to the AQL interpreter and must hence be valid AQL expressions. See [AQL](#aql) for an overview of the language.
{{% /notice %}}

## Comments

### Simple and multi-line comments

Simple line comments start with `//`:

```
// This is a comment
String name := "Foo"; // This is another comment at the end of a line
```

Multi-ligne comments are written between `/*` and `*/`:

```
/* 
 * This comment
 * is on
 * several lines.
 */
```

### Documentation

Documentation for classes, attributes and operations can be written between `/**` and `*/`:

```
/**
 * The time before droping the request.
 */
int timeoutInMs := 10;
```

{{% notice note %}}
At the moment this documentation is not leveraged at all.
{{% /notice %}}

Statements
----------

## Statement

A statement is an instruction understandable by the ALE interpreter. A statement always ends with a semicolon (`;`):

```
self.greeting().log();
int length := 12;
```

### Variable declaration

A variable can be declared either within a class or an operation body. It follows the following syntax:

```
<type> <var_name> [:= <initial_value>];
```

`<type>` is the type of the variable.

`<var_name>` is a unique string identifying the variable. Two different variables with the same name cannot be defined in the same scope.

`<initial_value>` is an expression specifying the value of the variable. It must match `<type>`. It is optional; the following table list the default value given to the variable according to its type:

| Type      | Default value |
| --------- | ------------- |
| Integer   | 0             |
| Boolean   | false         |
| String    | ''            |
| Any other | null          |

<p></p>

{{%unsafeExpand "<b>Example</b>" %}}
```
int localVar;        // set to 0
int otherVar := 2;   // set to 2
```
{{% /unsafeExpand %}}

### Variable assignment

The `:=` operators allows to assign a value to a variable. It follows the following syntax:

```
<var_name> := <expression>;
```

`<var_name>` is the identifier used to declare the variable.

`<expression>` is the value that must take the variable. It must match the type of the variable.

{{%unsafeExpand "<b>Example</b>" %}}
```
aString := 'hello';
anInteger := 42;
```
{{% /unsafeExpand %}}

{{% notice warning %}} 
The assignment operator `:=` must not be confused with the comparison operator `=` used in expressions.
{{% /notice %}}

### Block statement

In ALE, the scope of a variable is determined by the block within which it has been declared. A block is defined between `{` and `}`.

### Condition statement

The `if` keyword allows to specify a condition before executing a block:

```
if (<guard>) {
    // execute if the guard is true
}
```

`<guard>` is any expression that can be evaluated to true. 

{{%unsafeExpand "<b>Example</b>" %}}
```
Boolean isRaining := true;

if (isRaining) {
    self.getFluffyUmbrella();
}
```
{{% /unsafeExpand %}}

The `else` keyword allows to execute a block if the guard evaluates to false. `else` can only be written after the `}` closing `if`'s block.

{{%unsafeExpand "<b>Example</b>" %}}
```
String weather := 'sunny';
String raining := 'raining';

if (weather = raining) {
    self.getFluffyUmbrella();
}
else {
    self.enjoySunshine();
}
```
{{% /unsafeExpand %}}

### Iteration statement

The `for` keyword allows to execute a block for each element of a collection:

```
for (<item> in <collection>) {
    // executed for each element of the collection
}
```
`<item>` is the name of a new variable that will take successively the value of each element of the collection. Only accessible within `for`'s block.

`<collection>` is an existing variable which multiplicity is greater than 1, such as a sequence or a set.

{{%unsafeExpand "<b>Example</b>" %}}
```
Sequence(String) names := Sequence{'Foo', 'Bar'};

for (name in names) {
    name.log(); // Print "Foo" on the first iteration then "Bar"
}
```
{{% /unsafeExpand %}}

It is also possible to iterate over a sequence of integers with a range comprehension (`[<min>..<max>]`):

```
for (i in [1..5]) {
    ('' + i).log(); // Print "1", then "2", etc.
}
```

### Loop statement

The `while` keyword allows to execute a block until a condition is evaluated to false. It follows the following syntax:

```
while (<condition>) {
    
}
```

`<condition>` is any expression that can be evaluated as a boolean.

{{%unsafeExpand "<b>Example</b>" %}}
```
while (isRaining) {
    self.keepUmbrellaOpened();
}
```
{{% /unsafeExpand %}}

### Switch expressions

The `switch` keyword allows to declare switch expressions:

```
int i := 2;
int square :=
    switch (var) {
        case 2 : 4
        case 3 : 9
        default : 0
    };

square.log(); // prints '4'
```

Instead of expressions, it is also possible to guard on type:

```
int i := 2;
String type :=
    switch (var) {
        case int    : 'int'
        case String : 'String'
        case EClass : 'EClass'
        default : 0
    };

square.log(); // prints 'int'
```

Classes and operations
----------------------

### Creating a new class

The `class` keyword allows to define a new class. It follows the following syntax:

```
class <class_name> {

}
```

`<class_name>` is a valid Java identifier. 

{{%unsafeExpand "<b>Example</b>" %}}
```
/**
 * A class that only exists during the runtime.
 */
class State {

}
```
{{% /unsafeExpand %}}

Unlike [open classes](#opening-a-class), these classes only exist at runtime, when the ALE interpreter is running. Such classes typically do not make sense as part of a model but are useful during the execution (e.g. for state management purposes).

### Defining operations

The `def` keyword allows to define new operations. It follows the following syntax:

```
def <return_type> <op_name>([<param_type> <param_name>]*) {

}
```

`<return_type>` defines the type of the value returned by the operation.

`<op_name>` is a string uniquely identifying the operation.

`<param_type> <param_name>` define the type and the name of a parameter. Parameters are optional and separated by commas (`,`).

An operation must be defined within a class body.

{{%unsafeExpand "<b>Example</b>" %}}
```
open class Vector {
    def int add(int a, int b) {
        result := self.a + self.b;
    }
}
```
{{% /unsafeExpand %}}

`result` is a special variable which is only accessible within an operation body. It stores the result of the operation and is automatically returned at the end of the operation body. As such, it replaces the `return` keyword used by a lot of programming languages.

Within a method, one can refer to the current instance with the `self` keyword. It allows to access instance's attributes and call instance's operations. 

{{%unsafeExpand "<b>Example</b>" %}}
```
open class User {
    def String fullname() {
        result := self.firstname + ' ' + self.lastname;
    }
}
```
{{% /unsafeExpand %}}

Unlike [overridden methods](#implementing-an-eoperation), these methods only exist at runtime, when the ALE interpreter is running. Semantically, that means that their are not part of DSL's abstract syntax but are still useful during the development.

### Instanciating an EClass

`create()` is a Java service (see [Call Java code](#calling-java-code)) that is automatically added by ALE to every EClass and which allows to create a new instance. It follows the following syntax:

```
<class_name> <var_name> := <package_name>::<class_name>.create();
```

`<class_name>` is the Java name of the class to instantiate.

`<var_name>` is the name of the variable that stores the new instance.

`<package_name>` is the Java package in which the class lies.

{{%unsafeExpand "<b>Example</b>" %}}
```
HelloWorld world := helloworld::HelloWorld.create();
```
{{% /unsafeExpand %}}

### Importing an existing class

The `import` keyword allows to use classes defined in another file. It follows the following syntax:

```
import <behavior> as <alias>
```

`<behavior>` is the ID of the behavior to which the class belongs.

`<alias>` is the name under which the behavior is known in the current file.

{{%unsafeExpand "<b>Example</b>" %}}
```
behavior fsm.composite.executable;

import fsm.executable as fsm;

open class Start {

    @main
    def void run()
        fsm.State initial = fsm::State.create();
    }
}
```
{{% /unsafeExpand %}}

## Open Class

This chapter binds ALE's syntax with EMF concepts and explains how the ALE script can affect a metamodel at runtime.

--------------------------------------------------

### Open classes

The `open` keyword allows to re-open an existing EClass to add new elements and implement existing EOperations. We call such classes: "**open classes**". It follows the following syntax:

```
behavior <EClass_package>

open class <EClass> {

}
```

{{%unsafeExpand "<b>Example</b>" %}}
```
behavior helloworld;

open class HelloWorld {

}
```
{{% /unsafeExpand %}}

{{%notice info %}}
An *.ale* file can declare only one `open class` per EClass.
{{% /notice %}}

### Declaring a new attribute

[Creating a variable](#variable-declaration) in the body of an opened in fact adds a new attribute to the weaved EClass. If the feature is a primitive (boolean, int, string, etc.) it is inferred as an EAttribute. Otherwise it is inferred as an EReference.

{{%unsafeExpand "<b>Example</b>" %}}
```
open class FSM {
    State currentState;

    override void on(String event) {
        if (event = 'right-click') {
            self.currentState := fsm::MoveState.create();
        }
    }
}
```
{{% /unsafeExpand %}}

{{% notice tip %}}
The new feature should be runtime specific, such as adding a currentState inside a Finite State Machine.
{{% /notice %}}

A multiplicity can be specified to indicate that the attribute represents several values. It follows the following syntax:

```
<min>..<max> <type> <name>;
```

`<min>` is the minimum number of values in the attribute.

`<max>` is the maximum number of values. `*` indicates any number of values.

`<type>` is the type of the values acceptable in the attribute.

`<name>` is the name of the attribute.

{{%unsafeExpand "<b>Example</b>" %}}
```
open class FSM {
    0..* State states;

    override def addState(State newState) {
        self.states += newState;
    }

    def void display() {
        for (State state in self.states) {
            state.display();
        }
    }
}
```
{{% /unsafeExpand %}}

### Declaring bidirectional references

The `opposite` keyword allows to declare a bidirectional reference. It is equivalent to the EMF opposite relation. It follows the following syntax:

```
opposite <var_name_in_opposite_class> <opposite_class> <var_name_in_class>;
```

`<opposite_class>` is the name of the class with which the bidirectional must be set.

`<var_name_in_opposite_class>` is the name of the variable holding the reference to the current class in the opposite class.

`<var_name_in_class>` is the name of the variable holding the reference in the current EClass.

{{% notice warning %}}
An opposite reference must be declared in **both classes**.
{{% /notice %}}

{{%unsafeExpand "<b>Example</b>" %}}
```
class ParentNode {
    // can be accessed with self.child
    opposite parent ChildNode child;
}

class ChildNode {
    // can be accessed with self.parent
    opposite child ParentNode parent;
}
```
{{% /unsafeExpand %}}

### Declaring a set

The `unique` keyword allows to declare a multiplicity-many attribute that should only store unique values. Values are compared thanks to their Java `equals` method. It is equivalent to the EMF unique feature. It follows the following syntax:

```
unique <multiplicity> <type> <var_name>
```

`<multiplicity>` is the multiplicity of the attribute (see [declaring a new attribute](#declaring-a-new-attribute)). It must be a many multiplicity.

`<type>` is the type of the elements contained in the collection.

`<var_name>` is the name of the variable holding the reference.

{{%unsafeExpand "<b>Example</b>" %}}
```
class Parent {
    unique 0..* Child children;    
}
```
{{% /unsafeExpand %}}

### Implementing an EOperation

The `override` keyword allows to implement the behavior of an EOperation declared in the ECore metamodel of the weaved EClass. We call such operations: "**overridden operations**". It follows the following syntax:

```
override <type> <name>([<param_type> <param_name>]*) {
   <statement>*
}
```

`<type>` is the type of the value returned by the operation.

`<name>` is the name of the operation.

`<param_type> <param_name>` define the type and the name of a parameter. Parameters are optional and separated by commas (`,`).

`<stamement>` is an arbitrary number of [statements](#statements).

{{% notice info %}}
An overridden operation can only be declared within an open class an must have the exact same signature as an existing EOperation from the weaved EClass or one of its super types.
{{% /notice %}}

{{%unsafeExpand "<b>Example</b>" %}}
```
open class Circle {
    override int circumference() {
        double PI := 3.14159;
        result := self.radius * PI * 2;
    }
}
```
{{% /unsafeExpand %}}

{{% notice tip %}}
See also [defining operations](#defining-operations) for further details about operation syntax.
{{% /notice %}}


### Inheriting open classes

The `extends` keyword allows to extend an open class with another open class.

When writing an Open Class you may want to specialize one (or more) existing open class.
The new Open Class reuses all the inherited content, declares new features/operations and refines body of inherited operations.

The extended open class have to be weaved on the same EClass (or super type) of the current open class.

It follows the following syntax:

```
open class <name> extends <open_class_1>[, <open_class_n>]* {

}
```

`<name>` is the name of the extending class.

`<open_class_1>` is the name of the open class being extended. An open class may inherit from several open classes; in such a case the name of the extended classes must be separated by commas (`,`).

Any open class from the same file can be extended.

{{%unsafeExpand "<b>Example</b>" %}}
```
open class State {
    override String execute() {
        result := 'State ' + self.name;
    }
}

open class Initial extends State {
    override String execute() {
        result := 'Initial State ' + self.name;
    }
}
```
{{% /unsafeExpand %}}

Classes from other files can be extended too but must be imported first (see [importing an existing class](#importing-an-existing-class)).

{{%unsafeExpand "<b>Example</b>" %}}
```
behavior fsm.composite.executable;

import fsm.executable as simplefsm;

open class CompositeState extends simplefsm.State {
    override void exec() {
        // Redefine the behavior here
    }
}
```
{{% /unsafeExpand %}}

---------------------------------------------------------------------

Misc
----

### Calling Java code

ALE offers the possibility to call static methods written in Java from the body of an EOperation.

For example let's assume that you have a Java class `MyService` providing the method `foo()`:

```
package some.packagename;

public class MyService {

    // By convention the caller object is the first argument
    public static void foo(EObject caller) {
        System.out.println("Foo: "+ caller.eClass().getName());
    }

}
```

You can call `foo()` on any EObject just by importing the class `MyService` with the keyword `use` at the beginning of your `.ale` file.
The only requirement is that `MyService` has to be in the classpath of your project.

```
use some.packagename.MyService; //Import external Java services

    open class FSM {
        def void callJavaFoo() {
            self.states.forAll(state | state.foo());
        }
    }

```



### Printing to the console

ALE provides the `log()` method that can be used on String instances to print themselves to the console.

{{%unsafeExpand "<b>Example</b>" %}}
```
'Hello World!'.log();
('' + 42).log();
```
{{% /unsafeExpand %}}