# Ownership

## The Stack and The Heap

The stack and the heap are parts of memory available to your code at runtime.

_Stack_

- The stack stores values in order it gets them and removes the values in the opposite order. Last in, first out. Like a stack of plates.
- You push and pop from the stack.
- All data stored on the stack must have a known fixed size.
- Pushing to the stack is faster than allocating on the heap (on top O(1), vs finding a space).
- When calling a function, the values passed to it and that functions local variables are pushed onto the stack. When the function is over, they are popped of.

_Heap_

- Data put on the heap is done by requesting an amount of space.
- Memory allocator finds an empty spot in the heap that is big enough, marks it as being in use, and returns a pointer, which is the address of that location.
- Allocatoin on the heap
- A pointer to the heap is a known fixed size, you can store the pointer on the stack.
- When you want the actual data you follow the pointer.
- Accessing data on the heap is slower than accessing data on the stack due to following the pointer.

## Ownership Rules

- Each value in Rust has an owner
- There can only be one owner at a time
- When the owner goes out of scope, the value will be dropped

- If a type has implemented the Drop trait, it will never have the Copy trait
- Copy is used to make deep copy of items on the Stack
- Drop is used to delete the pointer and it's reference to a segment of heap data when a variable becomes out of scope

- You can move values from one owner to another. This allows you to build, rearrange, and tear down the ownership tree
- Very simple types like integers, floating-point numbers, and characters are excused from the ownership rule. These are called Copy types
- You can "borrow a reference" to a value; references are non-owning pointers with limited lifetimes

## Move

Operations like assigning a value to a variable, passing it to a function, or returning it from a function don't copy the value: they move it.

## References

While ownership can be passed around via returns to new variable instantiation, we can also use references.
The act of creating a reference is called _borrowing_.

You can use `&` to borrow a variable in other functions.

You can use `mut` to enable editing of a variable and in combination with `&` to pass a mutable version of an borrowed variable.

RESTRICTION: a mutable reference to a value, you can have no other references to that value.

This restriction prevents data races:

- two or more pointers access the same data at the same time.
- at least one pointer is being used to write to data.
- there is no mechanism being used to synchronize access to the data.

Rules of References

- at any given time, you can have either one mutable reference or any number of immutable references
- references ust always be valid

## The Slice Type

Slices let you reference a contiguous sequence of elements in a collections rather than the whole collection. A slice is a kind of reference, so it does not have ownership.

```rust
let s = String::from("hello world");
let hello = &s[0..5];
let world = &s[6..11];
```

# Copy on Structs

When making custom Structs, use the the `#[derive(Copy, Clone)]` to ensure values that are Copy Types inherit this trait.

```rust
#[derive(Copy, Clone)]
struct YourStruct { number: u32 }
```

# Rc and Arc: Shared Ownership

Rust provides reference-counted pointer type Rc and Arc

Arc (atomic reference count): is safe to share between threads directly
Rc (reference count): faster, non thread safe code to update reference count
