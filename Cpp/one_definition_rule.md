# One Definition Rule

One definition rule can be abbreviated as ODR

* In any translation unit, a **template**, **type**, **function**, or **object** can have no more than one definition
* In the entire program, an **object** or **non-inline function** cannot have more than one definition
* **Types**, **templates**, and **extern inline function** can be defined in more than one translation unit, each definition must be the same
* **Non-extern objects** and **Non-extern function** in different translation units are different entries
