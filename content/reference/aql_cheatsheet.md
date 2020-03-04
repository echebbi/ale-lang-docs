+++
title = "AQL cheatsheets"
weight = 3
+++

See [AQL syntax reference](https://www.eclipse.org/acceleo/documentation/aql.html#SyntaxReference) for an in-depth presentation of the language.

-------------------

### Type of

```java
anEPackage.oclIsKindOf(ecore::ENamedElement) // true
anEPackage.oclIsTypeOf(ecore::ENamedElement) // false
```

### Services for collections

```
OrderedSet{'a', 'b', 'c'} + OrderedSet{'c', 'b', 'f'}
Sequence{'a', 'b', 'c'}->any(str | str.size() = 1)
Sequence{'a', 'b', 'c'}->asOrderedSet()
OrderedSet{'a', 'b', 'c'}->asSequence()
Sequence{'a', 'b', 'c', 'c', 'a'}->asSet()
Sequence{'a', 'b', 'c'}->at(1)
Sequence{'a', 'b', 'c'}->collect(str | str.toUpper())
OrderedSet{'a', 'b', 'c'}->concat(Sequence{'d', 'e'})
OrderedSet{'a', 'b', 'c'}->count('d')
Sequence{'a', 'b', 'c'}->excludes('a')
Sequence{'a', 'b'}->excludesAll(OrderedSet{'a','f'})
OrderedSet{'a', 'b', 'c'}->excluding('c')
Sequence{'a', 'b', 'c'}->exists(str | str.size() > 5)
Sequence{anEClass, anEAttribute}->filter(ecore::EStructuralFeature)
Sequence{'a', 'b', 'c'}->first()
Sequence{'a', 'b', 'c'}->forAll(str | str.size() = 1)
Sequence{'a', 'b', 'c'}->includes('d')
Sequence{'a', 'b', 'c'}->includesAll(OrderedSet{'a', 'f'})
OrderedSet{1, 2, 3, 4}->indexOf(3)
OrderedSet{'a', 'b', 'c'}->insertAt(2, 'f')
OrderedSet{'a', 'b', 'c'}->intersection(OrderedSet{'a', 'f'})
OrderedSet{'a', 'b', 'c'}->isEmpty()
Sequence{'a', 'b', 'c'}->isUnique(str | str.size())
Sequence{'a', 'b', 'c'}->last()
OrderedSet{'a', 'b', 'c'}->notEmpty()
Sequence{'a', 'b', 'c'}->one(str | str.equals('a'))
OrderedSet{'a', 'b', 'c'}->prepend('f')
OrderedSet{'a', 'b', 'c'}->reject(str | str.equals('a'))
OrderedSet{'a', 'b', 'c'}->reverse()
Sequence{'a', 'b', 'c'}->select(str | str.equals('a'))
Sequence{'a', 'b', 'c'}->sep('[', '-', ']')
Sequence{'a', 'b', 'c'}->sep('-')
Sequence{'a', 'b', 'c'}->size()
Sequence{'aa', 'bbb', 'c'}->sortedBy(str | str.size())
Sequence{'a', 'b', 'c'} - Sequence{'c', 'b', 'f'}
OrderedSet{'a', 'b', 'c'}->subOrderedSet(1, 2)
Sequence{'a', 'b', 'c'}->subSequence(1, 2)
Sequence{1, 2, 3, 4}->sum()
Sequence{'a', 'b', 'c'}->union(Sequence{'d', 'c'})
```