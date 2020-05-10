---
title: "Manipulate ALE behaviors"
weight: 3
---

## Get ALE behaviors

The [IBehaviors](https://github.com/gemoc/ale-lang/blob/master/plugins/org.eclipse.emf.ecoretools.ale.core/src/org/eclipse/emf/ecoretools/ale/core/env/IBehaviors.java) interface provides a public API to manipulate the behaviors defined in ALE.

Behaviors can be obtained from an [IAleEnvironment](https://github.com/gemoc/ale-lang/blob/master/plugins/org.eclipse.emf.ecoretools.ale.core/src/org/eclipse/emf/ecoretools/ale/core/env/IAleEnvironment.java). An environment keeps track of a set of Ecore metamodels and of the ALE behaviors that are defined upon them.

Several factory methods allow to instantiate an environment:

```java
// The environment is loaded from a .dsl configuration file
IAleEnvironment dsl = IAleEnvironment.fromDslFile(new File("helloworld.dsl"));

// The environment is loaded from specific Ecore and ALE source files
IAleEnvironment env = IAleEnvironment.fromPaths(List.of("helloworld.ecore"), List.of("helloworld.ale"));
```

To get the associated behaviors:

```java
IBehaviors behaviors = env.getBehaviors();
```

{{% notice warning %}}
Always use ALE environments in **try-with-resource** statements: they hold a lot of resources and can cause memory leaks.
{{% /notice %}}

## Check ALE classes

```java
// The classes defined in an Ecore metamodel
// and which behavior is defined in ALE 
//
List<ExtendedClasses> openClasses = behaviors.getOpenClasses();

// The classes defined in ALE 
// and which do not belong to any metamodel
//
List<ExtendedClasses> openClasses = behaviors.getOpenClasses();
```