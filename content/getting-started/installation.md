---
title: "Installation"
date: 2020-02-28T13:49:58+01:00
weight: 1
---

## Install ALE from its update site

#### 1. Install Eclipse IDE

The recommended package is [Eclipse IDE for Java and DSL developers](https://www.eclipse.org/downloads/packages/release/2019-09/r/eclipse-ide-java-and-dsl-developers).

#### 2. Install Sirius 6.0.0

1. Open Eclipse IDE
2. Go to `Help > Install New Software...`
3. Copy Sirius 6.0.0 [update site's URL](http://download.eclipse.org/sirius/updates/releases/6.0.0/photon/) in the `Work with` textbox
   * [http://download.eclipse.org/sirius/updates/releases/6.0.0/photon/](http://download.eclipse.org/sirius/updates/releases/6.0.0/photon/)
4. Hit `Enter` and wait for the list to load
5. Check `Sirius Core Runtime`
6. Click `Next` and `Finish`
 
#### 3. Install ALE

1. Open Eclipse IDE
2. Go to `Help > Install New Software...`
3. Copy the [update site's URL](https://ci.inria.fr/gemoc/job/ale-lang/lastSuccessfulBuild/artifact/releng/org.eclipse.emf.ecoretools.ale.updatesite/target/repository/) in the `Work with` textbox
   * [http://www.kermeta.org/ale-lang/updates/latest/](http://www.kermeta.org/ale-lang/updates/latest/)
4. Hit `Enter` and wait for the list to load
5. Check `Action Language for EMF`
6. Click `Next` and `Finish`
7. Restart the IDE

You are ready to go!

## Install other versions

#### Archived versions

- Archived versions of ALE can be found at the following URL: [http://www.kermeta.org/ale-lang/updates/](http://www.kermeta.org/ale-lang/updates/)

#### Nightybuilt versions

- Latest version built by the continuous integration is available at: [https://ci.inria.fr/gemoc/job/ale-lang/job/master/lastSuccessfulBuild/artifact/releng/org.eclipse.emf.ecoretools.ale.updatesite/target/repository/](https://ci.inria.fr/gemoc/job/ale-lang/job/master/lastSuccessfulBuild/artifact/releng/org.eclipse.emf.ecoretools.ale.updatesite/target/repository/)

To install a version:
1. Pick its URL (which is in the form [http://www.kermeta.org/ale-lang/updates/yyyy-mm-dd/](http://www.kermeta.org/ale-lang/updates/yyyy-mm-dd/))
2. Use it in Eclipse IDE as explained above.