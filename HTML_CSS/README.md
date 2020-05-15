# Web Design

Web Development is designing a website using HTML, CSS & Javascript. Traditionally static websites used only HTML & CSS in web design but later Javascript was created so that sites can have different behaviors.

You can think of this as:

1. HTML - Basic structure of sites
   1. ie) Outline sketches or drawings in Anime
2. CSS - Control *presentation, formatting and layout* of the site
   1. ie) Coloring and the character design
3. Javascript - Controls the behavior of the elements
   1. ie) Animations of the anime characters


## 1. HTML

HTML stands for HyperText Markup Language. A markup language uses tags to identify different types of content and the purposes they serve to each webpage.

These HTML tags also called "elements" specify the structure of the site similar to a human skeleton. Each tag represents a different components or makeup of the site.

### 1.1. Basic Terminology:

1. **Element** - Makes up opening tag, closing tag and the content within the tags. An element can contain elements inside it as well.

```html
<p>Twice is best group ever!</p>
```

2. **Tags** - Define the type of element and the start and closing of that element

```html
<body></body>
```

3. **Attributes** - Properties that provide additional information about that element. It's used to refer to the location of images, websites, css files and classes or id.
```html
<a href="twiceIsBest.com" class = "Logo" id="Best">...</a>
```

### 1.2. Basic HTML Document Structure

Most elements have a pair of opening and closing tags but some ```<br>, <embed>, <img>, <meta>``` are self-closing.

Sites follow this format with the 
1. ```<!DOCTYPE html>``` - Describes what edition of html to use. (Newest one)
2. ```<html>``` - Tells the start and end of the HTML document
3. ```<head>``` - Contains your meta-data, links, titles, CSS files and scripts that are run immediately
4. ```<body>``` - Contains the main structure of your HTML page seen by the user. INclude scripts you want run then

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Hello World</title>
  </head>
  <body>
    <h1>Hello World</h1>
    <p>This is a web page.</p>
  </body>
</html>
```

## 2. CSS

CSS stands for Cascading Style Sheets. It's a styling language when coupled with HTML changes the appearance and animations of the HTML tags. You specify in your CSS files the colors, fonts, spacing, animations and so on forth. 

Cascading means that styling changes from your parents trickle down to your child elements.

### 2.1. Basic Terminology

1. Selectors - Designates the styling for a target element(s) within an HTML document. There are three types of selectors: **type, class and id**.

    1. Type - Refers to the element type ie) 
    ```css
    body {...}
    p {...}
    div {...}
    ```

    2. Class - Refers to elements that includes the classes' name inside the class attribute
   ```css
   .Logo {
       ...
   }
   ```
   
   ```html
   <h1 class="Logo">Twice is Life</h1>
   ```

   3. ID - Refers only to a specific element. ID styling only applies to first element declared with that id.
   ```css
   # twice {
       ...
   }
   ```
   ```html
   <div id="twice">
   ...
   </div>
   <a href="..." id="twice"> Hi </a> <!-- The ID styling doesn't apply -->
   ```

2. Properties - Descriptions of styling effects

```css
```

3. Values - Numerical values to the types of styling

```css
```

### 2.2 Others

```css
html {
   box-sizing: border-box; /* Tells the browser to include padding and margins in the element's width */
}
```

tells 


## 3. Javascript

Javascript is a dynamically-typed programming language that controls the behavior of a site. It can modify website content and change how the site reacts to user action. Most importantly it allows web developers to create interactive sites. Adding javascript to a site requires using the script tag.

Uses include security password cration, check forms, interactive games, animations and special effects. You can create mobile apps or even server-side application.


### link vs script for loading Javascript files

You normally use a ```<script>```tag to refer to your javascript files. The only time you would use a ```<link>``` tag to reference a javascript file would be if you would want to preload the file. Then later on you would use a ```<script>``` to execute that file in your body.

A ```<link>``` file is to relate stylesheets or other linked documents. ex) CSS, appendix, glossary etc. Although mainly in web dev, it's usually css stylesheets.

```html
<script src="~/Scripts/jquery-1.4.1.js" type="text/javascript"></script>

<link href="~/Scripts/jquery-1.4.1.js" as="script" rel="preload" />
```


