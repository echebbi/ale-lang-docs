+++
title = "File extensions"
weight = 1
+++

This chapter presents all the files used to configure ALE.

---------------------------------------------------------------------

## DSL file (*.dsl*)

This file describes a Domain Specific Language (DSL) made executable with ALE. Its file extension is *dsl*.

It defines both the abstract syntax (Ecore models) and the semantics (ALE source files) of the DSL.

It is a standard Java properties file (i.e. a textual file where each line follows the syntax `key=value`)

A typical DSL files contains the following entries:

| Key        | Value                                           |
| ---------- | ----------------------------------------------- |
| `syntax`   | A comma separated list of paths to *.ecore* files |
| `behavior` | A comma separated list of paths to *.ale* files   |


##### Examples:

{{%expand "logo-standalone.dsl" %}}
```
syntax=../logo.model/model/ASMLogo.ecore,../logo.model/model/VMLogo.ecore
behavior=../logo.example/data/LogoProgram.ale
```
{{% /expand %}}

{{%expand "logo.dsl" %}}
```
syntax=platform:/resource/logo.model/model/ASMLogo.ecore,platform:/resource/logo.model/model/VMLogo.ecore
behavior=platform:/resource/logo.example/data/LogoProgram.ale
```
{{% /expand %}}


{{% notice tip %}}
Eclipse Platform URL schemes are also supported, which eases the location of files within a workspace: `platform:/resource/<project>/<source_file.ale>`
{{% /notice %}}

---------------------------------------------------------------------

## Behavior file (*.ale)

This file defines a DSL implementation (i.e. its semantics).

It allows to re-open EClass from the abstract syntax to mainly implements existing EOperations but also to declare new ones, new features and even new classes specific to the runtime.

It uses the file extension *ale*. <br>
The file must start with `behavior <unique identifier>`. <br>

##### Example:

{{%expand "fsm.ale" %}}
```
behavior fsm.implementation;

open class FSM {
    override void exec() {
        // Do stuff
    }
}

class Variables {
    // Store values here
}
```
{{% /expand %}}
