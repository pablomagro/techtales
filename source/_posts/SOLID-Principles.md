---
title: SOLID Principles
date: 2023-07-14 10:29:52
tags:
  - SOLID Principles
categories:
  - Design
  - TypeScript
---

These 5 principles will guide you on how to ``write better code``. Though they come from object-oriented programming.

It's much easier to work on small Singly Responsible parts whose changes don't affect any upstream or downstream part.

1. ``S`` - `Single responsibility principle`
  A class should have only one reason to change. It means that a class should have only one responsibility or purpose
1. ``O`` - `Open closed principle`
  Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.
1. ``L`` - `Liskov substitution principle`
  Subtypes must be substitutable for their base types.
1. ``I`` - `Interface segregation principle`
  Clients should not be forced to depend on interfaces they do not use.
1. ``D`` - `Dependency Inversion principle`
  High-level modules should not depend on low-level modules; both should depend on abstractions.

Helping the code to:
- Tolerate change.
- Ease code understanding.
- Write components that can be used in many software systems.

## NOTE ##
`SOLID is a must know skill in OO development` but I think we should be willing to modernize it and make it fit in 2022 when industry is moving towards functional coding. I’m a 20 year c# vet and do full solid on most projects but it’s hard to justify the abstractions for smaller projects.  You end up with too many single method classes which can be functions instead.

## S — Single responsibility principle  (SRP)
"There should never be more than one reason for a class to change." same idea different words: "a class should have only one job and do one thing"

```Typescript
// Bad
class Book {
  public title: string;
  public author: string;
  public description: string;
  public pages: number;

  // constructor and other methods

  public saveToFile(): void {
    // some fs.write method to save book to file
  }
}

// Good
class Book {
  public title: string;
  public author: string;
  public description: string;
  public pages: number;

  // constructor and other methods
}

class BookPersistence {
  public saveToFile(book: Book): void {
    // some fs.write method to save book to file
  }
}
```

## O — Open-Close Principle (OCP)
“Software entities should be open for extension, but closed for modification.”

There are two primary attributes in the OCP:

1. It is open for extension — This means you can extend what the module can do.
1. It is closed for modification — This means you cannot change the source code, even though you can extend the behavior of a module or entity.

OCP means that a class, module, function, and other entities can extend their behavior without modifying their source code. In other words, an entity should be extendable without modifying the entity itself.

```Typescript
// Bad
// If we add another shape later, which means we need to create a new class.
// In that case, we would also need to modify the AreaCalculator class to calculate the area of the new class. That’s against the Open-Close  Principle.

class Rectangle {
  public width: number;
  public height: number;

  constructor(width: number, height: number) {
    this.width = width;
    this.height = height;
  }
}

class Circle {
  public radius: number;

  constructor(radius: number) {
    this.radius = radius;
  }
}

class AreaCalculator {
  public calculateRectangleArea(rectangle: Rectangle): number {
    return rectangle.width * rectangle.height;
  }

  public calculateCircleArea(circle: Circle): number {
    return Math.PI * (circle.radius * circle.radius);
  }
}

// God
interface Shape {
  calucatelateArea(): number;
}

class Rectangle extends Shape {
  public width: number;
  public height: number;

  constructor(width: number, height: number) {
    this.width = width;
    this.height = height;
  }

  calculateArea() {
    return this.width * this.height;
  }
}

class Circle extends Shape  {
  public radius: number;

  constructor(radius: number) {
    this.radius = radius;
  }

  calculateArea() {
    return Math.PI * (this.radius * this.radius);
  }
}

Class AreaCalculator {
  calculateAreas(shapes: Shape[]): number {
    return shapes.reduce(calculateArea, shape)
      => calculateArea + shape.calculateArea(), 0);
  }
}
```

## L — Liskov substitution principle (LSP)
If you have a function that works for a base type, it should work for a derived type.

    In simple terms, if a program is written to work with a certain type (superclass), it should also work correctly with any of its derived types (subclasses) without requiring any modifications.

```Typescript
// A classic example of a violation of this principle is the Rectangle-Square problem.
// The Square class extends the Rectangle class and assumes that the width and height are equal. When calculating the area of a square, we’d get a wrong value.

class Rectangle {
  constructor(private _width: number, private _height: number) {}

  public area() : number {
    return this._height * this._width;
  }
}

class Square extends Rectangle {

}

// Good

interface Shape {
  public area(): number;
}

class Rectangle extends Shape {
  constructor(private _width: number, private _height: number) {}

  public area() : number {
    return this._height * this._width;
  }
}

class Square extends Rectangle {
  constructor(private _height: number) {}

  public area() : number {
    return Math.pow(this._height, 2);
  }
}
```

## I — Interface segregation principle (ISP)
“Many client-specific interfaces are better than one general-purpose interface.”

The principle suggests that using client-specific interfaces instead of a general-purpose interface prevents the implementation of unnecessary methods in classes, ensuring better design.

```Typescript
// Bad

interface VehicleInterface {
  drive(): string;
  fly(): string;
}

class FutureCar implements VehicleInterface {
  public drive() : string {
    return 'Driving Car.';
  }

  public fly() : string {
    return 'Flying Car.';
  }
}

class Car implements VehicleInterface {
  public drive() : string {
    return 'Driving Car.';
  }

  public fly() : string { // <-- A car shouldn't implement this method.
    throw new Error('Not implemented method.');
  }
}

class Airplane implements VehicleInterface {
  public drive() : string { // <-- A fly shouldn't implement this method.
    throw new Error('Not implemented method.');
  }

  public fly() : string {
    return 'Flying Airplane.';
  }
}

// Good. Splliting in interfaces

interface AirplaneInterface {
  fly(): string;
}

interface CarInterface {
  fly(): string;
}

class FutureCar implements CarInteface, AirplaneInterface {
  public drive() : string {
    return 'Driving Car.';
  }

  public fly() : string {
    return 'Flying Car.';
  }
}

class Car implements CarInterface {
  public drive() : string {
    return 'Driving Car.';
  }
  }
}

class Airplane implements AirplaneInterface {
  public fly() : string {
    return 'Flying Airplane.';
  }
}
```

## D — Dependency Inversion principle (DIP)
"Entities must depend on abstractions not on concretions. It states that the high level module must not depend on the low level module, but they should depend on abstractions."

This principle states that a class should not depend on another class, but instead on an abstraction of that class. It allows loose-coupling and more reusability.

`It means that classes should depend on abstractions (interfaces or abstract classes) rather than concrete implementations.`

- Design Principles and Design Patterns:

    “If the open-closed principle (OCP) states the goal of object oriented (OO) architecture, the DIP states the primary mechanism”.

```Typescript
// Bad
// Here, the Post class depends on the MemoryStorage class to save new posts.
// What happens if we need to change the storage used to save posts? We’ll have to modify the PostService class to change the type of the db property, thus violating the Open-Closed Principle .

class MemoryStorage {
  private storage: any[];

  constructor() {
    this.storage = [];
  }

  public insert(record: any): void {
    this.storage.push(record);
  }
}

class PostService {
  private db = new MemoryStorage();

  createPost(title: string) {
    this.db.insert(title);
  }
}

// Good

interface GenericStorage {
  insert(record: any): void;
}

class MemoryStorage extends GenericStorage {
  private storage: any[];

  constructor() {
    this.storage = [];
  }

  public insert(record: any): void {
    this.storage.push(record);
  }
}

class PostService {
  private db = new GenericStorage();

  constructor(db: GenericStorage) {
    this.db = db;
  }

  createPost(title: string) {
    this.db.insert(title);
  }
}
```