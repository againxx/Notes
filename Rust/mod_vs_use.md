# Mod vs Use

## TLDR
* Using `use` brings a Rust item into the current scope, `use` is primarily used to make code cleaner and less verbose
* Using `mod` defines a module which is a collection of Rust items, or literally brings the contents of a file and inserts in its place.
* There is no need to explicitly import crates in Rust using `use`. When you compile your crate, Cargo will handle this automatically.

## Use
* `use` is like C++'s **using-declaration**, by using it we can make things less repetitive, and more concise
* Using `use` is mostly **optional**. It does not function like an `import` statement.

#### {} glob-like syntax
* `use a::b::{c, d, e::f, g::h::i};`

#### self keyword
* You can use the `self` keyword, allowing you to bring the common parent module into the namespace as well as any items you want to access
    - `use std::collections::hash_map::{self, HashMap}`

#### as keyword
* You can use `as` keyword to rename items and avoid naming conflicts
    - `use a::b::{self as ab, c as abc}`

#### asterisk wildcard syntax
* You can also use the asterisk wildcard syntax to bind all paths matching a given prefix
    - this is like C++'s **using-directive**

## Mod
#### module source filenames
* We can write a `mod` statement without declaring a body. When you do this and compile your crate, Cargo will look a `.rs` file in
the current directory with the name given after the `mod` declaration.

Imaging we have the following file structure with `lib.rs` containing `pub mod utilities;`
```
.
└── media
   ├── utilities.rs
   └── lib.rs
```
* Cargo **brings the contents of** `utilities.rs` **and inserts it into the current file**.
* This means that in `lib.rs` you can use any items you've written in `utilities.rs` as if they were actually written inside a `mod utilities {}` block
* By declaring `utilities` a module, you have added it to the tree hierarchy of your crate and the function `download` (inside `utilities.rs`) can now be accessed by
its path `media::utilities::download` by anyone who installs your crate.
* **We cannot replace** `pub mod utilities;` **line with a** `use` **statement**. We have to declare `utilities.rs` as a module, so it's added to the crate structure

## Reference
[The difference between mod and use in Rust | panaetius.io](https://panaetius.io/post/2020/11/the-difference-between-mod-and-use-in-rust/)
