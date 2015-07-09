

ANI


#{{ Become a Jinja Ninja }}

![Ninja](http://www.anarchyinthesandbox.com/wp-content/uploads/2013/12/Ninja-Baby.gif)

**{{ What is Jinja2? }}**

Another external library Flask is dependent on is Jinja2, a template engine. Jinja2 shares similarities with [Mustache](http://mustache.github.io/). Templates are housed in the templates folder in your application. 

**{{ Including Ninja }}**

In your main .py file, make sure to include the render_template() method. To enable this method, all you have to do is give the name of the template in your code and the variables you want to pass to Jinja2 as keyword arguments. 

For example: 


	from flask import render_template #first import render_template

	@app.route('/hello/')

	@app.route('/hello/<name>')

	def hello(name=None):

    	return render_template('hello.html', name=name)  #include the render_template() function, passing the name of the template and other variables as keyword arguments


**{{ Delimiters }}**

Jinja employs a couple of delimiters with varied uses. 

-{% ...%} are used for *statements*. This is where your code will go. 

-{{ ... }} are used for *expressions*. This will print out your output. 

-{# ... #} are used for *comments*.

Example: 

	<!DOCTYPE html>
	<html>
	<head>
		<meta charset="utf-8">
		<meta http-equiv="X-UA-Compatible" content="IE=edge">
		<title>Flaskr</title>
		<link rel=stylesheet type=text/css href="{{ url_for('static', filename='style.css') }}">
	</head>
	<body>
	  <div class="logo">
	    <img src="http://flask.pocoo.org/docs/0.10/_static/flask.png">
	  </div><br>
	  <div class=page>
	    <h1>FlaskChat</h1>
	    <div class=metanav>
	    {% if not session.logged_in %} 
	      <a href="{{ url_for('login') }}">log in</a> 
	    {% else %}
	      <a href="{{ url_for('logout') }}">log out</a>
	    {% endif %}
	    </div>
	    {% for message in get_flashed_messages() %}
	      <div class=flash>{{ message }}</div>
	    {% endfor %}
	    {% block body %}{% endblock %}
	  </div>

	  {# this is a comment #}
		
	</body>
	</html>

**{{ Variables }}**

Template variables are defined by the context dictionary that is passed to the template.You can access attributes of a varaible by using dot (.) or ['attribute']. 

Example: 





















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






