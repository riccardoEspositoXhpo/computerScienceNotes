# Web Development Wiki

## Basics

### Basic Directory Structure

To get a Flask app running and deploy a web server it is advised to use the following directory structure

* Project Name - hosts app.py, .py, requirements.txt
    * static - hosts .css, .js and any other static file (i.e. images, gif, ...)
    * templates - hosts .html files



## Flask 




## Jinja

Jinja is a templating engine. It uses placeholders in HTML files to dynamically generate content. It is used in conjunction with python.

It is especially helpful when dynamically filling HTML pages in a flask app, by passing variables to the front-end and rendering them with Jinja

### Re-using a template

With Jinja we can define a template, i.e layout.html, and use Jinja to construct "similar" pages.

```html
<!-- layout Page -->
<!DOCTYPE html>

<html lang="en">
    <head>
        <meta name="viewport" content="initial-scale=1, width=device-width">
        <title>Web Page</title>
    </head>
    <body>
        {% block body %}{% endblock %}
    </body>
</html>


<!-- success page -->
{% extends "layout.html" %}

<!-- here we tell Jinja how to replace the placeholders defined in the previous page -->
{% block body %}
    You are registered!
{% endblock %}

 
```

### Jinja Variables, Loops, Conditions

Jinja integrates well with Flask and it can receive variables to be displayed dynamically in HTML.
Firstly we send the variable via Flask

```python

# message is some string, rawPuzzle is n x n array
message = '' 
rawPuzzle = []
return render_template('index.html', message = message, rawPuzzle = rawPuzzle)

```

Jinja then uses the following syntax to display the above mentioned variables

```html

<!-- variables -->
 <p><h4>{{message}}</h4></p>

<tbody>
    <!-- loops -->
    {% for row in rawPuzzle %}
            <tr>
                {% for num in row %}  
                    <!-- conditions -->
                    {% if num == 0 %}
                        <td contenteditable='true' oncopy="return false" oncut="return false" onpaste="return false">
                    {% endif %}
                    {% if num != 0 %}
                        <td contenteditable='true' oncopy="return false" oncut="return false" onpaste="return false">{{num}}
                    {% endif %}
                {% endfor %}
            </tr>
    {% endfor %}
</tbody>


```



## HTML

HTML, known as Hyper Text Markup Language, is used to render web pages.

### Basic File Format

<!DOCTYPE html>

<!-- Demonstrates inheritance -->

```html

<!-- Used to specify HTML 5 use -->
<!DOCTYPE html>

<!-- HTML Comments are done like this. The language works by using tags with specific meanings. Each Tag can have attributes associated to it, and they are closed with </tagName>. A barebone html page needs a head, body, wrapped in a html tag -->
<html>
    <head>
        <title>hi</title>
    </head>
    <body >
        <header >
            Beily
        </header>
        <main>
            Welcome to my home page!
        </main>
        <footer>
            Copyright &#169; Beily
        </footer>
    </body>
</html>

```



### List of attributes and tags


```html

<!-- sets the language of document -->
<html lang="en">

    <head>
        
        <!-- responsive web design. width attribute helps render page on mobile vs desktop -->
        <meta name="viewport" content="initial-scale=1, width=device-width">
        
        <!-- heads have a title tag -->
        <title>headings</title>
    </head>

    <!-- style attribute assigns CSS -->
    <body style="text-align: center;"> 
        <!-- h1 to h6 to govern size of text -->
        <h1>One</h1>

        <!-- p to split in paragraphs -->
        <p>
            Lorem ipsum dolor sit amet.
        </p>


        <!-- forms are used  to submit data -->
        <form>
            <!-- autocomplete shows previously used answers. id used to reference in css. Placeholder puts data, type helps with input type. Type can be button, text, date, submit, ... -->
            <input autocomplete="off" autofocus id="name" placeholder="Name" type="text">
            <input type="submit">
        </form>

        <!-- alt is used to provide a metadata description to a field. src is the directory of the image, typical to have static/images/image.jpg -->
        <img alt="Image Description" src="image.jpg">

        <!-- a tag creates a link. Note this can be an internal page or an external one. -->
        Link here - <a href="image.html">this can be pressed</a>.

        <!-- unordere list, bullet points -->
        <ul>
            <li>foo</li>
        </ul>

        <!-- provides dropdown menu with options -->
        <select>
            <option value="xx-large">xx-large</option>
            <option selected value="initial">initial</option>
        </select>

            <!-- tables have heads and bodies. Must write data row by row, column by column -->
         <table>
            <thead>
                <tr>
                    <td>Title 1</td>
                    <td> Title 2</td>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>4</td>
                    <td>5</td>
                </tr>
            </tbody>
        </table>


    </body>

</html>
```

### Headers


```html
<!DOCTYPE html>

<!-- Demonstrates headings (for chapters, sections, subsections, etc.) -->

<html lang="en">

    <head>
        <title>headings</title>
    </head>

    <body>

        <h1>One</h1>
        <p>
            Lorem ipsum dolor sit amet.
        </p>

        <h2>Two</h2>
        <p>
            Mauris ut dui in eros semper hendrerit.
        </p>

        <h3>Three</h3>
        <p>
            Aenean venenatis convallis ante a rhoncus.
        </p>

        <h4>Four</h4>
        <p>
            Integer at justo lacinia libero blandit aliquam ut ut dui.
        </p>

        <h5>Five</h5>
        <p>
            Suspendisse rutrum vestibulum odio, sed venenatis purus condimentum sed.
        </p>

        <h6>Six</h6>
        <p>
            Sed quis malesuada mi.
        </p>

    </body>

</html>

``` 


### Images


```html

<!DOCTYPE html>

<!-- Demonstrates image -->

<html lang="en">
    <head>
        <title>image</title>
    </head>
    <body>
        <img alt="Image Description" src="image.jpg">
    </body>
</html>


```


### Links

```html

<!DOCTYPE html>

<!-- Demonstrates link -->

<html lang="en">
    <head>
        <title>link</title>
    </head>
    <body>
       Link here - <a href="image.html">this can be pressed</a>.
    </body>
</html>

```


### Lists

```html

<!DOCTYPE html>

<!-- Demonstrates (unordered) lists -->

<html lang="en">
    <head>
        <title>list</title>
    </head>
    <body>
        <ul>
            <li>foo</li>
            <li>bar</li>
            <li>baz</li>
        </ul>
    </body>
</html>


```


### Tables


```html
<!DOCTYPE html>

<!-- Demonstrates table -->

<html lang="en">
    <head>
        <title>table</title>
    </head>
    <body>
        <table>
            <tr>
                <td>1</td>
                <td>2</td>
                <td>3</td>
            </tr>
            <tr>
                <td>4</td>
                <td>5</td>
                <td>6</td>
            </tr>
            <tr>
                <td>7</td>
                <td>8</td>
                <td>9</td>
            </tr>
            <tr>
                <td>*</td>
                <td>0</td>
                <td>#</td>
            </tr>
        </table>
    </body>
</html>

```






## CSS

CSS is not a programming language, but is typically used in conjunction to HTML to change the style of a web page.

### Basic in-file styling

```html
<!DOCTYPE html>

<html lang="en">
    <head>
        <title>css</title>
    </head>
    <body style="text-align: center;">
        <header style="font-size: large;">
            Beily
        </header>
        <main style="font-size: medium;">
            Welcome to my home page!
        </main>
        <footer style="font-size: small;">
            Copyright &#169; Beily
        </footer>
    </body>
</html>
``` 

### List of CSS Tags and Attributes

```css

/* set the RGB color in hex.
Set behavior when hovering over an element, in this case underline
*/
a {
    color: #ff0000;
    text-decoration: none;
}

a:hover {
    text-decoration: underline;
}

/* set the text alignment and font size */
body
{
    text-align: center;
    font-size: large;


}

/* font size larger than previous */
#first
{
    font-size: larger;
}

/* grab the first child of paragraph tag */ 
p:first-child
{
    font-size: larger;
}


.jumbotron {
    background-color: #0e7551;
    color: #fff;
    margin-bottom: 2rem;
    padding: 2rem 1rem;
    text-align: center;
    font-family: -apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,"Noto Sans",sans-serif,"Apple Color Emoji","Segoe UI Emoji","Segoe UI Symbol","Noto Color Emoji";
}

.container {
    margin-left: auto;
    margin-right: auto;
    padding-left: 15px;
    padding-right: 15px;

}

#homePage {
    background-image: url("/image/homePage.jpeg");
}

main .form-control
{
    /* Center form controls */
    display: inline-block;

    /* Override Bootstrap's 100% width for form controls */
    width: auto;
}

main
{
    /* Scroll horizontally as needed */
    overflow-x: auto;

    /* Center contents */
    text-align: center;
}

main img
{
    /* Constrain images on small screens */
    max-width: 100%;
}


```

### Selectors

```html

<!DOCTYPE html>

<!-- If you have a single instance of "header", you can style it like this. -->

<html lang="en">
    <head>
        <style>

            body
            {
                text-align: center;
            }

            header
            {
                font-size: large;
            }

            main
            {
                font-size: medium;
            }

            footer
            {
                font-size: small;
            }

        </style>
        <title>css</title>
    </head>
    <body>
        <header>
            Beily
        </header>
        <main>
            Welcome to my home page!
        </main>
        <footer>
            Copyright &#169; Beily
        </footer>
    </body>
</html>


``` 


### Classes

```html
<!DOCTYPE html>

<!-- Demonstrates CSS classes -->

<html lang="en">
    <head>
        <style>

            .centered
            {
                text-align: center;
            }

            .large
            {
                font-size: large;
            }

            .medium
            {
                font-size: medium;
            }

            .small
            {
                font-size: small;
            }

        </style>
        <title>css</title>
    </head>
    <body class="centered">
        <header class="large">
            Beily
        </header>
        <main class="medium">
            Welcome to my home page!
        </main>
        <footer class="small">
            Copyright &#169; Beily
        </footer>
    </body>
</html>
```

### Stylesheet

```html

<!DOCTYPE html>

<!-- Demonstrates external stylesheets -->

<html lang="en">
    <head>
        <link href="css5.css" rel="stylesheet">
        <title>css</title>
    </head>
    <body>
        <header class="large">
            Beily
        </header>
        <main class="medium">
            Welcome to my home page!
        </main>
        <footer class="small">
            Copyright &#169; Beily
        </footer>
    </body>
</html>
```

```css
.centered
{
    text-align: center;
}

.large
{
    font-size: large;
}

.medium
{
    font-size: medium;
}

.small
{
    font-size: small;
}
```

### Bootstrap

```html

<!-- full bootstrap package -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
<link rel='stylesheet' href='https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css' integrity='sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2' crossorigin='anonymous'>
<script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>


```

### Useful HTML Links

```html
<!-- google fonts -->
<link href='https://fonts.googleapis.com/css2?family=Montserrat:wght@500&display=swap' rel='stylesheet'>

<!-- ajax -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>

```







## Javascript

Javascript is a fully functional programming language. It is often deployed on web application to handle "client-side" activities.
Although nothing prevents us from coding a calculator in javascript, it has functions that are well suited to handle events.

### Hide and Show Elements

<!DOCTYPE html>

```html
<html lang="en">
    <head>
        <script>

            // Toggles visibility of greeting
            function blink()
            {
                let body = document.querySelector('body');
                if (body.style.visibility == 'hidden')
                {
                    body.style.visibility = 'visible';
                }
                else
                {
                    body.style.visibility = 'hidden';
                }
            }

            // Blink every 500ms
            window.setInterval(blink, 500);

        </script>
        <title>blink</title>
    </head>
    <body>
        hello, world
    </body>
</html>
```

### Geolocation

```javascript

navigator.geolocation.getCurrentPosition(function(position) {
    document.write(position.coords.latitude + ", " + position.coords.longitude);
});

```

### Event Listeners

<!DOCTYPE html>

```html
<html lang="en">
    <head>
        <script>
            // this waits for the entire document to be loaded before executing
            document.addEventListener('DOMContentLoaded', function() {
                document.querySelector('form').onsubmit = function() {
                    // takes the content of form as soon as a submit button is pushed
                    
                    // pops a message on screen, we can call it via the "id", prefixed by #
                    alert('hello, ' + document.querySelector('#name').value);

                    // just returning something
                    return false;
                };
            });

        </script>
        <title>hello</title>
    </head>
    <body>
        <form>
            <input autocomplete="off" autofocus id="name" placeholder="Name" type="text">
            <input type="submit">
        </form>
    </body>
</html>
```

### Script File

```html

<!DOCTYPE html>

<html lang="en">
    <head>
        <script src="hello4.js"></script>
        <title>hello</title>
    </head>
    <body>
        <form>
            <input autocomplete="off" autofocus id="name" placeholder="Name" type="text">
            <input type="submit">
        </form>
    </body>
</html>

```

```javascript

document.addEventListener('DOMContentLoaded', function() {
    document.querySelector('form').onsubmit = function() {
        alert('hello, ' + document.querySelector('#name').value);
        return false;
    };
});

```

### Keypress

```html

<!DOCTYPE html>

<html lang="en">
    <head>
        <script>

            document.addEventListener('DOMContentLoaded', function() {
                let input = document.querySelector('input');

                // listens for key presses and executes a function every time
                input.addEventListener('keyup', function(event) {
                    let name = document.querySelector('#name');
                    if (input.value) {
                        name.innerHTML = `hello, ${input.value}`;
                    }
                    else {
                        name.innerHTML = 'hello, whoever you are';
                    }
                });
            });

        </script>
        <title>hello</title>
    </head>
    <body>
        <form>
            <input autocomplete="off" autofocus placeholder="Name" type="text">
        </form>
        <p id="name"></p>
    </body>
</html>

``` 


### Change Style Dynamically

```html

<!DOCTYPE html>

<!-- Demonstrates programmatic changes to size -->

<html lang="en">
    <head>
        <title>size</title>
    </head>
    <body>
        <p>
            Lorem ipsum dolor sit amet.
        </p>
        <select>
            <option value="xx-large">xx-large</option>
            <option value="x-large">x-large</option>
            <option value="large">large</option>
            <option selected value="initial">initial</option>
            <option value="small">small</option>
            <option value="x-small">x-small</option>
            <option value="xx-small">xx-small</option>
        </select>
        <script>

            // function listens for a change in option. Note that value = 'xxx' is the name for JS to recognize. The other one is displayed 
            // Changes the body size in this case based on the option chosen.

            // can be used to do almost anything with the page itself
            document.querySelector('select').addEventListener('change', function(event) {
                document.querySelector('body').style.fontSize = this.value;
            });

        </script>
    </body>
</html>


```