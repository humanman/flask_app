#So What is Flask?


![flask](http://media.giphy.com/media/5yLgoc6sGi6NqT9uNDa/giphy.gif)

Ruby has Rails. Python has Flask, except Flask is  a bit lightweight compared to Rails.

Flask manages your routing using Werkzeug and templating using Jinja 

The purpose of Flask is to provide a painless and quick way to get a simple app up and running on the web. 



###Werk-what?
	
Just think of Rack, but with a german sausage sounding name.

```
from werkzeug.wrappers import Request, Response

@Request.application
def application(request):
    return Response('Hello World!')

if __name__ == '__main__':
    from werkzeug.serving import run_simple
    run_simple('localhost', 4000, application)
 ```


###Jinj-huh?

Remember squids, flounders, and mustaches?  Then this will look familiar:

```
{% extends "layout.html" %}
{% block body %}
  <ul>
  {% for user in users %}
    <li><a href="{{ user.url }}">{{ user.username }}</a></li>
  {% endfor %}
  </ul>
{% endblock %}
```






