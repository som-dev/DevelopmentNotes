# S.O.L.I.D. Design Principles

## Single Responsibility Principle
A class should have only one responsibility, only one reason to change.

## Open/Close Principle
A class should be open to extension but closed to modification (barring bug fixes).

## Liskov Substitution Principle
Derived classes must be substitutable for their base classes.  If your derived class has an empty or throw-only override method from the interface, there is something wrong with the interface.

## Interface Segregation Principle
Prefer many fine-grained interfaces for specific roles rather than a few monolithic interfaces.

## Dependency Inversion Principle
Depend on interfaces/abstractions and not on concrete classes.
