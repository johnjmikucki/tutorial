# Dynamic Templates #

## What is it? ##

- Allows you to use the query sets that we discussed, and other things, to put stuff on your website that changes when your data changes.
- Django allows us to put special code right into the HTML.
- Remember the `mycats` value we sent in the `def current_cats(request):` function in `cat_shelter/views.py`?  We were passing that information into the HTML, so now we can use the `mycats` variable in our HTML

## HowTo ##

- Inside the HTML, variables/strings that you just want to print go inside double curly brackets `{{``}}`
  - `{{ mycats }}`
- Commands go inside a curly brace marked with a `%`: `{%``%}`

*Example*

    {% for cat in mycats %}
      {{ cat }}
    {% endfor %}

- Combine HTML and Django magic to make our page look like it did before, but this time using our variables
- **NOTE** If you're having trouble with your templates and getting weird errors, make sure you haven't put any spaces between your `{` and your `%`.  It doesn't like that.
- For now we're looking at `cat_shelter/templates/cat_shelter/current_cats.html`

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
