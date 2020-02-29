---
title: "Java API"
weight: 3
---

## Run the ALE interpreter programmatically

The [AleInterpreter](https://github.com/gemoc/ale-lang/blob/ease-contributions/plugins/org.eclipse.emf.ecoretools.ale/src/org/eclipse/emf/ecoretools/ale/ALEInterpreter.java) class provides a public API to interpret ALE scripts.

It can be used as follows:

```java
// Retrieve:
//    - the .dsl file defining the metamodel and its behavior
//    - the .xmi file defining the model to execute

IResource dslFile = ...
String dslFileLocation = dslFile.getLocationURI().getPath();
IResource xmiModelFile = ...
String xmiModelFileLocation = xmiModelFile.getLocation().toString();

// Initialize the ALE interpreter

List<Object> args = List.of();
Set<String> plugins = Set.of();
Set<String> projects = Set.of(dslFile.getProject().getName(), xmiModelFile.getProject().getName());

ALEInterpreter interpreter = new ALEInterpreter();
interpreter.javaExtensions.updateScope(plugins,projects);
interpreter.javaExtensions.reloadIfNeeded();

// Run the ALE interpreter

IEvaluationResult result = interpreter.eval(
    xmiModelLocation, args, new WorkbenchDsl(dslFileLocation)
);
```

{{% notice tip %}}
`AleInterpreter` is defined in the `org.eclipse.emf.ecoretools.ale` bundle.
{{% /notice %}}