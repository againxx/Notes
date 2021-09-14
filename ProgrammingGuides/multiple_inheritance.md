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
