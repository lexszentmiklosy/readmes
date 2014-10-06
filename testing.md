# Testing


* Mocha
* Chai
* Jasmine
* Casper
* Browserify
* e2e, end2end
* Phantom
* Common JS 
* * A way of writing modules, uses module.export. Alternatives are AMD (Asynchronous Module Definition). This is not a library, not a function or anything, just a standard and way to import things. 

* Browserify 
* * Enables the use of require statements in javascript, they are not built into the language or browsers. Used to compile (bundle) a file, like turning an ejs template into html which the browser can understand. This is the same for just JS.


### SEE PATERN

* Setup
* Execute
* Expect

(Known as AAA in TDD - Arrange, Act, Assert)

SUT - Subject Under Test


### Modules

Make things configurable, everything should have options

tightly coupled, loose coupled?

Breakup Code into groups:

1. Presentation & Interaction
2. Data/Server Communication
3. Application State
4. Setup


Unit Test

* Single Object under test is behaving correctly

Through, stable, fast, few

Query = ???
Command = makes changes, modifies


|                   |Query      | Command  |
|-------------------|-----------|----------|
| Incoming          | Test incoming query messages by making assertions abou what they send back (result). Test the interfact not the implimentation (what???)           |   Test incoming command messages by making assertions about direct public side effects.       |
| Sent to Self      |  DO NOT TEST THEM | DO NOT TEST THEM     |
| Outgoing          |  Redundant, tested on Incoming Query     |  Expect to send        |
 

A test that makes it impossible to improve code without breaking the test is not a good test 

Incoming 


Integration Test?

End to End?


Links

[The Magic Tricks of Testing by Sandi Metz](https://www.youtube.com/watch?v=URSWYvyc42M)

[Writing Testable Javascript](http://alistapart.com/article/writing-testable-javascript/)

[Writing Modular JS](http://addyosmani.com/writing-modular-js/)

[JS Module Patern](http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html)

