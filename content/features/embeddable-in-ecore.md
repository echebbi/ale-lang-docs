+++
title = "Embeddable in Ecore"
weight = 2
+++

## Save ALE behavior in the Ecore metamodel

ALE code can be added to *.ecore* metamodels through EAnnotations to define the body of EOperations. That allows to group both the metamodel and its behavior, making easier to share them.

## How to

1. Open the Ecore metamodel with the *Sample Ecore Model Editor*
2. Select an ``EOperation``
3. Right-click > *New Child* > *EAnnotation* > *EAnnotation*
4. Select the ``EAnnotation``
5. In the *Properties* view, set ``Source`` to ``http://implementation/``
6. Right-click on the ``EAnnotation`` > *New Child* > *Details Entry*
7. Select the ``Details Entry``
8. In the *Properties* view, set ``Key`` to ``body`` and type the corresponding ALE source code in ``Value``