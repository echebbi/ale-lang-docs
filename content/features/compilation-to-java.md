+++
title = "Compilation to Java"
weight = 12
+++

## ALE Compiler

The [Action Language for EMF Compiler (ALEC)](https://github.com/gemoc/ale-lang-compiler) allows to compile ALE source files as Java code for **better performances** and **integration with existing tools**.

## Main features

 - **Integration with Eclipse IDE**: compile ALE behaviors in the Eclipse IDE
 - **Maven integration**: automatically compile your behaviors using the ALE compiler Maven plugin
 - **Configurable**: the ALE Compiler can target four implementation patterns: Interpreter, Visitor, EMF’s Switch and [Revisitor]({{< ref "research.md#publications" >}})

## Prerequisites

At the moment ALEC is not embedded within ALE and must be installed separately. To this end:

1. `Help > Install New Software...`
2. Fill the `Work with` field with the update site's URL:
   - http://www.kermeta.org/ale-lang-compiler/updates/latest/
3. Hit `Enter` and wait for the list to load
4. Check `Action Language EMF Compiler`
5. Click `Next` then `Finish`

{{% notice info %}}
Archived versions of ALEC can be found under http://www.kermeta.org/ale-lang-compiler/updates/
{{% /notice %}}

## Compilation from the Eclipse IDE

1. Create a new ALE project with a metamodel and some behavior
2. Open the *.dsl* file and add the following line:  
   ```
   compilationType=interpreter
   ```
3. Right-click on the *.dsl* file then `ALE > Generate Ale Implementation`
4. A compiled version of the ALE behavior should have been generated in the `interpreter-comp/` directory.

This compiled version is implemented with the Interpreter pattern. By substituing `interpreter` for `visitor`, `switch` or `revisitor` on step ② you can freely compile to another implementation pattern.

## Compilation with Maven

{{% notice info %}}
We do not cover the details of the integration of you project using maven but several example of ALE projects with a Maven integration can be found in the [ALE Compiler repository](https://github.com/gemoc/ale-lang-compiler/tree/master/languages).
{{% /notice %}}

To execute ALEC as part of your Maven builds you have to add the `alecompiler-maven-plugin` to your project's POM:

```xml
<build>
    <sourceDirectory>${pattern}-comp</sourceDirectory>
    <plugins>
        <plugin>
            <groupId>org.eclipse.emf.ecoretools.ale.compiler</groupId>
            <artifactId>alecompiler-maven-plugin</artifactId>
            <version>1.0.0-SNAPSHOT</version>
            <executions>
                <execution>
                    <phase>generate-sources</phase>
                    <goals>
                        <goal>ale-dsl-compile</goal>
                    </goals>
                </execution>
            </executions>
            <configuration>
                <dslFile>${project.basedir}/src/${metamodel.name}.dsl</dslFile>
            </configuration>
        </plugin>
    </plugins>
</build>
```