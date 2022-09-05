# OOP Patterns & Principles

- [OOP Patterns & Principles](#oop-patterns--principles)
  - [The Four Fundamental Principles of OOP](#the-four-fundamental-principles-of-oop)
  - [SOLID Principles](#solid-principles)
    - [1. Single Responsibility (SRP)](#1-single-responsibility-srp)
    - [2. Open-Closed (OCP)](#2-open-closed-ocp)
    - [3. Liskov Substitution (LSP)](#3-liskov-substitution-lsp)
    - [4. Interface Segregation (ISP)](#4-interface-segregation-isp)
    - [5. Dependency Inversion (DIP)](#5-dependency-inversion-dip)
  - [Design Patterns](#design-patterns)
    - [Dependency Injection](#dependency-injection)
    - [Guard Pattern](#guard-pattern)

## The Four Fundamental Principles of OOP

- Abstraction: Modeling the relevant attributes and interactions of entities as
  classes to define an abstract representation of a system.

- Encapsulation: Hiding the internal state and functionality of an object and
  only allowing access through a public set of functions.

- Inheritance: Ability to create new abstractions based on existing
  abstractions.

- [Polymorphism][1]: Ability to implement inherited properties or methods in
  different ways across multiple abstractions.

## [SOLID Principles][2]

- [Separation of concerns][14] and [loose coupling][12] are a recurring benefit
  of adherence to SOLID principles. The adoption of SOLID principles promotes
  the general maintainability, reusability and testability of a codebase.

### 1. Single Responsibility [(SRP)][7]

> An object should only have one reason to change.

- N.B. The terms _"reason to change"_ and _"responsibility"_ are essentially
  interchangable with regards to SRP.

- Always pay regard to separation of concerns. Keeping an object tightly
  focused on a single concern makes it more robust and reliable, as well as
  being simpler to understand and reuse.

- Different abstractions should be represented by separate objects. Closely
  related tasks and functionality can be bundled under one object's
  responsibility.

### 2. Open-Closed [(OCP)][8]

> Open for extension; Closed for modification.

- Write objects so that they can be extended when new features are required
  eg. via an interface, or inheritance.

- Adherence to OCP allows object behaviour to be extended without having to
  modify its internals and potentially that of its inheritors/peers.

### 3. Liskov Substitution [(LSP)][9]

> If S is a [subtype][3] of T, Obj(T) can be replaced with Obj(S) \- without
> breaking the program.

- N.B. Subtyping is referred to informally as Inheritance, within the domain
  of OOP.

- Object subtypes (objects that extend another object) should be written
  to be interchangable with their supertype (the object that they extend).
  As such, program elements (functions, methods etc.) written to operate on
  elements of the supertype should also be able to operate on elements of the
  subtype as well.

- For type signatures of a derived object \- less specific types are allowed
  for method parameters (contravariance) eg. `Number` could substitute for
  `Integer` , whereas more specific types are allowed for method return types
  (covariance) eg. `Integer` could substitute for `Number`.

- In addition to the above, every inherited method in the subtype must
  preserve the intrinsic properties of the supertype. Preconditions cannot be
  strengthened, postconditions cannot be weakened and all invariants must be
  maintained. Methods introduced by the subtype should not be used to change
  state in a way inpermissable for the supertype (also known as the "History
  Rule").

- Adherence to LSP helps to prevent unexpected software behaviour and crashes
  due to subtype incompatibilities, as well as making it easier to ensure
  that classes fulfil the ["IS A"][5] criterion for inheritance as a true
  subtype.

> Technically, it's called ["Behavioural Subtyping"][6] \- subtypes behave like supertypes.
>
> \- [_Barbara Liskov, April 20, 2016_][4]

### 4. Interface Segregation [(ISP)][10]

> No client should be forced to depend upon interfaces that they do not use.

- Interfaces that are overly broad and monolithic should be broken down into
  smaller interfaces of smaller size and higher specificity. These
  streamlined interfaces can be referred to as ["Role Interfaces"][13].

### 5. Dependency Inversion [(DIP)][11]

> 1. High-level modules should not import from low-level modules. _Both should
>    depend upon abstractions_ (e.g. interfaces, abstract classes, factories).
>
> 2. Abstractions should not depend on concretions. _Concretions should depend
>    upon abstractions_.

## Design Patterns

### Dependency Injection

A dependency is an object that another object depends on. Hard-coded
dependencies are problematic and should be avoided for the following reasons:

1. To replace a hard-coded dependency with a different implementation, the
   containing object must be modified (which violates [OCP][8]).

2. If the hard-coded dependency has dependencies of its own, they must also be
   configued by the containing object \- thus scattering configuration code
   across the application (decreasing code maintainability and potentially
   violating [DRY][15]).

3. Mocks/stubs cannot be used to substitute for hard-coded dependencies
   (decreasing code testability).

Dependency injection is an implementation of [DIP][11] that addresses the
aforementioned problems by:

- The use of an interface or base class to abstract away the dependency
  concretion.
- Using a service to maintain a collection of dependency instances, which can
  then be _injected_ into the objects that require them via a:
  - _constructor_ \- for required dependencies.
  - _property_ \- for when it is desirable for a dependency to be settable after
    object instantiation.
  - _method_ \- for when it is unknown which dependency will be required until
    the point of use.

### Guard Pattern

It is often a good idea to reject certain types or values as a condition of
further code execution. This idea can be encapsulated into what is known as the
_Guard Pattern_:

> A boolean expression that must evaluate to `true` before program execution can
> continue.

- N.B. `undefined` is equivalent to `null` within the context of a Javascript
  loose equality check ([ref: loose equality using the `==` operator][16]).

```typescript
// Example guard helper function
function rejectNullOrUndefined<T>(arg: T | undefined | null): void {
  if (<T>arg == null) {
    throw new Error("Guard failure: parameter is null or undefined");
  }
}
```

---

---

[1]: https://en.wikipedia.org/wiki/Polymorphism_(computer_science)
[2]: https://docs.microsoft.com/en-us/archive/msdn-magazine/2014/may/csharp-best-practices-dangers-of-violating-solid-principles-in-csharp
[3]: https://en.wikipedia.org/wiki/Subtyping
[4]: https://www.youtube.com/watch?v=-Z-17h3jG0A
[5]: https://www.w3resource.com/java-tutorial/inheritance-composition-relationship.php
[6]: https://en.wikipedia.org/wiki/Behavioral_subtyping
[7]: https://en.wikipedia.org/wiki/Single-responsibility_principle
[8]: https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle
[9]: https://en.wikipedia.org/wiki/Liskov_substitution_principle
[10]: https://en.wikipedia.org/wiki/Interface_segregation_principle
[11]: https://en.wikipedia.org/wiki/Dependency_inversion_principle
[12]: https://en.wikipedia.org/wiki/Coupling_(computer_programming)
[13]: https://martinfowler.com/bliki/RoleInterface.html
[14]: https://en.wikipedia.org/wiki/Separation_of_concerns
[15]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
[16]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness#loose_equality_using
