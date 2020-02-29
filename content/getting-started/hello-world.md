---
title: "Hello World!"
weight: 2
---

## Requirements

* Have at least a basic knowledge of [EMF (Eclipse Modeling Framework)](https://www.eclipse.org/modeling/emf/).
* Have [installed ALE]({{< ref "installation.md" >}}).

## Objectives

 * Discover the structure of an ALE project through a built-in example.
 * Launch your first ALE program.

## Get the HelloWorld example

ALE provides an `Hello world!` project template:

1. `File > New > Example...`
2. `EcoreTools ALE Examples > Hello world!`
3. Select `helloworld`
4. `Finish`

After a few seconds a new project called *helloworld* should be created in your workspace. This project defines a simple `HelloWorld` EClass able to print "Hello world!". The content of the project is presented below.

## What we have inside

The interesting files of the `helloworld` project are inside the `model` folder:

| File               | Defines                                                                                |
| ------------------ | -------------------------------------------------------------------------------------- |
| _HelloWorld.aird_  | Graphical representation of _HelloWorld.ecore_                                         |
| _HelloWorld.ale_   | Behavior of _HelloWorld.ecore_                                                         |
| _HelloWorld.dsl_   | Binding between the metamodel (_HelloWorld.ecore_) and its behavior (_HelloWorld.ale_) |
| _HelloWorld.ecore_ | Metamodel describing the EClass HelloWorld                                             |
| _HelloWorld.xmi_   | Executable instance of the EClass HelloWorld                                           |

By opening _HelloWorld.aird_ you will see the `HelloWorld` EClass and its properties:

![HelloWorld EClass](/images/HelloWorld.png)

As you can see, all the members of `HelloWorld` are displayed in a bold font. That indicates that they are defined inside _HelloWorld.ale_.

{{% notice tip %}}
If the members are not shown make sure that [the Behavior layer is activated]({{< ref "features/sirius-integration.md#behavior-layer" >}}).
{{% /notice %}}

 _HelloWorld.ale_ contains the following code:

```
behavior HelloWorld;

open class HelloWorld {             // 1

    String msg := 'Hello world!';   // 2

    override EString greeting() {   // 3
        result := self.msg;         // 4
    }

    @main                           // 5
    def void main() {
        self.greeting().log();      // 6
    }
}
```
<ul style="list-style:none">
 <li>① Indicate that we modify the <code>HelloWorld</code> EClass.</li> 
 <li>② Declare a <i>new</i> attribute of type <code>String</code>. Defining <code>msg</code> within <i>HelloWorls.ale</i> makes it a runtime data. In other words, it does not exist in the metamodel and will be created by the ALE interpreter during the execution.</li>
 <li>③ Specify the behavior of the <code>greeting</code> operation.</li>
 <li>④ Return the value of the <code>msg</code> attribute (there is no <code>return</code> statement in ALE).</li>
 <li>⑤ Indicate that the <code>main</code> operation is the entry point of the execution and should be called by the ALE interpreter.</li>
 <li>⑥ Print "Hello world!".</li>
</ul>

{{% notice tip %}}
See the [Reference chapter]({{< ref "reference/_index.md" >}}) for a detailed overview of ALE's syntax.
{{% /notice %}}

## Run!

The execution can be launched through the contextual menu:

1. Right-click on _HelloWorld.dsl_
2. Select `Run As > ALE launch`, a dialog should open asking you to select the model to interpret
3. Make sure _HelloWorld.xmi_ is selected then click on `OK`.
4. Witness the result on the console:

```
Run helloworld.dsl
------------
Hello world!
```

## Conclusion

You should now have an idea of what can be achieved with ALE. Move on the [next topic for an overview of ALE's syntax]({{< ref "syntax-overview.md" >}}).

