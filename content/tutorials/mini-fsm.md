+++
title = "Mini-FSM Tutorial"
weight = 1
+++

### Objectives

- Learn how to make an Ecore model executable.

{{% notice info %}}
This is **not** a tutorial about EMF and some basic knowledge is expected. You can learn more about EMF [on Vogella](https://www.vogella.com/tutorials/EclipseEMF/article.html) or [on EclipseSource](https://eclipsesource.com/blogs/tutorials/emf-tutorial/)
{{% /notice %}}

### Introduction

For this first tutorial we'll implement a simple FSM. So, what is it?

[Wikipedia’s definition](https://en.wikipedia.org/wiki/Finite-state_machine):
> [A FSM] is a mathematical model of computation. It is an abstract machine that can be in exactly one of a finite number of states at any given time. The FSM can change from one state to another in response to some external inputs; the change from one state to another is called a transition. A FSM is defined by a list of its states, its initial state, and the conditions for each transition.

![FSM sample](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9e/Turnstile_state_machine_colored.svg/330px-Turnstile_state_machine_colored.svg.png)

Basically, it is a system which can be in different states, which behaves differently according to its current state and transition from one state to another upon certain events.

### 1. Import the _minifsm_ example project

The _minifsm_ example project defines a simple FSM metamodel with no behavior. To import it in the workspace:

1. `File > New > Example...`
2. `EcoreTools ALE Examples > Tutorials`
3. Select `minifsm`
4. `Finish`

The metamodel defined in this project is the following:

![FSM metamodel](/images/minifsm_metamodel_diagram.png)

We are now going to define its behavior. 

{{% notice tip %}}
The [Sirius integration]({{< ref "features/sirius-integration.md" >}}) provides handy features to both visualize and edit behavioral elements directely from a Sirius representation.
{{% /notice %}}

### 2. What do we want?

Let's pause for a moment and think about what we want to achieve exactly. Basically, we have the following behaviors to implement:
 - state to state transition
 - state execution

### 3. Behavior implementation

First of all, to check whether a transition can be activated we have to keep track of the current event. Open the _minifsm.ale_ file and add a `currentEvent` attribute to `FSM`:

```
behavior minifsm;

open class FSM {

    String currentEvent;

}
```

We can now implement `Transition.isActivated` as follows:

```
open class Transition {
    override boolean isActivated() {
        boolean isRelatedToCurrentState := self.incoming = self.fsm.currentState
        boolean isExpectedEvent := self.fsm.currentEvent = self.event;
        result := isRelatedToCurrentState and isExpectedEvent;
    }
}
```

We are checking that:
 * the event triggered by the Transition is the same as the current event handle by the FSM,
 * the incoming State from the Transition is the current State of the FSM.

The content of the variable `result` will be returned at the end of `isActivated`.  
The variable `self` refers to the current object (here it is a Transition).


In a similar way we implement `State.execute`:

```
open class State {
    override void execute() {
        ('  Execute ' + self.name).log();
    }
}
```

The `log` method is used to print an object.

And for the implementation of `FSM.handle`:

```
open class FSM {
    override void handle (EString event) {
        (' Handle ' + event).log();
        self.currentEvent := event;

        self.currentState :=
            self.transitions
                ->select(t | t.isActivated())
                ->first()
                .outgoing;
    }
}

```

Here we simply update `currentEvent`, search for an activated `Transition` and update `currentState` accordingly.

### 4. Entry point definition

To complete the behavior of our language, we will now define an entry point to run an FSM.

Create a new method annotated with `@main` in FSM:

```
open class FSM {
    @main
    def void run() {

    }
}
```

The `main` tag indicates that this method will be automatically called when executing an FSM.

Here we will create a sequence of 2 events, initialize FSM's current state with an initial state and then forward the events to the FSM:

```
open class FSM {
    @main
    def void run() {
        'Start'.log();

        Sequence(String) events := Sequence{'event1','event2'};

        self.currentState :=
            self.states
                ->select(s | s.oclIsKindOf(minifsm::InitialState))
                ->first();
        self.currentState.execute();

        for(event in events) {
            self.handle(event);
            self.currentState.execute();
        }

        'End'.log();
    }
}
```

The complete example should look as follows:

![complete minifsm example, with metamodel and behavior](/images/minifsm_complete_language_screenshot.png)

### 5. Create a dynamic instance

Before testing our implementation we need an actual FSM model:

1. Select `Dynamic > Dynamic instance`
2. Click on `FSM`
3. Name it `FSM.xmi` and click `Finish`
4. In the automatically opened `FSM.xmi`, right click on `FSM` and select `New Child > States Initial State`
5. Name it `First` in the `Properties` view
6. Create a child `State` named `Second` and a `Final State` named `Third`
7. Create a `Transition` and edit the properties `Event` to `event1`, `Incoming` to  `First` and `Outgoing` to `Second`
8. Add another `Transition` from `Second` to `Third` with `event2`

Your FSM model should look like:

![FSM model](/images/minifsm_model_tree.png)

### 6. Run!

Now we can test!

1. Right click on `minifsm.dsl`
2. Select `Run As > ALE launch`
3. Enter `*xmi`
4. Select `FSM.xmi`
5. Then click `OK`

Console output:

```
Run minifsm.dsl
------------
Start
  Execute First
 Handle event1
  Execute Second
 Handle event2
  Execute Third
End
```

### Conclusion

Congratulations, you created an executable language from scratch!

Given an Ecore metamodel you implemented its EOperations with ALE and you run it on an FSM model.
