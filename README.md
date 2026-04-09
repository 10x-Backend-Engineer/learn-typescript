# Learn TypeScript

Welcome to the comprehensive TypeScript course. TypeScript is a typed superset of JavaScript that compiles to plain JavaScript.

# Table of contents

- **Getting Started**
  - [What is TypeScript?](#what-is-typescript)
  - [Why learn TypeScript?](#why-learn-typescript)
  - [Installation and Setup](#installation-and-setup)

- **Chapter I**
  - [Basic Types](#basic-types)
  - [Interfaces](#interfaces)
  - [Type Aliases](#type-aliases)
  - [Enums](#enums)
  - [Union Types](#union-types)
  - [Intersection Types](#intersection-types)

- **Chapter II**
  - [Functions](#functions)
  - [Classes](#classes)
  - [Generics](#generics)
  - [Type Guards](#type-guards)
  - [Conditional Types](#conditional-types)
  - [Mapped Types](#mapped-types)

- **Chapter III**
  - [Decorators](#decorators)
  - [Modules](#modules)
  - [Utility Types](#utility-types)

- **Chapter IV**
  - [React with TypeScript](#react-with-typescript)
  - [Node.js with TypeScript](#nodejs-with-typescript)

- **Appendix**
  - [Next Steps](#next-steps)
  - [References](#references)

# What is TypeScript?

TypeScript is a strongly typed programming language that builds on JavaScript, giving you better tooling at any scale. It was developed and is maintained by Microsoft.

## Key Characteristics

- **Static Typing**: TypeScript allows you to declare types, catching errors during development.
- **Compile to JavaScript**: TypeScript code is transpiled to JavaScript.
- **Type Inference**: TypeScript can infer types even when you don't explicitly declare them.
- **Modern Features**: TypeScript supports ES6+ features and more.
- **Tooling**: Enhanced IDE support with autocomplete and error checking.

# Why learn TypeScript?

## 1. Better Error Detection

TypeScript catches errors during development with static type checking.

```typescript
function add(a: number, b: number): number {
    return a + b;
}

add("hello", "world"); // Error!
```

## 2. Improved Developer Experience

TypeScript provides better autocomplete, inline documentation, and refactoring support.

## 3. Growing Ecosystem

Many popular frameworks like Angular, React, and Vue support TypeScript.

# Installation and Setup

## Installing TypeScript

```bash
npm install -g typescript
tsc --version
```

## tsconfig.json

```bash
npx tsc --init
```

```json
{
    "compilerOptions": {
        "target": "ES2020",
        "module": "commonjs",
        "strict": true,
        "outDir": "./dist",
        "rootDir": "./src"
    }
}
```

## Running TypeScript

```bash
npx tsc
npx tsc --watch
npx ts-node src/index.ts
```

# Basic Types

## Number

```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let big: bigint = 100n;
```

## String

```typescript
let name: string = "John";
let template: string = `Hello, ${name}!`;
```

## Boolean

```typescript
let isActive: boolean = true;
let isComplete: boolean = false;
```

## Array

```typescript
let numbers: number[] = [1, 2, 3];
let strings: Array<string> = ["a", "b", "c"];
```

## Tuple

```typescript
let tuple: [string, number];
tuple = ["hello", 42];
```

## Any

```typescript
let anything: any = 4;
anything = "hello";
```

## Void

```typescript
function log(message: string): void {
    console.log(message);
}
```

## Never

```typescript
function error(message: string): never {
    throw new Error(message);
}
```

## Unknown

```typescript
let unknownValue: unknown = 4;
if (typeof unknownValue === "number") {
    console.log(unknownValue + 2);
}
```

# Interfaces

## Basic Interface

```typescript
interface User {
    name: string;
    age: number;
}

const user: User = { name: "John", age: 30 };
```

## Optional Properties

```typescript
interface User {
    name: string;
    age?: number;
}
```

## Readonly Properties

```typescript
interface User {
    readonly id: number;
    name: string;
}
```

## Interface Extends

```typescript
interface Animal {
    name: string;
}

interface Dog extends Animal {
    breed: string;
}
```

## Function Interface

```typescript
interface SearchFunc {
    (source: string, subString: string): boolean;
}
```

## Class Interface

```typescript
interface Printable {
    print(): void;
}

class Document implements Printable {
    print() {
        console.log("Printing...");
    }
}
```

# Type Aliases

```typescript
type ID = string | number;
type Point = { x: number; y: number };
type Callback = () => void;
```

# Enums

## Numeric Enums

```typescript
enum Direction {
    Up,    // 0
    Down,  // 1
    Left,  // 2
    Right  // 3
}
```

## String Enums

```typescript
enum Status {
    Success = "SUCCESS",
    Error = "ERROR"
}
```

## Const Enums

```typescript
const enum Colors {
    Red = "RED",
    Green = "GREEN"
}
```

# Union Types

```typescript
let id: string | number;
id = "abc123";
id = 42;

function padLeft(value: string | number, padding: string | number) {
    if (typeof value === "string") {
        return value + padding;
    }
    return String(padding) + value.toString();
}
```

## Discriminated Unions

```typescript
interface Bird {
    type: "bird";
    flyingSpeed: number;
}

interface Horse {
    type: "horse";
    runningSpeed: number;
}

type Animal = Bird | Horse;

function move(animal: Animal) {
    switch (animal.type) {
        case "bird": return animal.flyingSpeed;
        case "horse": return animal.runningSpeed;
    }
}
```

# Intersection Types

```typescript
interface A { a: string; }
interface B { b: number; }

type AB = A & B;

const obj: AB = { a: "hello", b: 42 };
```

# Functions

```typescript
function greet(name: string): string {
    return `Hello, ${name}!`;
}

function add(a: number, b: number): number {
    return a + b;
}
```

## Optional Parameters

```typescript
function buildName(first: string, last?: string): string {
    if (last) return `${first} ${last}`;
    return first;
}
```

## Default Parameters

```typescript
function greet(name: string = "Guest"): string {
    return `Hello, ${name}!`;
}
```

## Rest Parameters

```typescript
function sum(...numbers: number[]): number {
    return numbers.reduce((a, b) => a + b, 0);
}
```

## Overloadings

```typescript
function reverse(x: string): string;
function reverse(x: number): number;
function reverse(x: string | number): string | number {
    if (typeof x === "string") {
        return x.split("").reverse().join("");
    }
    return Number(x.toString().split("").reverse().join(""));
}
```

# Classes

```typescript
class Greeter {
    greeting: string;
    
    constructor(message: string) {
        this.greeting = message;
    }
    
    greet(): string {
        return `Hello, ${this.greeting}`;
    }
}
```

## Access Modifiers

```typescript
class Person {
    public name: string;       // Accessible everywhere
    private age: number;       // Only in class
    protected id: number;      // In class and subclasses
    readonly createdAt: Date;  // Cannot be modified
}
```

## Parameter Properties

```typescript
class Person {
    constructor(
        public name: string,
        private age: number
    ) {}
}
```

## Inheritance

```typescript
class Animal {
    constructor(public name: string) {}
    move(distance: number = 0) {
        console.log(`${this.name} moved ${distance}m`);
    }
}

class Dog extends Animal {
    constructor(name: string, private breed: string) {
        super(name);
    }
    bark(): void {
        console.log("Woof!");
    }
}
```

## Abstract Classes

```typescript
abstract class Shape {
    abstract getArea(): number;
    
    display(): void {
        console.log(`Area: ${this.getArea()}`);
    }
}

class Circle extends Shape {
    constructor(public radius: number) { super(); }
    getArea(): number {
        return Math.PI * this.radius ** 2;
    }
}
```

# Generics

## Basic Syntax

```typescript
function identity<T>(arg: T): T {
    return arg;
}

const result = identity<string>("hello");
const num = identity(42);
```

## Generic Interfaces

```typescript
interface Container<T> {
    value: T;
    getValue(): T;
}
```

## Generic Classes

```typescript
class Box<T> {
    private content: T;
    
    set(value: T): void { this.content = value; }
    get(): T { return this.content; }
}

const box = new Box<number>();
box.set(42);
```

## Generic Constraints

```typescript
interface Lengthwise {
    length: number;
}

function logLength<T extends Lengthwise>(arg: T): number {
    return arg.length;
}
```

## Keyof Constraint

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
}
```

# Type Guards

## typeof

```typescript
function pad(value: string | number) {
    if (typeof value === "string") {
        return value.length;
    }
    return value.toFixed(2);
}
```

## instanceof

```typescript
class Dog {
    bark(): void { console.log("Woof!"); }
}

class Cat {
    meow(): void { console.log("Meow!"); }
}

function speak(animal: Dog | Cat) {
    if (animal instanceof Dog) {
        animal.bark();
    } else {
        animal.meow();
    }
}
```

## Custom Type Guards

```typescript
function isFish(pet: Fish | Bird): pet is Fish {
    return (pet as Fish).swim !== undefined;
}
```

# Conditional Types

```typescript
type TypeName<T> = T extends string ? "string" : "not string";

type A = TypeName<string>; // "string"
type B = TypeName<number>;  // "not string"
```

## Infer

```typescript
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

type Func = () => string;
type R = ReturnType<Func>; // string
```

# Mapped Types

```typescript
type Readonly<T> = {
    readonly [P in keyof T]: T[P];
};

type Partial<T> = {
    [P in keyof T]?: T[P];
};
```

## Key Remapping

```typescript
type Getters<T> = {
    [P in keyof T as `get${Capitalize<string & P>}`]: () => T[P];
};
```

# Decorators

Enable in tsconfig.json:
```json
{
    "compilerOptions": {
        "experimentalDecorators": true
    }
}
```

## Class Decorator

```typescript
function sealed(constructor: Function) {
    Object.seal(constructor);
}

@sealed
class Person {}
```

## Method Decorator

```typescript
function log(target: any, key: string, descriptor: PropertyDescriptor) {
    const original = descriptor.value;
    descriptor.value = function(...args: any[]) {
        console.log(`Calling ${key}`);
        return original.apply(this, args);
    };
    return descriptor;
}
```

# Modules

## ES Modules

```typescript
// math.ts
export const PI = 3.14;
export function add(a: number, b: number): number {
    return a + b;
}

// main.ts
import { PI, add } from "./math";
import * as math from "./math";
```

# Utility Types

## Partial<T>

```typescript
type User = { name: string; age: number };
type PartialUser = Partial<User>;
// { name?: string; age?: number }
```

## Required<T>

```typescript
type User = { name?: string; age?: number };
type RequiredUser = Required<User>;
// { name: string; age: number }
```

## Pick<T, K>

```typescript
type User = { name: string; age: number; email: string };
type UserPreview = Pick<User, "name" | "email">;
```

## Omit<T, K>

```typescript
type User = { name: string; age: number; email: string };
type UserWithoutAge = Omit<User, "age">;
```

## Record<K, V>

```typescript
type Page = "home" | "about" | "contact";
type PageInfo = Record<Page, { title: string }>;
```

## Exclude<T, U>

```typescript
type T0 = Exclude<"a" | "b" | "c", "a">; // "b" | "c"
```

## Extract<T, U>

```typescript
type T0 = Extract<"a" | "b" | "c", "a" | "f">; // "a"
```

## ReturnType<T>

```typescript
function f(): { a: number; b: string } { return { a: 1, b: "hi" }; }
type T0 = ReturnType<typeof f>;
```

## Parameters<T>

```typescript
type T0 = Parameters<() => void>;              // []
type T1 = Parameters<(s: string) => void>;     // [s: string]
```

# React with TypeScript

## Functional Components

```typescript
import React from "react";

interface Props {
    name: string;
    age?: number;
    onClick: (name: string) => void;
}

const UserCard: React.FC<Props> = ({ name, age = 18, onClick }) => {
    return (
        <div onClick={() => onClick(name)}>
            <h1>{name}</h1>
            <p>{age} years old</p>
        </div>
    );
};
```

## useState with Types

```typescript
const [name, setName] = useState<string>("");
const [user, setUser] = useState<User | null>(null);
const [items, setItems] = useState<{ id: number; name: string }[]>([]);
```

## useRef Types

```typescript
const inputRef = useRef<HTMLInputElement>(null);
const countRef = useRef<number>(0);
```

# Node.js with TypeScript

```bash
npm install --save-dev @types/node
```

```typescript
import express, { Request, Response } from "express";

interface User {
    id: number;
    name: string;
}

const app = express();

app.get("/users/:id", (req: Request, res: Response) => {
    const id = parseInt(req.params.id);
    res.json({ id, name: "John" } as User);
});
```

# Next Steps

Now that you know TypeScript fundamentals:

- Build React apps with TypeScript
- Create Node.js APIs with TypeORM
- Learn testing with Jest
- Explore NestJS framework

# References

- [TypeScript Documentation](https://www.typescriptlang.org/docs)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript)
- [React TypeScript Cheatsheet](https://react-typescript-cheatsheet.netlify.app)
