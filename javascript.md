# Absolventa JS Styleguide

## Content

1. Linting
2. Variables
3. Spacing
4. Objects
5. Arrays
6. Strings
7. Properties
8. Equality
9. Comments
10. Semicolons
11. Commas
12. Naming conventions
13. DOM Node Rules
14. Events
15. Appendix

### 1. Linting

JSLint is a static code analysis tool used in software development for checking if JavaScript source code complies with coding rules.

It might be necessary to install jslint.
The easiest way to do this is via npm which is available if you install nodejs(http://nodejs.org/)
    
    // the -g flag is necessary to install it globally
    $ npm install jslint -g
    
Now you just have to make it work with your text editor of choice.

####vim
TODO

####Sublime
Use package control to install jslint and set it up.

Settings can be opened via the Command Palette, or the Preferences > Package Settings > JSLint > Settings – User menu entry.

    {

        // Options pass to jslint.
        "jslint_options": "--nomen --predef $, document, _gaq, Modernizr, HandlebarsTemplates, Absolventa, PraktikumInfo, jQuery, console, fixture, describe, it, expect, beforeEach, afterEach, spyOn, loadFixtures, confirm, CustomizeActiveAdmin, unescape,_ --browser"

    }

### 2. Variables

Always use var to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace. Captain Planet warned us of that.

    // bad
    superPower = new SuperPower();

    // good
    var superPower = new SuperPower();

Assignments in a declaration must be on their own line. For example:

    // Bad
    var foo = true;
    var bar = false;
    var a;
    var b;
    var c;

    // Good
    var a,
        b,
        c,
        foo = true,
        bar = false;

### 3. Spacing

- Use 4 spaces for indentation.
- Remove trailing whitespace.
- Always use curly braces.

**Example**

    // bad
    if(condition) foo();

    // good
    if (condition) {
        foo();
    }

- Lines should be no longer than 80 characters, and must not exceed 100 (counting tabs as 4 spaces).
- if/else/for/while/try always have braces and always go on multiple lines.

**Example**

    var i;

    // good
    if (condition) {
        doSomething();
    } else if (otherCondition) {
        somethingElse();
    } else {
        otherThing();
    }

    // good
    for (i = 0; i < 100; i += 1) {
        object[array[i]] = someFn(i);
    }

- Any , and ; must not have preceding space.
- Any : after a property name in an object definition must not have preceding space.
- The ? and : in a ternary conditional must have space on both sides.

**Example**

    // bad
    var match = 'foo'.length===3?true:false;

    // good
    var match = 'foo'.length === 3 ? true : false;

- New line at the end of each file.
- No extra spaces around elements and arguments

**Example**

    array = ['*'];
    array = [a, b];
    foo(arg);
    foo("string", object);
    foo(options, object[property]);
    foo(node, "property", 2);

- Use indentation when making long method chains:

**Example**

    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // good
    $('#items')
        .find('.selected')
            .highlight()
            .end()
        .find('.open')
            .updateCount();

### 4. Objects

Use the literal syntax for object creation.

  // bad
  var obj = new Object();

    // good
    var obj = {};

Use a readable indentation:

    // bad
    var obj = { ready: false,
        nav: 'test', foo: 9 };

    // good
    var obj = {
        ready: false,
        nav: 'test',
        foo: 9
    };

### 5. Arrays

Use the literal syntax for array creation.

    // bad
    var arr = new Array();

    // good
    var arr = [];

### 6. Strings

Use single quotes '' or double quotes "" for strings, but stay consistent inside of your project. At Absolventa, we use single quotes for most of our projects.

    // bad
    var yourName = "Roy Trenneman",
        myName = 'Maurice Moss';

    // good
    var yourName = "Roy Trenneman",
        myName = "Maurice Moss";

    // good
    var yourName = 'Roy Trenneman',
        myName = 'Maurice Moss';

Strings longer than 80 characters should be written across multiple lines using string concatenation.

    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that \
        was thrown because of Batman. \
        When you stop to think about \
        how Batman had anything to do \
        with this, you would get nowhere \
        fast.';

    // good
    var errorMessage = 'This is a super long error that ' +
        'was thrown because of Batman. ' +
        'When you stop to think about ' +
        'how Batman had anything to do ' +
        'with this, you would get nowhere ' +
        'fast.';

### 7. Properties

Use dot notation when accessing properties:

    var luke = {
      jedi: true,
      age: 28
    };

    // bad
    var isJedi = luke['jedi'];

    // good
    var isJedi = luke.jedi;

Use subscript notation [] when accessing properties with a variable.

    var luke = {
      jedi: true,
      age: 28
    };

    function getProp(prop) {
      return luke[prop];
    }

    var isJedi = getProp('jedi');


### 8. Equality

Strict equality checks (===) must be used in favor of abstract equality checks (==). The only exception is when checking for undefined and null by way of null.

    // Check for both undefined and null values, for some important reason.
    undefOrNull == null;

**How to test for types**:

- String: typeof object === "string"
- Number: typeof object === "number"
- Boolean: typeof object === "boolean"
- Object: typeof object === "object"
- Function: typeof object === "function"
- Plain Object: object != null && typeof object === 'object'
- Array: object instanceof Array
- null: object === null
- null or undefined: object == null
- undefined:
    - Global Variables: typeof variable === "undefined"
    - Local Variables: variable === undefined
    - Properties: object.prop === undefined

Hint: There is a convenient helper method (Absolventa.Helpers.type(yourParam)), which makes type checking a breeze.

### 9. Comments

Comments are always preceded by a blank line. Comments start with a capital first letter, but don't require a period at the end, unless you're writing full sentences. There must be a single space between the comment token and the comment text; for multi-line comments a new line may be used in place of a space.

Single line comments go over the line they refer to:

    // We need an explicit "bar", because later in the code foo is checked.
    var foo = "bar";

Multi-line comments may be used for long comments:

    /*
    Four score and seven—pause—minutes ago...
    */

Comment functions with the following pattern, use the following comment format with **@desc** and optional **@param** and **@return** statements. Each param has its own line.

    var isNumber = function(possiblyANumber, foo) {
        // @desc    robust solution to identify different types of numbers
        //          reference here: http://stackoverflow.com/questions/18082/validate-numbers-in-javascript-isnumeric
        // @param   {string} possiblyANumber
        // @param   {boolean} foo
        // @return  {boolean}

        return !isNaN(parseFloat(possiblyANumber)) && isFinite(possiblyANumber);
    };

### 10. Semicolons

Use them. Never rely on [ASI](http://inimino.org/~inimino/blog/javascript_semicolons).

    // bad
    (function() {
        var name = 'Skywalker'
        return name
    })()

    // good
    (function() {
        var name = 'Skywalker';
        return name;
    })();

### 11. Commas

No leading commas

    // bad
    var once
        , upon
        , aTime;

    // good
    var once,
        upon,
        aTime;

No additional trailing commas

    // bad
    var hero = {
        firstName: 'Bob'
      , lastName: 'Parr'
      , heroName: 'Mr. Incredible'
      , superPower: 'strength'
    };

    // good
    var hero = {
        firstName: 'Bob',
        lastName: 'Parr',
        heroName: 'Mr. Incredible',
        superPower: 'strength'
    };



### 12. Naming conventions

Variable and function names should be full words, using camel case with a lowercase first letter. Names should be descriptive but not excessively so. Exceptions are allowed for iterators, such as the use of i to represent the index in a loop.

**Example**:

    var normalVariableName = 'test',  // camel case, lowercase first letter
        Absolventa = {},              // namespace has capital first letter
        ContentSlider,                // constructors have a capital first letter
        i = 0;                        // just an iterator, no need to be expressive here

### 13. DOM Node Rules

.nodeName must always be used in favor of .tagName.

.nodeType must be used to determine the classification of a node (not .nodeName).

### 14. Events

To recognise hooked up events on dom nodes at a glance, we use custom data attributes:

Instead of:

  // MARKUP
  <a class="button">Click me</a>

  // JS
    $('.button').click(function() {
      // DO SOMETHING
    });

We should avoid using css classes and ids for event handling issues.

So, a better approach would be:

  // MARKUP
  <a data-action="openLightbox">Click me</a>

  // JS
    $('[data-action="openLightbox"]').click(function() {
      // DO SOMETHING
    });

If you don't want to manually bind events to the custom data action attributes, you could use some logic like the following:

  // MARKUP
  <a data-action="openLightbox">Click me</a>

  // JS
    var actions = {
        openLightbox: function() {},
        submitForm: function() {}
        //....
    };

    $(document).on('click', '[data-action]', function() {
        var action = $(this).data('action'); // Use jQuery for IE6+ compatibility
        if (action in actions) {
            actions[action].apply(this, arguments);
        }
    });

### 15. Appendix

This styleguide is based on the following styleguides and articles:

[idiomatic.js](https://github.com/rwaldron/idiomatic.js/)

[jQuery](http://contribute.jquery.org/style-guide/js/#spacing)

[airnbnb.js](https://github.com/airbnb/javascript)

[Alex Kinnee](http://alexkinnee.com/2013/11/binding-js-events-using-data-action-selectors/)

