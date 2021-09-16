# Multiple Inheritance

#### Distinguish interface inheritance from implementation inheritance
The main reasons fro subclassing:
* Inheritance of interface creates a subtype, implying an "is-a" relationship
    - Backbone of a framework
* Inheritance of implementation avoids code duplication by reuse
    - Implementation detail, can often be replaced by composition and delegation

#### Make interfaces explicit with ABCs
* In modern Python, if a class is designed to define an interface, it should be an explicit ABC.

#### Use Mixins for code reuse
* If a class is designed to provide method implementations for reuse by multiple unrelated subclasses (without **is-a** relationship).
It should be an explicit _mixin_ class
* A mixin does not define a new type; it merely bundles methods for reuse.
* A mixin should never be instantiated, and concrete classes should not inherit only from a mixin

#### Make Mixins explicitly by naming
* There is no formal way in Python to state that a class is a mixin (c++ either), so it is highly recommended that they are named with a **...Mixin** suffix

#### An ABC may also be a Mixin; The reverse is not true
* Because an ABC can implement concrete methods, it works as a mixin as well.
* An ABC also defines a type, which a mixin does not.
* An ABC can be the sole base class of any other class, while a mixin should never be subclassed alone.

#### Don't subclass from more than one concrete class
* Concrete classes should have zero or at most one concrete superclass
    - All but one of the superclasses of a concrete class should be ABCs or mixins

#### Provide aggregate classes to users
* _aggregate class_ brings some combination of ABCs or mixins together in a sensible way
* It brings together some superclasses so that the user doesn't need to remember all ABCs and mixins or wonder if they need to be declared in a certain order in **class** statement

#### Favor object composition over class inheritance
* It's too easy to overuse class inheritance
