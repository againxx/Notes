# Difference between Class and Struct

> Member of a class defined with the keyword _class_ are private by default.
> Members of a class defined with the keywords _struct_ or _union_ are public by default.

> In absence of an access-specifier for a base class, public is assumed when the derived class is declared _struct_
> and private is assumed when the class is declared _class_.

* Additional difference: the keyword **class** can be used to declare template parameters, while the **struct** keyword cannot be so used

## Reference
* C++ Primer 15.5
