---
title: "Run the interpreter"
weight: 1
---

## Get an interpreter

The [IAleInterpreter](https://github.com/gemoc/ale-lang/blob/master/plugins/org.eclipse.emf.ecoretools.ale.core/src/org/eclipse/emf/ecoretools/ale/core/interpreter/IAleInterpreter.java) interface provides a public API to evaluate an ALE program.

An interpreter shouldn't be instantiated directly but instead retrieved from an [IAleEnvironment](https://github.com/gemoc/ale-lang/blob/master/plugins/org.eclipse.emf.ecoretools.ale.core/src/org/eclipse/emf/ecoretools/ale/core/env/IAleEnvironment.java). An environment defines the metamodels and the ALE behaviors that are known by the interpreter.

Several factory methods allow to instantiate an environment:

```java
// The environment is loaded from a .dsl configuration file
IAleEnvironment dsl = IAleEnvironment.fromDslFile(new File("helloworld.dsl"));

// The environment is loaded from specific Ecore and ALE source files
IAleEnvironment env = IAleEnvironment.fromPaths(List.of("helloworld.ecore"), List.of("helloworld.ale"));
```

To get the associated interpreter:

```java
IAleInterpreter interpreter = env.getInterpreter();
```

{{% notice warning %}}
Always use ALE environments in **try-with-resource** statements: they hold a lot of resources and can cause memory leaks.
{{% /notice %}}

## Get the caller and the main method

An interpreter runs by calling a ``@main`` method on an EObject. Both the method and the object **must** be loaded by the environment, otherwise they won't be properly resolved by the interpreter:

```java
EObject      caller = environment.loadModel(createURI("HelloWorld.xmi")).get(0);
Method       main   = environment.getBehaviors().getMainMethods().get(0);
List<Object> args   = emptyList();
```

## Run the interpreter and use the results

```java
// Run the interpreter
//
IAleInterpreter   interpreter = environment.getInterpreter();
IEvaluationResult result      = interpreter.eval(caller, main, args);

// Check the results
//
Object valueReturnedByMainMethod  = result.getValue();
DiagnosticLogger evaluationErrors = interpreter.getLogger();
```

## Full code example

```java
IProject project = workspace.getProject("helloworld");

try (IAleEnvironment env = IAleProject.from(project).getEnvironment()) 
{
    EObject      caller = environment.loadModel(createURI("HelloWorld.xmi")).get(0);
    Method       main   = environment.getBehaviors().getMainMethods().get(0);
    List<Object> args   = emptyList();

    IAleInterpreter   interpreter = environment.getInterpreter();
    IEvaluationResult result      = interpreter.eval(caller, main, args);

    if (result.getDiagnostic().getSeverity == Diagnostic.OK) {
        System.out.println("Method returned: " + result.getValue());
    }
    else {
        System.out.println("Failure");
    }
}
```