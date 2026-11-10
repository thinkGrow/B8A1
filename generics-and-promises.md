# Generics and Promise<T> in TypeScript

## Introduction

Sometimes I want one function or type to work with many different types, without losing type safety. Generics do that. A generic is a placeholder for a type, and the real type is filled in when I use it.

## How generics work

The `<T>` below is the placeholder.

```ts
const wrapInArray = <T>(value: T): T[] => {
  return [value];
};

const names = wrapInArray<string>("Mir"); // string[]
const ages = wrapInArray<number>(25); // number[]
```

In the first call `T` becomes `string`, and in the second it becomes `number`. TypeScript always knows what comes out. Types can be generic too:

```ts
interface ApiResponse<T> {
  data: T;
  success: boolean;
}

interface User {
  name: string;
  role: string;
}
```

`ApiResponse<User>` means a response whose `data` is a `User`.

## Generics and Promise<T>

An async function always gives back a Promise. `Promise<T>` tells TypeScript what the promise holds when it finishes. In my assignment, `validateAgeAsync` returns a `Promise<string>`:

```ts
const validateAgeAsync = (age: number): Promise<string> => {
  return new Promise((resolve, reject) => {
    if (age >= 18) {
      setTimeout(() => resolve("Access Granted"), 1000);
    } else {
      reject(new Error("Access Denied: Must be 18 or older"));
    }
  });
};

validateAgeAsync(20).then((message) => message.toUpperCase()); // message is a string
```

Here `T` is `string`, so `resolve` only accepts a string and `message` is known to be a string. If I wrote `resolve(123)`, TypeScript would show an error.

## Conclusion

Generics let me write code once and reuse it for many types. With `Promise<T>`, they tell me exactly what my async data looks like.
