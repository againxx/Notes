# Trait

## What's a trait

> A trait is a set of methods that can be used to extend the functionality of a class

Difference between **interface** and **mixin**:
* An interface may define one or more behaviors via method signatures
* A trait defines behaviors via full method definitions (including method bodies)
* A mixin includes full method definitions and may also carry state through member variable, while traits usually don't.

## Goal
The main goal of trait is horizontal code reuse and not wanting to necessarily inherit from an abstract class

## Type traits in C++
* In C++, type traits are a suit of templates defined in `<type_traits>` which can be used for type transformation in template metaprogramming
