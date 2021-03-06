# TypeScript Style Guide

This is the TypeScript style guide that we use internally at Platypi! It is *semi-reasonable*, but it's more important that we keep a consistent look/feel of our code.


## Table of Contents

  0. [Browser Compatibility](#browser-compatibility)
  0. [Files](#files)
  0. [Indentation](#indentation)
  0. [Line Length](#line-length)
  0. [Quotes](#quotes)
  0. [Comments](#comments)
    0. [Class](#class)
    0. [Inline](#inline)
    0. [Todo and XXX](#todo-and-xxx)
  0. [Variable Declarations](#variable-declarations)
  0. [Function Declarations](#function-declarations)
    0. [Anonymous Functions](#anonymous-functions)
  0. [Names](#names)
    0. [Variables, Modules, and Functions](#variables-modules-and-functions)
    0. [Use of var, let, and const](#use-of-var-let-and-const)
    0. [Types](#types)
    0. [Classes](#classes)
    0. [Enumerations](#enumerations)    
    0. [Interfaces](#interfaces)
    0. [Constants](#constants)
  0. [Statements](#statements)
    0. [Simple](#simple)
    0. [Compound](#compound)
    0. [Return](#return)
    0. [If](#if)
    0. [For](#for)
    0. [While](#while)
    0. [Do While](#do-while)
    0. [Switch](#switch)
    0. [Try](#try)
    0. [Continue](#continue)
    0. [Throw](#throw)
  0. [Whitespace](#whitespace)
  0. [Object and Array Literals](#object-and-array-literals)
  0. [Assignment Expressions](#assignment-expressions)
  0. [Typings](#assignment-expressions)
    0. [External](#external)
    0. [Internal](#internal)
  0. [Imports and Exports](#imports-and-exports)
  0. [null and undefined](#null-and-undefined)
  0. [General Assumptions](#general-assumptions)
  0. [Asserts](#asserts)
  0. [=== and !== Operators](#===-and-!==-Operators)
  0. [Eval](#eval)
  0. [TSLint](#tslint)
  0. [License](#license)

**[top](#table-of-contents)**

## Browser Compatibility
  - Target evergreen browsers `ie >= 11`
  - Target modern browsers `ie >= 10` if it is necessary for a project
  - Avoid targeting older browsers `ie < 9` if at all possible

**[top](#table-of-contents)**

## Files
  - All TypeScript files must have a ".ts" extension.
  - They should be all camelCase case, and only include letters and numbers.
  - 1 file per logical component (e.g. parser, scanner, emitter, checker).
  - **All files should end in a new line.** This is necessary for some Unix systems.

**[top](#table-of-contents)**

## Indentation
  - The unit of indentation is four spaces.
  - **Never use tabs**, as this can lead to trouble when opening files in different IDEs/Text editors. Most text editors have a configuration option to change tabs to spaces.

**[top](#table-of-contents)**

## Line Length
  - Lines must not be longer than 200 characters.
  - When a statement runs over 200 characters on a line, it should be broken up, ideally after a comma or operator.

**[top](#table-of-contents)**

## Quotes
  - Use single-quotes `''` for all strings, and use double-quotes `""` for strings within strings.

  ```typescript
  // bad
  let greeting = "Hello World!";

  // good
  let greeting = 'Hello World!';

  // bad
  let html = "<div class='bold'>Hello World</div>";

  // bad
  let html = '<div class=\'bold\'>Hello World</div>';

  // good
  let html = '<div class="bold">Hello World</div>';
  ```

**[top](#table-of-contents)**

## Comments
  - Comments are strongly encouraged. It is very useful to be able to read comments and understand the intentions of a given block of code.
  - Comments need to be clear, just like the code they are annotating.
  - Make sure your comments are meaningful.

The following example is a case where a comment is completely erroneous, and can actually make the code harder to read.

  ```typescript
  // Set index to zero.
  let index = 0;
  ```

  - All public functions must have a comment block `/**...*/` using [JSDoc](http://usejsdoc.org/) style comments.

JSDocs can be interpreted by IDEs for better intellisense. Below is an example of a JSDoc comment block for a function.

  ```typescript
  /**
   * Takes in a name and returns a greeting string.
   * @param {string} name The name of the greeted person.
   * @returns {string} Greeting string.
   */
  function getGreeting(name: string): string {
      return 'Hello ' + name + '!';
  }
  ```

### Class

  - All classes must have block comments `/**...*/` for all public variables and functions.
  - All public functions should use [JSDoc](http://usejsdoc.org/) style comments.
  - Functions need to have a comment explaining what the function does, and all of the input parameters need to be annotated with `@param`.
  - The class should include a block comment containing the description of the class.
  - The constructor should contain a JSDoc comment annotating any input parameters.

  ```typescript
  /**
   * Contains properties of a Person.
   */
  class Person {
      /**
       * Returns a new Person with the specified name.
       * @param {string} name The name of the new Person.
       * @returns {Person} A new person.
       */
      static GetPerson(name: string): Person {
          return new Person(name);
      }

      /**
       * @param {string} name The name of the new Person.
       */
      constructor(public name: string) { }

      /**
       * Instructs this Person to walk for a certain amount
       * of time.
       * @param {number} millis - The number of milliseconds the Person
       * should walk.
       */
      walkFor(millis: number): void {
          console.log(this.name + ' is now walking.');

          setTimeout(() => {
              console.log(this.name + ' has stopped walking.');
          }, millis);
      }
  }
  ```

**[top](#table-of-contents)**

### Inline

  - Inline comments are comments inside of complex statements (loops, functions, etc).
  - Use `//` for all inline comments.
  - Keep comments clear and concise.
  - Place inline comments on a newline above the line they are annotating
  - Put an empty line before the comment.

  ```typescript
  // bad
  let lines: Array<string>; // Holds all the lines in the file.

  // good
  // Holds all the lines in the file.
  let lines: Array<string>;

  // bad
  function walkFor(name: string, millis: number): void {
      console.log(name + ' is now walking.');
      // Wait for millis milliseconds to stop walking
      setTimeout(() => {
          console.log(name + ' has stopped walking.');
      }, millis);
  }

  // good
  function walkFor(name: string, millis: number): void {
      console.log(name + ' is now walking.');

      // Wait for millis milliseconds to stop walking
      setTimeout(() => {
          console.log(name + ' has stopped walking.');
      }, millis);
  }
  ```

**[top](#table-of-contents)**

### Todo and XXX

`TODO` and `XXX` annotations help you quickly find things that need to be fixed/implemented.

  - Use `// TODO:` to annotate solutions that need to be implemented.
  - Use `// XXX:` to annotate problems the need to be fixed.
  - It is best to write code that doesn't need `TODO` and `XXX` annotations, but sometimes it is unavoidable.

**[top](#table-of-contents)**

## Variable Declarations

  - All variables must be declared prior to using them. This aids in code readability and helps prevent undeclared variables from being hoisted onto the global scope.

  ```typescript
  // bad
  console.log(a + b);

  let a = 2,
  let b = 4;

  // good
  let a = 2,
  let b = 4;

  console.log(a + b);
  ```

  - Implied global variables should never be used.
  - You should never define a variable on the global scope from within a smaller scope.

  ```typescript
  // bad
  function add(a: number, b: number): number {
      // c is on the global scope!
      c = 6;

      return a + b + c;
  }
  ```

  - Use one `let` keyword to define a block of variables.
  - Declare each variable on a newline with own let statement.

  ```typescript
  // bad
  let a = 2;
      b = 2;
      c = 4;

  // good
  let a = 2,
  let b = 2,
  let c = 4;

  // bad
  // b will be defined on global scope.
  let a = b = 2, c = 4;
  ```
  
**[top](#table-of-contents)**

## Function Declarations

  - All functions must be declared before they are used.
  - Any closure functions should be defined right after the let declarations.

  ```typescript
  // bad
  function createGreeting(name: string): string {
      let message = 'Hello ';

      return greet;

      function greet() {
          return message + name + '!';
      }
  }

  // good
  function createGreeting(name: string): string {
      let message = 'Hello ';

      function greet() {
          return message + name + '!';
      }

      return greet;
  }
  ```

  - There should be no space between the name of the function and the left parenthesis `(` of its parameter list.
  - There should be one space between the right parenthesis `)` and the left curly `{` brace that begins the statement body.

  ```typescript
  // bad
  function foo (){
      // ...
  }

  // good
  function foo() {
      // ...
  }
  ```

  - The body of the function should be indented 4 spaces.
  - The right curly brace `}` should be on a new line.
  - The right curly brace `}` should be aligned with the line containing the left curly brace `{` that begins the function statement.

  ```typescript
  // bad
  function foo(): string {
    return 'foo';}

  // good
  function foo(): string {
      return 'foo';
  }
  ```

  - For each function parameter
    - There should be no space between the parameter and the colon `:` indicating the type declaration.
    - There should be a space between the colon `:` and the type declaration.

  ```typescript
  // bad
  function greet(name:string) {
    // ...
  }

  // good
  function greet(name: string) {
    // ...
  }
  ```

**[top](#table-of-contents)**

### Anonymous Functions

  - All anonymous functions should be defined as fat-arrow/lambda `() => { }` functions unless it is absolutely necessary to preserve the context in the function body.
  - All fat-arrow/lambda functions should have parenthesis `()` around the function parameters.

  ```typescript
  // bad
  clickAlert() {
      let element = document.querySelector('div');

      this.foo = 'foo';

      element.addEventListener('click', function(event: Event) {
          // this.foo does not exist!
          alert(this.foo);
      });
  }

  // good
  clickAlert() {
      let element = document.querySelector('div');

      this.foo = 'foo';

      element.addEventListener('click', (event: Event) => {
          // TypeScript allows this.foo to exist!
          alert(this.foo);
      });
  }
  ```

  - There should be a space between the right parenthesis `)` and the `=>`
  - There should be a space between the `=>` and the left curly brace `{` that begins the statement body.

  ```typescript
  // bad
  element.addEventListener('click', (event: Event)=>{alert('foo');});

  // good
  element.addEventListener('click', (event: Event) => {
      alert('foo');
  });
  ```

  - The statement body should be indented 4 spaces.
  - The right curly brace `}` should be on a new line.
  - The right curly brace `}` should be aligned with the line containing the  left curly brace `{` that begins the function statement.

**[top](#table-of-contents)**

## Names

  - All variable and function names should be formed with alphanumeric `A-Z, a-z, 0-9` charcters using lowerCamelCase or UpperCamelCase notiation.
  - Use whole words in names when possible.

### Variables, Modules, and Functions

  - Variable, module, and function names should use lowerCamelCase.
  
#### Boolean

  - Use semantic prefixes for boolean variables and properties (e.g. is-, has-, was-, ...).
  
  ```typescript
  // bad
  let validPerson: boolean = person.valid();
  
  // good
  let isValidPerson: boolean = person.isValid();
  ```
  
  
### Use of var, let, and const

  - Use `const` where appropriate, for values that should never change
  - Use `let` everywhere else
  - Avoid using `var`

**[top](#table-of-contents)**

### Types

  - Always favor type inference over explicit type declaration except for function return types
  - Always define the return type of functions.
  - Always specify variable type.
  - Arrays should be defined as `type[]` instead of `Array<type>`.
  - Use the `any` type sparingly, it is always better to define an interface.

  ```typescript
  // bad
  let numbers = [];

  // bad
  let numbers: Array<number> = [];

  // good
  let numbers: number[] = [];
  ```

**[top](#table-of-contents)**

### Classes

  - Classes/Constructors functions should use UpperCamelCase (PascalCase).
  - `Private` and `private static` members in classes should be denoted with the `private` keyword.
  - `Protected`  members in classes should be denoted with the `protected` keyword.
  - Use `public` instance members only when they are used by other parts of the application.
  - Use lowerCamelCase for all fields, properties and methods names (Don't use "_"  as a prefix for private properties).

  ```typescript
  class Person {
      private fullName: string;
      public firstName: string;
      public lastName: string;

      constructor(firstName: string, lastName: string) {
          this.firstName = firstName;
          this.lastName = lastName;
          this.fullName = firstName + ' ' + lastName;
      }

      public toString(): string {
          return this.fullName;
      }

      public walkFor(millis: number): void {
          console.log(this.fullName + ' is now walking.');

          // Wait for millis milliseconds to stop walking
          setTimeout(() => {
              console.log(this.fullName + ' has stopped walking.');
          }, millis);
      }
  }
  ```
    - Don't use parameter properties.
    
  ```typescript
  // bad
  class Person {
      constructor(public firstName: string, public lastName: string) {
      }
  }
  
  // good
  class Person {
      public firstName: string;
      public lastName: string;

      constructor(firstName: string, lastName: string) {
          this.firstName = firstName;
          this.lastName = lastName;
      }
  }
  ```    
  
  - Use following order for class members:
  0. public fields.
  0. private fields.
  0. constructor.
  0. public methods.
  0. private methods.
  
  ```typescript
  class Person {
      public firstName: string;
      public lastName: string;

      private age: number;

      constructor(firstName: string, lastName: string, age: number) {
          this.firstName = firstName;
          this.lastName = lastName;
          this.age = age;
      }
      
      public sayGreetings(): string {
        var greetings: string = 'Hello, ' + this.getFullName();
        return greetings;
      }
      
      private getFullName(): string {
        var fullName: string = this.firstName + ' ' + this.lastName;
        return fullName;
      }
  }

**[top](#table-of-contents)**

### Enumerations

  - Use class with static fields for enumerations.

  ```typescript
  export class Gender {
    public static male: number = 0;
    public static female: number = 1;
  }
  ``` 

**[top](#table-of-contents)**

### Interfaces

  - Interfaces should use UpperCamelCase.
  - Interfaces should be prefaced with the capital letter I.
  - Only `public` members should be in an interface, leave out `protected` and `private` members.

  ```typescript
  interface IPerson {
      firstName: string;
      lastName: string;
      toString(): string;
  }
  ```

**[top](#table-of-contents)**

### Constants

  - All constants should use lowerCamelCase.
  - All constants you be defined with the `const` keyword.

**[top](#table-of-contents)**

## Statements

### Simple

  - Each line should contain at most one statement.
  - A semicolon should be placed at the end of every simple statement.

  ```typescript
  // bad
  let greeting: string = 'Hello World'

  alert(greeting)

  // good
  let greeting: string = 'Hello World';

  alert(greeting);
  ```

**[top](#table-of-contents)**

### Compound

Compound statements are statements containing lists of statements enclosed in curly braces `{}`.

  - The enclosed statements should start on a newline.
  - The enclosed statements should be indented 4 spaces.

  ```typescript
  // bad
  if (condition === true) { alert('Passed!'); }

  // good
  if (condition === true) {
      alert('Passed!');
  }
  ```
  - The left curly brace `{` should be at the end of the line that begins the compound statement.
  - The right curly brace `}` should begin a line and be indented to align with the line containing the left curly brace `{`.

  ```typescript
  // bad
  if (condition === true)
  {
      alert('Passed!');
  }

  // good
  if (condition === true) {
      alert('Passed!');
  }
  ```

  - **Braces `{}` must be used around all compound statements** even if they are only single-line statements.

  ```typescript
  // bad
  if (condition === true) alert('Passed!');

  // bad
  if (condition === true)
      alert('Passed!');

  // good
  if (condition === true) {
      alert('Passed!');
  }
  ```

If you do not add braces `{}` around compound statements, it makes it very easy to accidentally introduce bugs.

  ```typescript
  if (condition === true)
      alert('Passed!');
      return condition;
  ```

It appears the intention of the above code is to return if `condition === true`, but without braces `{}` the return statement will be executed regardless of the condition.

  - Compount statements do not need to end in a semicolon `;` with the exception of a `do { } while();` statement.

**[top](#table-of-contents)**

### Return

  - If a `return` statement has a value you should not use parenthesis `()` around the value.
  - Avoid of returning statements. If you need to return statement - assign statement to the new variable and return it.
  - The return value expression must start on the same line as the `return` keyword.

  ```typescript
  // bad
  return
      'Hello, ' + this.fullName + '!';

  // bad
  return ('Hello, ' + this.fullName + '!');

  // good
  let greeting: string = 'Hello, ' + this.fullName + '!';
  return greeting;
  ```

  - It is recommended to take a return-first approach whenever possible.

  ```typescript
  // bad
  function getHighestNumber(a: number, b: number): number {
      let out: number = b;

      if(a >= b) {
          out = a;
      }

      return out;
  }

  // good
  function getHighestNumber(a: number, b: number): number {
      if(a >= b) {
          return a;
      }

      return b;
  }
  ```

  - Always **explicitly define a return type**. This can help TypeScript validate that you are always returning something that matches the correct type.

  ```typescript
  // bad
  function getPerson(name: string) {
      var person: Person = new Person(name);
      return person;
  }

  // good
  function getPerson(name: string): Person {
      var person: Person = new Person(name);
      return person;
  }
  ```

**[top](#table-of-contents)**

### If

  - Alway be explicit in your `if` statement conditions.

  ```typescript
  // bad
  function isString(str: any) {
      return !!str;
  }

  // good
  function isString(str: any) {
      let result: boolean = (typeof str === 'string');
      return result;
  }
  ```

Sometimes simply checking falsy/truthy values is fine, but the general approach is to be explicit with what you are looking for. This can prevent a lot of unncessary bugs.

If statements should take the following form:

  ```typescript
  if (/* condition */) {
      // ...
  }

  if (/* condition */) {
      // ...
  } else {
      // ...
  }

  if (/* condition */) {
      // ...
  } else if (/* condition */) {
      // ...
  } else {
      // ...
  }
  ```

**[top](#table-of-contents)**

### For

For statements should have the following form:

  ```typescript
  for(/* initialization */; /* condition */; /* update */) {
      // ...
  }

  let keys: string[] = Object.keys(/* object */),
  let length = keys.length;

  for(let i: number = 0; i < length; i++) {
      // ...
  }
  ```

Object.prototype.keys is supported in `ie >= 9`.

  - Use _.keys() in lieu of a `for...in` statement.

**[top](#table-of-contents)**

### While

While statements should have the following form:

  ```typescript
  while (/* condition */) {
      // ...
  }
  ```

**[top](#table-of-contents)**

### Do While

  - Do while statements should be avoided unless absolutely necessary to maintain consistency.
  - Do while statements must end with a semicolon `;`

Do while statements should have to following form:

  ```typescript
  do {
      // ...
  } while (/* condition */);
  ```

**[top](#table-of-contents)**

### Switch

Switch statements should have the following form:

  ```typescript
  switch (/* expression */) {
      case /* expression */:
          // ...
          /* termination */
      default:
          // ...
  }
  ```

  - Each switch group except default should end with `break`, `return`, or `throw`.

**[top](#table-of-contents)**

### Try

  - Try statements should be avoided whenever possible. They are not a good way of providing flow control.

Try statements should have the following form:

  ```typescript
  try {
      // ...
  } catch (error: Error) {
      // ...
  }

  try {
      // ...
  } catch (error: Error) {
      // ...
  } finally {
      // ...
  }
  ```

**[top](#table-of-contents)**

### Continue

  - It is recommended to take a continue-first approach in all loops.

**[top](#table-of-contents)**

### Throw

  - Avoid the use of the throw statement unless absolutely necessary.
  - Flow control through try/catch exception handling is not recommended.

**[top](#table-of-contents)**

## Whitespace

Blank lines improve code readability by allowing the developer to logically group code blocks. Blank spaces should be used in the following circumstances.

  - A keyword followed by left parenthesis `(` should be separated by 1 space.

  ```typescript
  // bad
  if(condition) {
      // ...
  }

  // good
  if (condition) {
      // ...
  }
  ```

  - All operators except for period `.`, left parenthesis `(`, and left bracket `[` should be separated from their operands by a space.

  ```typescript
  // bad
  let sum: number = a+b;

  // good
  let sum: number = a + b;

  // bad
  let name: string = person . name;

  // good
  let name: string = person.name;

  // bad
  let item: number = items [4];

  // good
  let item: number = items[4];
  ```

  - No space should separate a unary/incremental operator `!x, -x, +x, ~x, ++x, --x` and its operand.

  ```typescript
  // bad
  let negative: number = - a;

  // good
  let negative: number = -a;
  ```

  - Each semicolon `;` in the control part of a `for` statement should be followed with a space.

  ```typescript
  // bad
  for(let i: number = 0;i < 10;i++) {
      // ...
  }

  // good
  for(let i: number = 0; i < 10; i++) {
      // ...
  }
  ```

**[top](#table-of-contents)**

## Object and Array Literals

  - Use curly braces `{}` instead of `new Object()`.
  - Use brackets `[]` instead of `new Array()`.

**[top](#table-of-contents)**

## Assignment Expressions

  - Assignment expressions inside of the condition block of `if`, `while`, and `do while` statements should be avoided.

  ```typescript
  // bad
  while (node = node.next) {
      // ...
  }

  // good
  while (typeof node === 'object') {
      node = node.next;

      // ...
  }
  ```

**[top](#table-of-contents)**

## Typings

### External

  - Use [tsd](http://definitelytyped.org/tsd/) for all external library declarations
  - Actively add/update/contribute typings to [DefinitelyTyped](http://definitelytyped.org/) when they are missing

### Internal

  - Create declaration files `.d.ts` for your interfaces instead of putting them in your `.ts` files
  - Let the TypeScript compiler infer as much as possible
  - Always define types.

  ```typescript
  // bad
  let a = 2;

  // good
  let a: number = 2;
  ```

  - Always define the return type of functions, this helps to make sure that functions always return the correct type

  ```typescript
  // bad
  function sum(a: number, b: number) {
      var result: number =  a + b;
      return result;
  }

  // good
  function sum(a: number, b: number): number {
      var result: number =  a + b;
      return result;
  }
  ```

**[top](#table-of-contents)**

## Imports and Exports

  - Use ES6 import notation for all imports.
  - Use relative paths for non-libary dependencies in imports.
  - Declare all imports at the beginning of the file.
  - Don't use `export default` statement.

  ```typescript
    // bad
    import { Entity } from '/app/common/models/entity';
  
    // good
    import { Entity } from './entity';
    import * as _ from 'lodash';
  ```

**[top](#table-of-contents)**

## null and undefined

  - Use `undefined`, do not use `null`.

**[top](#table-of-contents)**

## General Assumptions

  - Consider objects like Nodes, Symbols, etc. as immutable outside the component that created them. Do not change them.
  - Consider arrays as immutable by default after creation.

**[top](#table-of-contents)**

## Asserts

  - Use Asserts for all methods/functions parameters that cannot be undefined.
  ```typescript
    class UserApiService {
      constructor(httpService: HttpService) {
        Assert.isNotNull(httpService, 'httpService');
      }
    }
  ```
  

**[top](#table-of-contents)**

## === and !== Operators

  - It is better to use `===` and `!==` operators whenever possible.
  - `==` and `!=` operators do type coercion, which can lead to headaches when debugging code.

**[top](#table-of-contents)**

## Eval

  - **Never use eval**
  - **Never use the Function constructor**
  - **Never pass strings to `setTimeout` or `setInterval`**

**[top](#table-of-contents)**

## TSLint

  - Always use a Linter

Linting your code is very helpful for preventing minor issues that can escape the eye during development. We use TSLint (written by Palantir) for our linter.

  - TSLint: https://github.com/palantir/tslint
  - Our [tslint.json](https://github.com/Platypi/style_typescript/blob/master/tslint.json)

## License
(The MIT License)

Copyright (c) 2014 Platypi, LLC

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
