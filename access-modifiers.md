# Access Modifiers in TypeScript

## Introduction

When I write a class, not everything inside it should be open to everyone. Access modifiers let me decide who can use a property or a method. TypeScript has four: public, private, protected and readonly.

## How they work

**public**: everyone can access it. This is the default.

```ts
class Employee {
  public id: number = 1;
}

new Employee().id; // works
```

**private**: only the class itself can access it.

```ts
class Employee {
  private baseSalary: number = 50000;
}

new Employee().baseSalary; // error
```

**protected**: the class and its child classes can access it, but code outside cannot.

```ts
class Employee {
  protected name: string = "Alice";
}

class Manager extends Employee {
  getName(): string {
    return this.name; // works
  }
}

new Employee().name; // error
```

**readonly**: it can be read, but not changed after the constructor sets it.

```ts
class Employee {
  readonly company: string = "Acme";
}

new Employee().company = "Beta"; // error
```

## Conclusion

Access modifiers keep my data safe by limiting who can reach it. I try to pick the strictest one that still lets my code work.
