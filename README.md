# Type vs Interface in TypeScript: What's the Difference?

There are a few key differences between **interface** and **type alias** in TypeScript. While they often serve similar purposes, they have some distinct features and use cases.

---

## 1. Extending

**Interface:**
We can easily extend another interface using the `extends` keyword.

```ts
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}
```

**Type Alias:**
We can also extend a type alias, but in a different way using intersections (`&`).

```ts
type Animal = {
  name: string;
};

type Dog = Animal & {
  breed: string;
};
```

---

## 2. Declaration Merging

**Interface:**
If we declare the same interface multiple times, TypeScript will merge them into one.

```ts
interface User {
  name: string;
}

interface User {
  age: number;
}

// Merged as: { name: string; age: number }
```

**Type Alias:**
Type aliases cannot be declared multiple times with the same name.

```ts
type User = {
  name: string;
};

//  Error: Duplicate identifier
// type User = { age: number };
```

---

## 3. Use Cases

* **Interface** is used mainly to define the **structure of an object**.
* **Type Alias** is more flexible. It can define:

  * Union types: `"success" | "error"`
  * Intersection types: `TypeA & TypeB`
  * Tuples: `[number, string]`
  * Literal values and objects

---

## 4. Flexibility & Usage

* **Type Alias** is very flexible and beneficial when creating complex custom types.
* **Interface** is commonly used with class-based structures and when designing consistent object models.

---

## Summary Table

| Feature               | Interface | Type Alias  |
| --------------------- | ----------- | ------------- |
| Extending             | Yes         | Yes (via `&`) |
| Declaration Merging   | Yes         | No            |
| Object Structure      | Yes         | Yes           |
| Union & Literal Types | No          | Yes           |
| Tuples                | No          | Yes           |
| Usage with Classes    | Common      | Less Common   |

---

So, these are the key differences between **Type** and **Interface** in TypeScript.
Choose the one that best fits your use case!


<!-- --------------------- -->
# Mastering `keyof` in TypeScript: A Simple Guide with Examples

## What is `keyof`?

`keyof` is a utility keyword in TypeScript that creates a **union type** of an object's property names. Simply put, it returns the property names of an object as a type.

---

## Example

```ts
// Define a type for a person object
type Person = {
  name: string;
  age: number;
};

// Create a union type of the property names using keyof
type PersonKeys = keyof Person; // "name" | "age"
```

In this example, `PersonKeys` becomes a union of the keys in `Person`, meaning it can be either `'name'` or `'age'`.

---

## Practical Example

You can use `keyof` in generic functions to ensure type safety:

```ts
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const person = { name: "Subir", age: 70 };

const name = getProperty(person, "name"); // Output: "Subir"
const age = getProperty(person, "age");   // Output: 70
```

This ensures that you can only access properties that exist on the object, making your code safer and more predictable.

---

## Summary

* `keyof` is used to create a union of property names from a given type.
* It's commonly used in generic functions to enforce type safety.
* Makes your code cleaner, safer, and more maintainable.

---

### Happy coding with TypeScript! 🚀
