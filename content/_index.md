# Action Language for EMF

The [Action Language for EMF (ALE)](https://github.com/gemoc/ale-lang) is a language used to make Ecore metamodels executable. Define the behavior of your models in a dedicated, interpreted and object-oriented language and **run it in minutes!**

![ALE allows to weave behavior into Ecore models](images/overview.png)

{{% notice tip %}}
With ALE, you can execute your models right from your IDE: you no longer need to spend time generating and tweaking Java code!
{{% /notice %}}

## Main features
 * **Executable metamodeling**: re-open existing EClasses to insert new methods with their implementations
 * **Metamodel extension**: the very same mechanism can be used to extend existing Ecore metamodels and insert new features (eg. attributes) in a non-intrusive way
 * **Interpreted**: no need to deploy Eclipse plugins, just run the behavior on a model directly in your modeling environment
 * **Extensible**: if ALE doesn't fit your needs, register Java classes as services and invoke them directly from ALE

## Breathe life into your metamodels!

ALE makes it easy to address a wide range of activities related to model elements manipulation. This includes activities such as:
 * weaving operational semantics in metamodel definitions,
 * defining model checkers,
 * defining model-to-model transformations,
 * defining model-to-text transformations.


## Open-class mechanism

The following ALE snippet defines the behavior of an FSM:
```
behavior fsm.dummy.implementation;

open class FSM {

    State currentState;
    String currentEvent;

    override void execute(EList<String> events) {
        'Start'.log();
        self.currentState := self.initialState;
        for(event in events) {
            self.currentState.execute();
            self.currentState :=
                self.currentState.transitions
                    ->select(t | t.event = self.currentEvent)
                    ->first();
        }
        'End'.log();
    }

}
```
