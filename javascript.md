Javascript
==========
### Inclusion of code ###
Use external Javascript files. **Do NOT include Javascript in-line in the page unless there is a good reason**.

Use the <script> tag to include your JavaScript files at the bottom of your HTML document just before the closing </body> tag. For optimal page performance, concatenate your JavaScript into as few files as possible.
```
<script src="bundle.js"></script>
```

### Writing and formatting Javascript ###
The use of whitespace should follow long-standing English writing conventions, with blank lines between ideas and groups of code such as objects, functions, and new lines for new statements.

Formatting the language statements and patterns should follow these basics:
1. _Open braces_ are preceded by a single space
2. _Open braces_ should appear on the same line as their preceding argument
3. There shoudl be no space characters between _parentheses_ and their contents
4. Use _semicolons_ and do not rely on automatic semicolon insertion
5. Each _comma_ and _colon_ (and semi-colons that don't end a line) should be followed by a single space
6. _Binary_ and _ternary operators_ should have a single space on each side
7. _Quoted values_ should be in 'single quotes' so that double quotes may easily exist inside them
8. _Comment Javascript_ code thoroughly and consider using a pattern such as those described by [JSDocs](http://usejsdoc.org/)
9. Conditional statements go on a new line followed by the opening brace
10. Else/ else go on the same line as the brace
11. Use type strict checks with === as opposed to == whenever possible
```
for (var i = 0, len = arr.length; i < len; i++) {
    var example = 1;
    if (example === i) {
        // we are looping
    } else {
        // this will never happen
    }
}
```
To maximize readability without worrying about which boolean operators bind more tightly than others, each segment of a boolean expression should be enclosed in parentheses.
```
if ((allowUpdate) && ((user.isAdmin) || (user.role === item.owner))) {
    // do something
}
```

### Variable Declaration ###
To avoid confusion between global and local variables, we declare each variable on its own line with the var keyword. We do not use a single var keyword and then chain several variable declarations onto it separated by a comma.
```
var windowWidth;
var windowHeight;
var currentVal = $(this).val();
var min = parseInt($(this).attr('min'), 10);
```

### Best Practices ###

1. Avoid user-agent sniffing and rely on feature detection instead. Browser detection is dangerous and error-prone.
2. Avoid using document.write.
3. Only run scripts on a page that are needed for that page.
4. Don't repeat yourself (i.e. keep your code DRY)
5. Do not modify JavaScript core objects .prototype unless you really know what you're doing.
6. Use method names that make sense, such as init() or setup() for code that starts things off. Be consistent on your project.

### Variables ###
#### Variable Scope ####
Minimize the use of global or window level variables and name-spaces. Pollution of the global name-space is error prone and a bad practice.

If referencing a window or global level variable that isn't obvious, please comment as such or explicitly state it.

#### Variable Names and Types ####
Always use meaningful variable names that can be read as words, not as silly abbreviations only you understand.

1. Variable names should be camelCase.
2. Objects, classes, and name-spaces should be TitleCase.
3. Boolean values should be prefixed with `is` if at all possible.
4. Cached jQuery objects can be prefixed with $.
5. Use shorthand versions of empty `Arrays` and `Objects`.

```
// some examples
var exampleValue = 'my example variable value';
var numberOfTimes = 3;
// booleans
var isThisWorking = true;
var isNotWorking = 0;
// cache a selector
var $body = $('body');
// short hand objects and arrays
var newObject = {};
var newArray = [];
```

#### Limit Events — Use Event Delegation ####
It is always preferable to use fewer events being bound to objects on a page as possible. Too many events bound on a page can mean memory leaks or just an accumulation of handlers bound to DOM elements which becomes less and less efficient over time. Additionally, event delegation has the added benefit of persisting events over dynamic page updates when items are added or removed from the DOM.

With jQuery this is easy, simply use the on method with a selector:
```
$('body').on('click', 'a.scroller', function(){
   // this only runs if the a.scroller is matched
});
```

### Useful Resources ###
1. [5 tips for efficient jQuery](http://www.punkchip.com/javascript-efficiency/)
