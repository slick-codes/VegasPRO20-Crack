
# Description

JSON validace (json-validace) is an open source schema base validator that allows developers validate json and javascript object using an object Schema.

#### Why use json-validace

There are alot of schema base validator packages out there but only a few supports nested validation, outside nested validation json-validace also has lots of useful methods, modifiers, types and many more feautures.

  

# Installation

Just like any clasic npm package you can install json-validace using npm, yarn or any other installer you prefer.

```bash
# npm
npm install --save json-validace
```

```bash
# yarn 
yarn add json-validace 
```

# Usage & example

```javascript
// Filename: validace.schema.js
const jsonValidace = require("json-validace")

// create a validace schema 
const loginSchema = new jsonValidace.Schema({
    password: {
        type: "string",
        required: true,
        minLength: 10,
        maxLength: 20
    },
    email: {
        type: "email",
        required: true
    }
})

// export loginSchema
module.exports = loginSchema
```

```javascript
// Filename: test.js
cosnt { loginSchema } = require('validace.schema.js')

    // Useage
const result = loginSchema.validate({
    email: "test@gmail.com",
    password: "slickcodes"
})

// login the result
console.log(result)
```

```bash
# Result: in ternimal | console
    {
        error: null,
        isValid: true,
        data: { email: 'test@gmail.com', password: 'slickcodes' }
    }
```

### NOTE

if you're using <strong>REACT, VUE ,Svelte, Angular </strong> or other frontend framework you'll need to import using the import keyword.

```javascript
import { Schema } from "json-validace"
```
or
```javascript
import jsonValidace from "json-validace"
```

# Types

the Type key is the only required key in the schema, it states what type of data is expected.
The type key can be parsed as a key in the schema or directly.


```js
// parse type as directly
const { Schema } = require('json-validace')

const loginSchema = new Schema({
    password: "string",
    email: "email"
})
```

```js
// parse type as a key 
const { Schema } = require('json-validace')

const loginSchema = new Schema({
    password:  { type: "string" },
    email: { type: "email" }
})
```

while declearing type directly can be simpler and easier to read, it doesnt allow you to parse in other keys, which is why it's good to set type as a key.

if the value parsed to the valdate method does not meet the type requirements the returned value will be populated with a type error.

#### Example of a type error

```javascript
const { Schema } = require('json-validace')

const loginSchema = new Schema({
    password: { type: "string" },
    email: { type: "email" }
})

// validate the login object
const validate = loginSchema.validate({
    email: "slickcodes@mail",
    password: 59489483
})

console.log(validate)
```

```bash
# BASH : result
{
  error: {
    password: { type: ' "password" value is not a string' },
    email: { type: ' "email" value is not a email' }
  },
  isValid: false,
  data: null
}

```

To prevent error message like the one above we'll need to parse in the correct type.

### Available types

| S/N | Types  | Example        | Description                         |
|-----|--------|----------------|-------------------------------------|
| 1   | string  | Hello Word       |  this is any sequence of character
| 2   | email   | test@gmail.com   | email is a sub-type of string, it detects if the parsed value is a valid email address
| 3   | number  | 59               | the number type checks if the parsed value is a valid number, NOTE: floats and any falsy or truty data are also considered as valid number.
| 4   | float   | 49.5             | floats is a sub-type of number and it checks if the value parsed in is a valid floating point number.
| 5   | boolean | true             | boolean is type checks if the parsed data is a valid boolean value, a good example can be using true, false or an expression like 59 > 3
| 6   | date    | 1997-10-17       | date is a sub-type of string and it checks if the parsed data is a valid date type, it uses the YYYY-MM-DD configuration and it will work with any javascript date object like the date number (1671987916618) or (2022-12-25T17:05:33.957Z)
| 7   | array   | ["Paul", "Mike"] | array checks if the parsed in value is a valid array, depending on your schema you can also validate the value if the array is an array of object.
| 8   | object  | {author: "Paul"} | object type check if the data parsed is a valid object literal
| 9   | jwt     |  eyJhbGciOiJIUzI1NiIsInR5c<br>CI6IkpXVCJ9.eyJzdWIiOiI<br>xMjM0NTY3ODkwIiwibmFtZSI6 <br> IkpvaG4gRG9lIiwiaWF0Ij<br>oxNTE2MjM5MDIyfQ<br>.SflKxwRJSMeKKF2QT4fwp<br>MeJf36POk6yJV_adQssw5c                 | JWT (JSON Web Token) is a sub-type of string and it checks if the parsed string meets the jwt standard.
| 10  | mongoid | 507f191e810c19729de860ea | the mongoId type is a sub-type of string and it checks if the string provided is a valid mongoID.

# More Doc coming soon
