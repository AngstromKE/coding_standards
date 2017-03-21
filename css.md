## Goals for Effective CSS ##
CSS is an unusual language which can easily lead to code bloat, inconsistencies in design or clashing code techniques. It is easy to end up with CSS code that is so fragile it can cause site-wide regressions with small changes.

**Note**: This stylesheet also applies to SCSS and SASS

CSS should: 
1. Be easy to maintain
2. Follow clear enought patterns to understand
3. Offer a clear place for new styles going forwards
4. Not be a drag on page loading performance
5. Not include unused style rules
6. Address different devices, browser versions, and do as much as it can with as little code as possible

#### Frameworks ####
Pre-built UI components or CSS frameworks can be beneficial, however just like any third party code please choose wisely and based on benefit of features and flexibility. Locking development into a library that unintentionally imposes limits is not good.

Some examples of third party frameworks might include:
1.  UI component or widget libraries (e.g. Foundation, Bootstrap, jQuery UI)
2.  Grid Systems
3.  Typography adjustments
4.  Normalizing code

#### Living Style Guides ####
One technique to consider is maintaining static HTML style reference implementations well into integration with server-side / back-end systems. These could be a series of templates or widgets that use the live styles being built. This helps reduce regressions that can happen across the board as the code for the site evolves. Continue to test these reference implementations as they will be the "source of record" for the styles created on the site. They also allow you to more easily distinguish the front-end bugs from the bugs potentially introduced by integration with a complex back-end.

These reference implementations can serve as a living style guide and broken components are easily spotted in testing over time.

Defining a solid style guide to be applied to tag names can significantly reduce the size of the CSS if that style guide is adhered to by both the design and development teams. It is recommended that a style guide is agreed upon at the beginning of a project, defined in HTML and then iterated on by both the design and development teams.

#### Inclusion ####
Use the <link> tag to include all your style sheets in the <head> of the document. For optimal page performance, concatenate your CSS into as few files as possible and do not use the @import command to include other style sheets, as this will fire an additional HTTP request and block page rendering until its completion.
```
<link rel="stylesheet" type="text/css" href="main.css">
```


### Inline Styles ###
 We strive to maintain proper separation of content and design, and therefore highly discourage the use of inline `style="..."` attributes. This not only makes maintenance a nightmare, but inextricably ties the presentation to the data it represents. All of our CSS will be stored in external files, with one `master.css` file called per page. That single file will incorporate other files as necessary with the `@import` syntax.

**Note:** An exception to this rule is `style="display:none"` for revealing hidden elements via JavaScript.

### CSS Validation ###
All cascading stylesheets should be verified against the [W3C](http://jigsaw.w3.org/css-validator/) 
validator, to ensure correct syntax and to check for possible accessibility issues with text and background colors. This in and of itself is not directly indicative of good code, but it helps to weed out problems that are able to be tested via automation. It is no substitute for manual code review.

**Note**: Some text editors are able to check the validity of the currently open CSS document.

### CSS Formatting ###
To ease potential headaches for maintenance, we require that all CSS be written in a consistent manner. For one, all CSS selectors must be listed on their own line. As a general rule of thumb, if there is a comma in CSS, it should immediately be followed by a line break. This way, we know that all text on a single line is part of the same selector. Likewise, all property/value pairs must be on their own line, with one tab of indentation. The closing brace must be on the same level of indentation as the selector that began it - flush left.

```
/* Correct */
#selector-1 span,
#selector-2 span,
#selector-3 span {
    background: #fff;
    color: #000;
}

/* Incorrect */
#selector-1 span, #selector-2 span, #selector-3 span {
    background: #fff;
    color: #000;
}

/* Incorrect */
#selector { background: #fff; color: #000; }
```
Here is a summary of the CSS formatting rules we recommend:
1. Use a new line for every selector and very declaration
2. Use a single space before the opening brace of a set of rules
3. Use lowercase for elements and shorthand hex values e.g #aaa
4. Hyphenate class selector names; avoid underscores and camelCase
5. Quote attribute values in selectors
6. Use one level of indentation for each declaration.
7. The closing brace of declaration goes in the same column as the first character of the set of rules
8. Use a single blank line between sets of rules

Inside sets of rules or style declarations:
1. Add a single space between the property and value, for example:
`prop: value;` and not `prop:value;`
2. Use double quotes for quoted values
3. Always include a semi-colon at the end of the last declaration
4. Use shorthand if you can
5. When allowed, use 0 without units

### Pixels Vs. Ems ###
 We use the px unit of measurement to define font size, because it offers absolute control over text. We realize that using the em unit for font sizing used to be popular, to accommodate for Internet Explorer 6 not resizing pixel based text. However, all major browsers (including IE7 and IE8) now support text resizing of pixel units and/or full-page zooming. Since IE6 is largely considered deprecated, pixels sizing is preferred. Additionally, unit-less line-height is preferred because it does not inherit a percentage value of its parent element, but instead is based on a multiplier of the font-size.
 ```
/* Correct */
/* 13 * 1.5 = 19.5 ~ Rounds to 20px. */
#selector {
    font-size: 13px;
    line-height: 1.5;
}

/* Incorrect */
/*
    Equivalent to 13px font-size and 20px line-height,
    but only if the browser default text size is 16px.
*/
#selector {
    font-size: 0.813em;
    line-height: 1.25em;
}
```
### Shorthand ###
In general, CSS shorthand is preferred because of its terseness, and the ability to later go back and add in values that are already present, such as the case with margin and padding. Developers should be aware of the TRBL(Top Right Bottom Left) acronym, denoting the order in which the sides of an element are defined, in a clock-wise manner: Top, Right, Bottom, Left. If bottom is undefined, it inherits its value from top. Likewise, if left is undefined, it inherits its value from right. If only the top value is defined, all sides inherit from that one declaration.
```
/* Correct */
#selector {
    margin: 0 0 10px;
    padding: 0 0 10px;
}

/* Incorrect */
#selector {
    margin: 0 0 10px 0;
    padding: 0 0 10px 0;
}
```

#### Hex Colors ####
 We prefer hex values for all colors, written in lower-case. No upper-case or RGB, please! Additionally, all colors should be written as tersely as possible. This means that colors such as full blue, which can be written lengthily as `#0000FF`, should be simply written as `#00f`. Obviously, for colors that require more precision, all six characters should be used. For example, a light shade of grayish beige: `#f9f9f0`.

#### Background ####
```
/* Correct- shorthand */
#selector {
    background: #fff url(../images/file.png) repeat-x fixed left bottom;
}

/* Incorrect- longhand unnecessary */
#selector {
    background-color: #fff;
    background-image: url(../image/file.png);
    background-repeat: repeat-x;
    background-attachment: fixed;
    background-position: left bottom;
}
```

#### Border ####
In general, border should be a single line declaration, assuming that the values of the border are the same on all sides of the element. The order in which values are declared are: width, style, and color.
```
/* correct */
#selector {
    border: 1px solid #000;
}
```
If the values of each side differ, then there are two possible ways of using shorthand, and it is up to the discretion of the developer to decide which to use. Note that method 2 follows the TRBL pattern.
```
/* Method 2 */
#selector {
    border-color: #fff #999 #666 #ccc;
    border-style: solid dashed dotted double;
    border-width: 1px 2px 3px 4px;
}

/* Method 3 */
#selector {
    border-top: 1px solid #fff;
    border-right: 2px dashed #999;
    border-bottom: 3px dotted #666;
    border-left: 4px double #ccc;
}
```
By contrast, the same style declaration is extremely verbose using longhand. This should be avoided, except in instances where only one particular value needs to be overridden, allowing the rest to flow through.

```
/* Avoid this */
/* longhand */
#selector {
    border-top-color: #fff;
    border-right-color: #999;
    border-bottom-color: #666;
    border-left-color: #ccc;
    border-top-style: solid;
    border-right-style: dashed;
    border-bottom-style: dotted;
    border-left-style: double;
    border-top-width: 1px;
    border-right-width: 2px;
    border-bottom-width: 3px;
    border-left-width: 4px;
}
```
#### Font ####
Not to be confused with the inadvisable <font> tag, the CSS font property can be written in a few different ways. The shorthand property puts all the aspects of the font into a single declaration, whereas the longhand splits it out over several lines. While the contrast between methods is not as stark as with that of the border property, there is still space to be saved by using shorthand. While line-height can be defined within the scope of the font declaration, but when written in longhand it has its own unique property.

**Note:** Times New Roman is encapsulated in quotes, because the font name itself contains spaces.
```
/* shorthand */
#selector {
    font: italic small-caps bold 15px/1.5 Cambria, 'Times New Roman', sans-serif;
}

/* longhand */
#selector {
    font-style: italic;
    font-variant: small-caps;
    font-weight: bold;
    font-size: 15px;
    line-height: 1.5;
    font-family: Cambria, 'Times New Roman', sans-serif;
}
```
### Longhand ###
When overriding only parts of a style, longhand declaration is preferred. This way, by sticking to shorthand for initial style declarations, anytime we see a longhand declaration used, we know that we are specifically overriding only a very precise part of an overall style, thereby leaving other aspects unaffected.
```
/* longhand override */
#selector {
    border: 1px solid #ccc;
    font: 11px Verdana, sans-serif;
}

#selector.modifier {
    border-bottom-color: #333;
    border-bottom-width: 2px;
    font-family: Georgia, serif;
}
```
### Specifity ###
Use the minimum specificity required to achieve the desired style. It can be difficult to quickly read and locate styles or even bugs with heavily nested styles in the CSS.

The ID is the most specific selector, since it can only match one element, and the class is a close second. Use those whenever possible rather than HTML tag names.
```
/* BAD */
button#back-button { ... }
.popular ul li a { ... }
.popular > ul > li > a { ... }

/* GOOD */
.back-button { ... }
.popular-link { ... }
.unpopular-link { ... }
```
As a rule, CSS is most maintainable with the simplest selectors possible. Try applying a class to the element you want to target instead

While performance of CSS selectors has been a debated topic, browsers perform quite well on most types of selectors. That said, specificity reduced to the most simple name to get the desired results is the best idea in most cases for readability and maintainability.

**Note: **

Avoid using the `!important` keyword. Treat it like the nuclear option, only to be used in the most extreme of cases. This fundamentally destroys the specificity feature and can even break accessibility for some users.

There is usually another way to achieve the same goal without causing headaches for developers in the future who are either trying to debug a styling issue, or trying to use normal specificity to override a style for a particular element only to find that they can't.

### ID Selectors ###
Use the lowest level of specificity necessary to get the desired results. This means the use of the ID selector should be minimized. Often creating a new class is preferable to using inheritance or additional specificity to target an element or elements.

ID selectors, if used, should be used mainly as access points for JavaScript or if a very particular use case surfaces. Styles and classes can be applied via the same element with a className.

### Vendor Prefixes ###
When using vendor prefixed features, put the standardized rule at the end to ensure browsers optimize and use the standard if they recognize it.

```
.thing {
    -webkit-transition: all 100ms;
    transition: all 100ms;
}
```

 ### Coding Patterns ###
There are a number of popular design patterns for naming conventions on selectors, groupings or extensions of styles in CSS files. Sometimes these are of value and may be used on projects as long as the developers are on board and they are used consistently by the team.

Examples of pattern systems include BEM, SMACSS, Object Oriented CSS, Atomic design, and others.

A particular coding pattern system will be decided upon for every project. The most simple, and basic set of conventions will be used.
