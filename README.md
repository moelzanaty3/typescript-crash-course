# Typescript Crash Course
the needed skills you need to ship to get familiar with typescript 

## TypeScript Setup

you can open your terminal and install typescript globally in your machine via 
```shell
npm install -g typescript
```
and you will be able to find it's version via `tsc --version` but as mention in [official website for 
typescript](https://www.typescriptlang.org/download) 

> Having TypeScript set up on a per-project basis lets you have many projects with many different versions of TypeScript, this keeps each project working consistently.

so now we will install it via npm TypeScript is available as a [package](https://www.npmjs.com/package/typescript) on the npm registry available as `typescript`.

You will need a copy of [Node.js](https://nodejs.org/en/) as an environment to run the package. Then you use a dependency manager like [npm](https://www.npmjs.com/), [yarn](https://yarnpkg.com/) to download TypeScript into your project.

```shell
npm install typescript --save-dev
# or 
yarn add typescript --dev
```

🎭 © [typescriptlang.org](https://www.typescriptlang.org/download)

## TSC && tsconfig.json

Typically the first step in any new TypeScript project is to add a `tsconfig.json` file. A `tsconfig.json` file defines the TypeScript [project settings](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html), such as the compiler options and the files that should be included. 

To do this, open up the folder where you want to store your source and add a new file named `tsconfig.json`.

A simple `tsconfig.json` looks like this for ES5, [CommonJS](http://www.commonjs.org/specs/modules/1.0) modules and source maps:

```json 
{
  "compilerOptions": {
    "target": "es5", // es6
    "module": "commonjs"
  }
}
```
Now when you create a `.ts` file as part of the project we will offer up rich editing experiences and syntax validation.

Let's walk through **transpiling a simple TypeScript Hello World program.**  

1- Create a` index.ts` file, place the following code in that file...

```ts 
let message: string = 'Hello World';
console.log(message);
```

open a terminal and type `tsc index.ts`. You should now see the transpiled `index.js` JavaScript file, which you can run if you have [Node.js](https://nodejs.org/) installed, by typing `node index.js`.

🎭 © [code.visualstudio.com](https://code.visualstudio.com/docs/typescript/typescript-compiling)

## Folder Structure

comming soon!

## Basic Types

comming soon!

## Arrays & Tuples

comming soon!

## Unions & Enum

comming soon!

## Objects

comming soon!

## Type Assertion

comming soon!

## Functions

comming soon!

## Interfaces

comming soon!

## Function Interface

comming soon!

## Classes

comming soon!

## Data Modifiers

comming soon!

## Implement Interface in Class

comming soon!

## Extending Classes (Subclasses)

comming soon!

## Generics

comming soon!
