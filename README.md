# ts-ps Blog
### The differences among any, unknown, and never Types in TypeScript:

These are special types in TypeScript. Let’s understand them one by one.

**any:**
* Anything can be stored in it.
* TypeScript won’t check it for errors - not safe.

```ts
let data: any = 10;
data = "hello";
data(); // No compile-time error, but will crash at runtime
```

**unknown:**
* Anything can be stored in it also.
* But one must check the type before using it.

```ts
let info: unknown = "hello";

if (typeof info === "string") { // Safe to use String methods now
  console.log(info.toUpperCase());
}
```

**never:**
* Used when something should never happen.
* For example, a function that always throws an error.

```ts
function crash(): never {
  throw new Error("This always fails");
}
```


### Examples of Union (|) and Intersection (&) types in TypeScript:

**Union Types:**
* Union types allow a value to be one of several types.

```ts
function handleInput(input: string | number | boolean) {
  if (typeof input === "string") {
    console.log("String input:", input.toUpperCase());
  } else if (typeof input === "number") {
    console.log("Number input:", input * 2);
  } else {
    console.log("Boolean input:", input ? "Yes" : "No");
  }
}

handleInput("admin");  // Output: String input: ADMIN
handleInput(42);       // Output: Number input: 84
handleInput(true);     // Output: Boolean input: Yes
```

**Intersection Types:**
* The final type object must have all the properties from the combined types.

```ts
type ContactInfo = { email: string; phone: string };
type AccountInfo = { username: string; password: string };
type Preferences = { darkMode: boolean };

type UserProfile = ContactInfo & AccountInfo & Preferences;

const user: UserProfile = {
  email: "user@example.com",
  phone: "1234567890",
  username: "user01",
  password: "securePass123",
  darkMode: true
};
```