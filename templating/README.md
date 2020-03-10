### Partials & EJS
EJS is a templating language that allows you to generate HTML markup with Javascript. You incorporate template tags into the html text.

```html
<ul>
  <% users.forEach(function(user){ %>
    <%- include('user/show', {user: user}); %>
  <% }); %>
</ul>
```
Partials are smaller ejs files that can be incorporated into the larger webpage. For example, a nabar can be a seperate ejs file to be included into the index page.
```html
<!-- views/pages/index.ejs -->
<!DOCTYPE html>
<html lang="en">
<head>
    <% include ("./partials/head.ejs") %>
</head>
<body class="container">

<header>
    <% include ("./partials/header.ejs") %>
</header>
```
You can pass values into your ejs files to be used. ie) Passing in objects, errors, arrays, etc.
```javascript
app.get('/', function (req, res) {
    res.render('index', {weatherObject: null, error: null, format: null, location:null});
})
```
### Escaping vs Unescaping
<a href="https://stackoverflow.com/questions/20727910/what-is-escaped-unescaped-output">Escaping and unscaping </a>
are useful to prevent Cross Site Scripting (XSS) attacks. HTML escaping is when you encode the special characters of a text, it will store it differently than expected. ie) User inputs this into the text field.
```html
<script>
    alert("Welcome");
</script>
```
However it will be stored as follows in the DB.
```html
&lt;script&gt;<br/>        alert(&quot;Welcome&quot;);<br/>&lt;/script&gt;
```
As such, the browser will display the previous text and so will not execute it.

### TOOLS
<ul>
	<li> browsersync - one of the coolest nodejs software that I've ever used. It refreshes the browser each time the files specified are saved. ie) folder 'views', 'css/*.css" and etc.

```
browser-sync start --proxy 'localhost:3000' --files 'views'
```
