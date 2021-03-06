# TypeScript Style Guide

This is the TypeScript style guide used by Limbus Medtec. It has been forked from Platypi!


## Table of Contents

  1. [Introduction](#introduction)
  1. [Browser Compatibility](#browser-compatibility)
  1. [Files](#files)
  1. [Indentation](#indentation)
  1. [Line Length](#line-length)
  1. [Quotes](#quotes)
  1. [Comments](#comments)
    1. [Class](#class)
    1. [Inline](#inline)
    1. [Todo and XXX](#todo-and-xxx)
  1. [Variable Declarations](#variable-declarations)
  1. [Function Declarations](#function-declarations)
    1. [Anonymous Functions](#anonymous-functions)
  1. [Names](#names)
    1. [Variables, Modules, and Functions](#variables-modules-and-functions)
    1. [Types](#types)
    1. [Classes](#classes)
    1. [Interfaces](#interfaces)
    1. [Constants](#constants)
  1. [Statements](#statements)
    1. [Simple](#simple)
    1. [Compound](#compound)
    1. [Return](#return)
    1. [If](#if)
    1. [For](#for)
    1. [While](#while)
    1. [Do While](#do-while)
    1. [Switch](#switch)
    1. [Try](#try)
    1. [Continue](#continue)
    1. [Throw](#throw)
  1. [Whitespace](#whitespace)
  1. [Object and Array Literals](#object-and-array-literals)
  1. [Assignment Expressions](#assignment-expressions)
  1. [=== and !== Operators](#===-and-!==-Operators)
  1. [Eval](#eval)
  1. [TSLint](#tslint)
  1. [License](#license) 

## Introduction
When developing software as an organization, the value of the software produced is directly affected by the quality of the codebase. Consider a project that is developed over many years and handled/seen by many different people. If the project uses a consistent coding convention it is easier for new developers to read, preventing a lot of time/frustration spent figuring out the structure and characteristics of the code. For that purpose, we need to make sure we adhere to the same coding conventions across all of our products. This will not only help new developers, but it will also aid in quickly identifying potential flaws in the code, thereby reducing the brittleness of the code.

**[top](#table-of-contents)**

## Browser Compatibility
  - Target modern browsers `ie >= 9`

**[top](#table-of-contents)**

## Files
  - All TypeScript files must have a ".ts" extension.
  - They should be all UpperCamelCase (PascalCase), and only include letters, numbers, and periods.
  - All files should end in a new line. This is necessary for some Unix systems.

**[top](#table-of-contents)**

## Indentation
  - The unit of indentation is two spaces. 
  - **Never use tabs**, as this can lead to trouble when opening files in different IDEs/Text editors. Most text editors have a configuration option to change tabs to spaces.

**[top](#table-of-contents)**

## Line Length
  - Lines must not be longer than 140 characters. 
  - When a statement runs over 140 characters on a line, it should be broken up, ideally after a comma or operator.

**[top](#table-of-contents)**

## Quotes
  - Use double-quotes `""` for all strings, and use single-quotes `''` for strings within strings. This is more in line with     Java style and facilitates working between front-end and back-end.

  ```typescript
  // bad
  var greeting = 'Hello World!';
  
  // good
  var greeting = "Hello World!";
  
  // bad
  var html = '<div class="bold">Hello World</div>';
  
  // bad
  var html = "<div class=\"bold\">Hello World</div>";
  
  // good
  var html = "<div class='bold'>Hello World</div>";
  ```

**[top](#table-of-contents)**

## Comments
  - Comments are encouraged. It is very useful to be able to read comments and understand the intentions of a given block of code. 
  - Comments need to be clear, just like the code they are annotating. 
  - Make sure your comments are meaningful. 

The following example is a case where a comment is completely erroneous, and can actually make the code harder to read.

  ```typescript
  // Set index to zero.
  var index = 0;
  ```

### Class

  - On top, all class should include a block `/**...*/` comment containing the licens description.
  - Following the imports, all class should include a block `/**...*/` comment containing the description of the class and the author.

  ```typescript
  /**
 * (c) Copyright 2015, Limbus GmbH
 *
 * All rights reserved.
 */
 
 import BasePerson = require("path/to/BasePerson");

  /**
   * Contains properties of a Person.
   *
   * @author First Last
   */
  class Person extends BasePerson {
    
  }
  ```

**[top](#table-of-contents)**

### Inline

  - Inline comments are comments inside of complex statements (loops, functions, etc). 
  - Use `//` for all inline comments. 
  - Keep comments clear and concise. 
  - Place inline comments on a newline above the line they are annotating

  ```typescript
  // bad
  var lines: Array<string>; // Holds all the lines in the file.
  
  // good
  // Holds all the lines in the file.
  var lines: Array<string>;
  
  // bad
  function walkFor(name: string, millis: number) {
      console.log(name + ' is now walking.');
      // Wait for millis milliseconds to stop walking
      setTimeout(() => {
          console.log(name + ' has stopped walking.');
      }, millis);
  }
  ```

**[top](#table-of-contents)**

### Todo and FIXME

`TODO` and `FIXME` annotations help you quickly find things that need to be fixed/implemented. 

  - Use `// TODO:` to annotate solutions that need to be implemented. 
  - Use `// FIXME:` to annotate problems the need to be fixed. 
  - It is best to write code that doesn't need `TODO` and `FIXME` annotations, but sometimes it is unavoidable. 

**[top](#table-of-contents)**

## Variable Declarations

  - All variables must be declared prior to using them. This aids in code readability and helps prevent undeclared variables from being hoisted onto the global scope. 
  
  ```typescript
  // bad
  console.log(a + b);

  var a = 2;
  var b = 4;

  // good
  var a = 2;
  var b = 4;
      
  console.log(a + b);
  ```

  - Implied global variables should never be used. 
  - You should never define a variable on the global scope from within a smaller scope.
  
  ```typescript
  // bad
  function add(a: number, b: number) {
      // c is on the global scope!
      c = 6;
      
      return a + b + c;
  }
  ```

  - Use a `var` keyword for each defined variable.
  - Declare each variable on a newline.
  
  ```typescript
  // bad
  var a = 2,
      b = 2,
      c = 4;

  // good
  var a = 2;
  var b = 2;
  var c = 4;
  
  // bad
  // b will be defined on global scope.
  var a = b = 2, c = 4;
  ```

## Function Declarations

  - All functions must be declared before they are used.
  - Any closure functions should be defined right after the var declarations.

  ```typescript
  // bad
  function createGreeting(name: string): string {
      var message = 'Hello ';

      return greet;

      function greet() {
          return message + name + '!';
      }
  }
  
  // good
  function createGreeting(name: string): string {
      var message = 'Hello ';

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

  - The body of the function should be indented 2 spaces.
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
      var element = document.querySelector('div');
      
      this.foo = 'foo';
      
      element.addEventListener('click', function(ev: Event) {
          // this.foo does not exist!
          alert(this.foo);
      });
  }
  
  // good
  clickAlert() {
      var element = document.querySelector('div');
      
      this.foo = 'foo';
      
      element.addEventListener('click', (ev: Event) => {
          // TypeScript allows this.foo to exist!
          alert(this.foo);
      });
  }
  ```

  - There should be a space between the right parenthesis `)` and the `=>`
  - There should be a space between the `=>` and the left curly brace `{` that begins the statement body.

  ```typescript
  // bad
  element.addEventListener('click', (ev: Event)=>{alert('foo');});
  
  // good
  element.addEventListener('click', (ev: Event) => {
      alert('foo');
  });
  ```

  - The statement body should be indented 2 spaces.
  - The right curly brace `}` should be on a new line.
  - The right curly brace `}` should be aligned with the line containing the  left curly brace `{` that begins the function statement.

**[top](#table-of-contents)**C

## Names

  - All variable and function names should be formed with alphanumeric `A-Z, a-z, 0-9` and underscore `_` charcters.

### Variables, Modules, and Functions

  - Variable, module, and function names should use lowerCamelCase.

**[top](#table-of-contents)**

### Types

  - Types should be used whenever necessary.
  - Arrays should be defined as `Array<type>` instead of `type[]`.
  - Use the `any` type sparingly, it is always better to define an interface.
  - Always define the return type of functions.
  - If TypeScript is capable of implicitly determining the return type of a function, then it is unnecessary to define the return type.
  - Always define the types of variables/parameters unless TypeScript can implicitly infer their type.
  
  ```typescript
  // bad
  var numbers = [];

  // bad
  var numbers: number[] = [];

  // good
  var numbers: Array<number> = [];
  ```

**[top](#table-of-contents)**

### Classes

  - Classes/Constructors should use UpperCamelCase (PascalCase).
  - All memebers of a class should be annotated with an access modifier (`private`, `protected`, or `public`).
  - As a rule of thumb, each class should be defined in its own file that has the same name as the class.

**[top](#table-of-contents)**

### Interfaces

  - Interfaces should use UpperCamelCase.
  - Only `public` members should be in an interface, leave out `protected` and `private` members. Hence, interface members       should not use access modifiers.
  - - As a rule of thumb, each interface should be defined in its own file that has the same name as the class.
  
  ```typescript
  interface Person {
      firstName: string;
      lastName: string;
      toString(): string;
  }
  ```

**[top](#table-of-contents)**

### Constants

  - All constants should use UPPER_SNAKE_CASE.

**[top](#table-of-contents)**

## Statements

### Simple

  - Each line should contain at most one statement.
  - A semicolon should be placed at the end of every simple statement.
  
  ```typescript
  // bad
  var greeting = 'Hello World'

  alert(greeting)
  
  // good
  var greeting = 'Hello World';

  alert(greeting);
  ```

**[top](#table-of-contents)**

### Compound

Compound statements are statements containing lists of statements enclosed in curly braces `{}`.

  - The enclosed statements should start on a newline.
  - The enclosed statements should be indented 2 spaces.

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
  - The return value expression must start on the same line as the `return` keyword.
  
  ```typescript
  // bad
  return 
      'Hello World!';

  // bad
  return ('Hello World!');

  // good
  return 'Hello World!';
  ```

  - It is recommended to take a return-first approach whenever possible.
  
  ```typescript
  // bad
  function getHighestNumber(a: number, b: number): number {
      var out = b;

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

  - It is recommended to **explicitly define a return type**. This can help TypeScript validate that you are always returning something that matches the correct type.

  ```typescript
  // bad
  function getPerson(name: string) {
      return new Person(name);
  }
  
  // good
  function getPerson(name: string): Person {
      return new Person(name);
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
      return typeof str === 'string';
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
  
  var keys = Object.keys(/* object */),
      length = keys.length;
  
  for(var i = 0; i < length; ++i) {
      // ...
  }
  ```

Object.prototype.keys is supported in `ie >= 9`.

  - Use Object.prototype.keys in lieu of a `for...in` statement.

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
  var sum = a+b;
  
  // good
  var sum = a + b;
  
  // bad
  var name = person . name;
  
  // good
  var name = person.name;
  
  // bad
  var item = items [4];
  
  // good
  var item = items[4];
  ```

  - No space should separate a unary/incremental operator `!x, -x, +x, ~x, ++x, --x` and its operand.
  
  ```typescript
  // bad
  var neg = - a;

  // good
  var neg = -a;
  ```
  
  - Each semicolon `;` in the control part of a `for` statement should be followed with a space.
  
  ```typescript
  // bad
  for(var i = 0;i < 10;++i) {
      // ...
  }

  // good
  for(var i = 0; i < 10; ++i) {
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

## === and !== Operators

  - It is better to use `===` and `!==` operators whenever possible.
  - `==` and `!=` operators do type coercion, which can lead to headaches when debugging code.

**[top](#table-of-contents)**

## Eval

  - **Never use eval**
  - **Never use the Function constructor**
  - **Never pass strings to `setTimeout` or `setInterval`**

**[top](#table-of-contents)**

## Rules for AngularJS

AngularJS is used as front-end framework.

###	Folder Structure

The angular folder structure should resemble the structure below:

```
angular/ 
----- my-component/
---------- MyComponentController.ts
---------- MyComponentTemplate.ts
---------- MyComponentConstants.ts 
----- my-directive/
---------- MyDirective.ts 
----- my-other-directive/
---------- OtherDirective.ts 
----- shared/ 
-----------config/
--------------- MyConfig.ts
---------- my-services/
--------------- MyService.ts 
---------- my-other-services/
--------------- MyOtherService.ts
--------- typings/
--------------- typing.d.ts
```

###	One component per file
Each service, controller, and directive should be defined in an own class and file. Each component class should comontain a static ID comprising the identifier for angular's dependency injection.

###	Avoid injecting scopes
$scope and $rootScope should not be injected and used, if possible. Use the controllerAs syntax for data binding. Per default the controller name should be referenced with “$ctrl”. 

###	Bindable members public
All bindable members of a controller should have the public access modifier.

###	Defer controller logic to services 

###	Directives

-	Declaration restrictions: Only use custom element and custom attribute methods for declaring your Directives ({ restrict: 'EA' }) depending on the Directive's role. Comment and class name declarations are confusing and should be avoided. Comments do not play nicely with older versions of IE. Using an attribute is the safest method for browser coverage.
-	Templating: Use string templates for clean templating to improve readability as code can be indented properly. This also avoids the '+' operator which is less clean and can lead to errors if used incorrectly to split lines. Furthermore, variables can be referenced with the ${myVariable} syntax.

  ```
  // avoid 
  class someDirective {  
  template:   '<div class="' + classVariable + '">' + 
                '<h1>My directive</h1>' + 
              '</div>' 
  } 

  // recommended 
  class someDirective { 
  template: `div class="${classVariable}">
              <h1>My directive</h1>
            </div>`
  }
  ```

-	DOM manipulation: Takes place only inside Directives, never a service. Note, that service can provide methods for DOM manipulation that are used in directives.
-	Directives and Filters are the only providers that have the first letter as lowercase; this is due to strict naming conventions in Directives. Angular hyphenates camelCase, so dragUpload will become <div drag-upload></div> when used on an element.
-	controllerAs: Use the controllerAs syntax inside Directives


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
