---
title: "Deal with ALE projects"
weight: 2
---

## Get an existing project

The [IAleProject](https://github.com/gemoc/ale-lang/blob/master/plugins/org.eclipse.emf.ecoretools.ale.ide/src/org/eclipse/emf/ecoretools/ale/ide/project/IAleProject.java) interface provides a public API to manipulate an ALE project:

```java
IProject project = workspace.getProject("helloworld");

if (IAleProject.hasAleNature(project)) {
    IAleProject aleProject = IAleProject.from(project);

    // The environment provides access to the metamodels 
    // and the ALE behaviors available in the project.
    //
    // It is configured from either project's preferences
    // or a .dsl file, depending on project's configuration.
    //
    IAleEnvironment env = aleProject.getEnvironment();

    // The environment provides an interpreter 
    // that can be used to execute Ecore models (.xmi)
    //
    IAleInterpreter interpreter = aleProject.getInterpreter();
}
```

## Create a new project

The [WorkspaceAleProject](https://github.com/gemoc/ale-lang/blob/master/plugins/org.eclipse.emf.ecoretools.ale.ide.ui/src/org/eclipse/emf/ecoretools/ale/ide/ui/project/WorkspaceAleProject.java) defines nested classes to describe and create new ALE projects:

```java
IWorkspace workspace = ResourcesPlugin.getWorkspace();

// Describe the project to create.
//
// ALE projects can be configured in several ways and
// that's why the constructor takes a lot of arguments.
//
WorkspaceAleProject.Description desc = new WorkspaceAleProject.Description(
    isUsingAnExistingEcoreModel, ecoreModelFilePath, 
    ecorePackageName, 
    hasSiriusRepresentation, 
    hasJavaNature
);

// Do create the project in the workspace
//
Template project = new WorkspaceAleProject.Template(workspace, desc);
project.create(projectName, projectPath, new NullProgressMonitor());
```