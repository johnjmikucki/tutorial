# Dynamic Templating #

## What is it? ##
- Incorporates data from QuerySets into views, so your website's content changes when your data changes.
- A bit like Mad Libs with HTML.  Words come from your database!
- Works by putting special python and Django code right inside the HTML.

- Remember the `mycats` value we passed to the `def current_cats(request):` function in `cat_shelter/views.py`?  We did that to make it accessible here, so we can use it in our template code.

- Inside the HTML, variables/strings that you just want to print go inside double curly brackets `{{``}}`, like so: `{{ mycats }}`
- Commands go inside a curly brace marked with a `%`: `{%``%}`.  This tells Django to interpret the contents as Python code.  Be sure not to put spaces between the `{` and `%` !

*Example*

    {% for cat in mycats %}
      {{ cat }}
    {% endfor %}


## Next Steps ##

### Rebuild your view using templates###

Why: So we don't have to manually update our web page every time we get a new cat.

How:

- Add some Django magic to your HTML, so our page looks like before, but uses our variables

*Example*

    <html>
      <head>
        <title>Kitty Kastle</title>
      </head>
      <body>
        <div>
          <h1><a href="">Tara's Kitty Kastle!</a></h1>
        </div>
        
        {% for cat in mycats %}
          <div>
            <h2><a href=""> {{ cat.name }}</a></h2>
            <p>Age: {{ cat.age }}</p>
            <p>Fluffy: 
            {% if cat.fluffy %}
              Yes!
            {% else %}
              Nope
            {% endif %}</p>
            <p>{{ cat.desc|linebreaks}}</p>
          </div>
        {% endfor %}
        
      </body>
    </html>
