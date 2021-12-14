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

let's add a `src` folder which will contain all of the typescript files and make it as `Root Directory` in `tsconfig.json` file When **TypeScript** compiles files, it keeps the same directory structure in the output directory as exists in the input directory.

For example, let’s say you have some input files:

MyProj
├── tsconfig.json
├── src
│   ├── a.ts
│   ├── b.ts
│   ├── sub
│   │   ├── c.ts
├── types.d.ts

The inferred value for `rootDir` is the longest common path of all non-declaration input files, which in this case is `src/`.

If your `outDir` was `dist`, TypeScript would write this tree:

MyProj
├── dist
│   ├── a.js
│   ├── b.js
│   ├── sub
│   │   ├── c.js

🔗 [Read more from documentation](https://www.typescriptlang.org/tsconfig#rootDir)

## Variables and Values

### Variable Declarations & Inference

In JavaScript we declare variables all the time with `let` and `const` like this:

```ts 
let name = 'Younes'
```

As we can see, TypeScript is able to [infer](https://www.typescriptlang.org/docs/handbook/type-inference.html) that `name` is a **string**, based on the
fact that we're initializing it with a value _as we are declaring it_.

If we try to give `name` a value that is _incompatible_ with `string`, we get an error

```ts 
let name = 'Younes'
name = 1
```

**In TypeScript, variables are "born" with their types.** Although
there are ways of making them more specific in certain branches of code,
there's no (safe) way of changing `name`'s type from `string` to `number`.

Let's try the same thing with `const`:

```ts 
const name = 'Younes'
```

Notice that the type of this variable is not `string`, it's `'Younes'`. **TS is able to make
a more specific assumption here**, because:

- `const` variable declarations cannot be reassigned
- the initial value assigned to `name` is a string, which is an **immutable value type**

Therefore, `name` will always be `'Younes'` in this program.


### Literal Types

The type `'Younes'` is called a **literal type**. If our `let` declaration is a variable
that can hold any `string`, the `const` declaration is one that can hold only `'Younes'` --
a specific number.

## Implicit `any` and type annotations

Sometimes, we need to declare a variable before it gets initialized, like `name` below:

```ts
let name //=> type of any
```

`name` is "born" without a type, so it ends up being an implicit `any`.


TypeScript doesn't have enough information around the declaration site to infer
what `name` should be, so it gets **the most flexible type: `any`**.

Think of `any` as "the normal way JS variables work", in that you could assign
`name` to a `number`, then later a `function`, then a `string`.

If we wanted more safety here, we could add a **type annotation**:

```ts 
let name: string
name = 12
```

Now, TypeScript will correctly alert us when we try to flip flop between the number `12` and a `string`.


## Function arguments and return values

The syntax we've just seen for variable type annotations can also be used
to describe function arguments and return values. In this example it's not clear,
even from the implementation of the function, whether `add` should accept numbers or strings.

```ts 
// @noImplicitAny: false
function add(a, b) {
  return a + b // strings? numbers? a mix?
}
```

Here's what your in-editor tooltip would look like if you were using this function:

```ts twoslash
// @noImplicitAny: false
function add(a, b) {
  return a + b
}
const result = add(3, "4")
result
```

Without type annotations, "anything goes" for the arguments passed into `add`. Why is this a problem?

```ts 
// @noImplicitAny: false
function add(a, b) {
  return a + b
}
/// ---cut---
const result = add(3, "4")
const p = new Promise(result)
```

If you've ever created a `Promise` using the promise constructor, you may see
that we are using a `string` where we _should_ use a two-argument function. This
is the kind of thing we'd hope that TypeScript could catch for us.

Without type annotations, "anything goes" for the arguments passed into `add`. Why is this a problem?

Let's add some type annotations to our function's arguments:

```ts
function add(a: number, b: number) {
  return a + b
}
const result = add(3, "4")
```

Great, now we can enforce that only values of type `number` are passed into the function,
and TS can now determine the return type automatically:

```ts 
function add(a: number, b: number) {
  return a + b
}
const result = add(3, 4)
//              ^?
```

If we wanted to specifically state a return type, we could do so using the `:foo` syntax in one more place

```ts 
function add(a: number, b: number): number {}
```

This is a great way for code authors to state their intentions up-front. TypeScript will make sure
that we live up to this intention, and errors will be surfaced _at the location of the function declaration_
instead of _where we use the value returned by the function_.