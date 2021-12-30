# TypeScript базовые вещи
___

## Basic types
```ts
const a:number = 12;
const b: string = "Hello world";
const c = "Hello world"; // можно
const bool: boolean = true;

const d = a + b;
// const e = bool + a; нельзя

let arr: string[] = ["Hello", "World"];

let another_a: any = 3;
another_a = "Hello world"; // можно, но крайне не рекомендуется

function test(a: string): string | number {
    return 1;
}

const test2 = (a: number): number => {
    return a*2;
}

arr = arr.map((s: string) => s.toUpperCase());

function printIt(a: number | string) {
    if (typeof a === "string") {
        console.log(a.toUpperCase());
    }
}

function isArray(a: number | number[]) {
    if (Array.isArray(a)) {
        a.map((s) => {});
    }
}

function voided(a: number): void {
    console.log("void");
}

const x: undefined = undefined;
const z: null = null;

function countCoord(coord: { lat: number, long?: number }) {

}

type Point = {x: number, y: number};

interface IPoint {
    x: number,
    y: number
}

interface I3DPoint extends IPoint {
    z: number;
}

// аналог для type
type D3Point = Point & {
    z: number;
}

type stringOrNumber = string | number; // лучше использовать type в этом случае

function print(coord: IPoint) {
    console.log("Hello world");
}


// Что недоступно для type ( добавление в интерфейс новых св-в ):

interface ITest {
    a: number;
}

interface ITest {
    b: number;
}

//

// const c1 = (point: IPoint) => {
//     const d: I3DPoint = point; // error
// }

const c2 = (point: IPoint) => {
    const d: I3DPoint = point as I3DPoint; // norm!
}

const element = document.getElementById('canvas') as HTMLCanvasElement;

```

## Literals
```ts
// Литеральные типы

let c3: 'test' = 'test'; // у переменной может быть только значение 'test'

type actionType = 'up' | 'down'; // тип принимает зн-ия либо "up" либо "down"

// ф-ия возвращает либо -1 либо 1
function performActionType(action: actionType): 1 | -1 {
    switch (action) {
        case "down":
            return 1;
        case "up":
            return -1;
    }
}
```

## Enums
```ts
enum Direction {
    Up = "Up",
    Down = "Down",
    Right = "Right",
    Left = "Left"
}

enum Decision {
    Yes = 1,
    No = calcEnum()
}

function calcEnum() {
    return 2;
}

function runEnum(obj: { Up: string }) {

}
runEnum(Direction);

enum Test {
    A
}

let testing = Test.A; // 0
let nameA = Test[testing]; // A

const enum ConstEnum {
    A,
    B
}

console.log(ConstEnum.A + " " + ConstEnum.B); // 0 1

enum Dice {
    One = 1,
    Two,
    Three
}

function ruDice(dice: Dice) {
    switch (dice) {
        case Dice.One:
            return "один";
        case Dice.Two:
            return "два";
        case Dice.Three:
            return "три";
        default:
            const n: never = dice; // паттерн, если не реализуем все случаи из енама то попадем в дефолт, где нельзя так пирсваивать
    }
}

```

## Tuples
```ts
const tuple: [number, string, number] = [1, 'a', 2];
tuple.push(1);
// console.log(tuple[3]);  error

```

## Generics
```ts
function logTime<T>(num: T): T {
    return num;
}

logTime<number>(100);
logTime<string>("100");

function logTime2<T>(num: T): T {
    if (typeof num === "string") {
        num.toUpperCase();
    }

    return num;
}


interface MyInterface {
    transform: <T, F>(a: T) => F
}

class MyClass<T> {
    value: T;

    constructor(value: T) {
        this.value = value;
    }
}

interface TimeStamp {
    stamp: number;
}

function logTimeStamp<T extends TimeStamp>(num: T): T {
    console.log(num.stamp);
    return num;
}
```

## TSX
```ts
import React from 'react';

const a: JSX.Element = (
    <div>
        <h1>Hello world</h1>
    </div>
);
```