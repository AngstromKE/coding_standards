HTML5
=====
### HTML Validation ###
All HTML pages should be validated against the [W3C Validator](http://validator.w3.org/) to ensure that markup is well formed. This helps to weed out problems that are able to be tested via automation.

**Note:** Most decent editors[emacs, textmate, etc] have tools that can do HTML validation.

### Doctype ###
Always include a proper doctype to trigger standards mode. Omitting the doctype triggers quirks mode and should always be avoided. The HTML5 doctype is simple and easy to remember.
```
<!doctype html>
```

### Character Encoding ###
All markup should be delivered as UTF-8, since it has the best support for internationalization. The character encoding should be designated in both the HTTP header and the head of the document via a meta tag. If the server happens to omit the HTTP header, browsers can take a guess at the character encoding and begins parsing and rendering the markup in a particular way. If there are inconsistencies, the browser will re-parse and re-render, throwing away all that work and starting over if it encounters the meta tag and its guess was incorrect. As a best practice, we always put the meta tag as early in the <head> tag as early as possible — however server-settings are ideal.
```
<meta charset="UTF-8"
```

### Self-closing Elements ###
All tags must be properly closed. For self-closing tags, the forward slash should have exactly one space preceding it. It is important to not that generally speaking, self-closing tags are not necessary.
```
<!-- Correct -->
<br />

<-- Incorrect -->
<br/>

```
### Needless Code ###
Formerly, in HTML 4.01 and XHTML 1.0, certain attributes were required for code validity, but are not actually necessary for proper parsing by a browser. The following code conventions should no longer be used. 
```
<!-- Correct HTML5 -->
<link rel="stylesheet" href="/path/file.css" />

<style>
    /* Code here. */
</style>

<script>
    // Code here
</script>

<!-- Incorrect- unnecessary cruft: XHTML 1.0 -->
<link rel="stylesheet" type="text/css" media="all" href="/path/file.css" />

<style type="text/css">
    /* Code here */
</style>

<script type="text/javascript">
    /* <![CDATA[ */
        // Code here.
    /* ]]> */
</script>
```

### Tags & Attributes ###
 All tags and attributes must be written in lowercase. Additionally, we prefer that any attribute values also be lowercase, when the purpose of the text therein is only to be interpreted by machines. For instances in which the data needs to be human readable, proper title capitalization should be followed, such as:
 ```
<!-- For machines: -->
 <meta http-equiv="content-type" content="text/html; charset=utf-8" />

<!-- For humans: -->
<a href="http://example.com/" title="Description Goes Here">Example.com</a>
```
### Indentation ###
Indent nested elements and tags with single indentation settings, whatever they may be, for each level in the hierarchy of the document.
```
<!-- Proper indentation -->
<div>
    <p>Lorem ipsumLorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod.</p>
    <ul>
        <li>tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,</li>
        <li>quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
        consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse</li>
        <li>cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non</li>
        <li>proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</li>
    </ul>
</div>
```

### HTML5 Elements ###
To provide additional semantic value to our documents, make use of HTML5 elements such as `<header>`, `<article>`, and `<section>` where appropriate. However, in cases where the HTML needs to be as backwards-compatible as possible, do not apply IDs or classes to them, since older browsers do not understand these elements by default and will not apply styling to them.
```
<header>
    <div class="site-header">
        ...
    </div>
</header>
```

### Quotes ###
In keeping with the strictness of XHTML code conventions, according to the W3C, all attributes must have a value, and must use double-quotes. The following are examples of proper and improper usage of quotes and attribute/value pairs.
```
<!-- Correct -->
<input type="text" name="email" disabled="disabled" />

<!-- Incorrect -->
<input type=text name=email disabled>
```

### IDs vs. Classes ###
HTML elements can be identified by using the id and class attributes. An ID is a unique identifier for that particular element; no other element on the page should use the same ID.

This uniqueness allows <label> elements to associate themselves with a particular input and URLs to jump to a particular scroll position on a page.

Classes are not unique. The same class can be used on multiple elements within a page, and a single element can have more than one class, in a space delimited list.
```
<ul id="categories">
    <li class="category">Jackets</li>
    <li class="category specials">Accessories</li>
    <li class="category">Shoes</li>
</ul>
```
When coming up with names for an ID or class, we use semantic names like "secondary-nav" or "primary-button" that describe what the element is, rather than names like "left-nav" or "blue-button" that describe what the element looks like, which can change over time. We also use lowercase names with hyphens separating words as opposed to camelCase or underscores.

### Anchors & Links ###
All links should point to absolute or relative URLs with user-readable content. Do not link to XML or JSON resources that are designed to be Ajaxed by JavaScript instead of navigated to directly, and do not put JavaScript in an anchor's href attribute like javascript:loadPage(2);. This allows search engines to index the content, allows the user to open the links in a new tab or window, and means the links will still work when JavaScript is broken, disabled, or not supported. This will require that the back-end be able to return a full HTML page for each important content state (e.g. sorting a table column).

### Paragraphs ###
Avoid using `<br>` tags to separate paragraphs or lines of text. Use `<p>` instead with proper opening and closing elements.

### Tables ###
Tables should not be used for page layout; only use them when you need to display tabular data. Tables provide an important semantic association (used mostly by screen readers for the sight-impaired) between row/column headers and their data, so use `<table>` rather than other elements when displaying multiple records of data.

The `<caption>` element is the recommended way to describe a table for both sighted and sight-impaired users, though this can also be done less semantically in the normal page text around the table. Use the `<thead>` and `<tbody>` elements to denote which row contains column headers so when a user prints the website and the table runs onto another page, browsers can display the `<thead>` on each page for easier readability. Remember to use the scope attribute on the `<th>` element to indicate whether the header applies to the row or column.

### Forms ###
For both semantic and functional reasons, we make full use of the `<form>` tag for all sections requiring user input. All form action attributes should point to URLs with user-readable content, so they will still work if the form is submitted by the user before JavaScript has loaded on a page, or if JavaScript is broken, disabled, or not supported. This will require that the back-end be able to return a full HTML page for form submission (e.g. registering a new user, editing the quantity in a shopping cart).

Do not nest the HTML form element tag.

### Input Labels ###
All input fields should be associated with a `<label>` element. The for attribute of the `<label>` element should contain the ID of the corresponding input field. This means the input field will receive focus when a user clicks the label and also enables screen readers for sight-impaired users to read out an appropriate description of the input field.

```
<-- Here's an example -->
<label for="home-address">Home Address</label>
<input id="home-address" type="text">
```

### Markup Deliverables ###
Typically HTML deliverables are incorporated into Content Management Systems or application delivery platforms as templates. A plan for incorporation of templates that leverage patterns created during the markup creation phase should be followed and matching types of pages to templates that were created, so that an association between the source markup and the destination markup can be maintained over time.

### Other Considerations ###

1. Site maintenance procedures
2. Browser testing strategies
3. How new features will be added
4. Where new features will be added
5. What the file system looks like for static site assets
6. If a CDN is involved
7. Naming conventions and organization of graphics and photography assets
8. If the "back-end implementation" of static HTML templates will require review by front-end team members

## References:
1. [Isobar coding standards](https://isobar-idev.github.io/code-standards/)
2. [Design Patterns Library & Code Standards](http://developer.fellowshipone.com/patterns/code.php) 





