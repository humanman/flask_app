MARK


ANI


#{{ Become a Jinja Ninja }}

![Ninja](http://www.anarchyinthesandbox.com/wp-content/uploads/2013/12/Ninja-Baby.gif)

**{{ What is Jinja2? }}**

Another external library Flask is dependent on is Jinja2, a template engine. Jinja2 shares similarities with [Mustache](http://mustache.github.io/). Templates are housed in the templates folder in your application. 

**{{ Includeing Ninja }}**

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

	{{ user.name }}
	{{ user['name']}}



Jinja2 has a number of builtin filters that are used to modify variables. Filters are separated by the pipe symbol (|). The output of one filter is applied to the next. 

For example, in our show_entries.html file we employ a filter: 


	{% extends "layout.html" %}
	{% block body %}
	  {% if session.logged_in %}
	    <form action="{{ url_for('add_entry') }}" method=post class=add-entry>
	      <dl>
	        <dt>Title:
	        <dd><input type=text size=30 name=title>
	        <dt>Text:
	        <dd><textarea name=text rows=5 cols=40></textarea>
	        <dd><input type=submit value=Share>
	      </dl>
	    </form>
	  {% endif %}
	  <ul class=entries>
	  {% for entry in entries %}
	    <li><h2>{{ entry.title }}</h2>{{ entry.text|safe }}
	  {% else %}
	    <li><em>Unbelievable.  No entries here so far</em>
	  {% endfor %}
	  </ul>
	{% endblock %}



{{ entry.text|safe }} says the text of the entry is safe from automatic escaping. A list of builtins is available [here](http://jinja.pocoo.org/docs/dev/templates/#builtin-filters).

** {{ Template Inheritance }} **

The best part about using Jinja2 is the ability to use template inheritance. 

Template inheritance enables you to build a base template that contains all the common elemts of your site and defines blocks that child templates can override. Child blocks are defined by {% block -- %} {% endblock %} 


It's like using yields and partials in Rails. 

Base Template: 


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

		
	</body>
	</html>



In the above example, one block is defined: {% block body %}{% endblock %}. 

Child Template: 

	{% extends "layout.html" %}
	{% block body %}
		<h2>Login</h2>
		{% if error %}<p class=error><strong>Error:</strong> {{ error}}{% endif %}
		<form action="{{ url_for('login')}}" method=post>
			<dl>
				<dt>Username:
				<dd><input type=text name=username>
				<dt>Password:
				<dd><input type=password name=password>
				<dd><input type=submit value=Login>
			</dl>
		</form>
	{% endblock %}

The {% extends %} tag tells Jinja2 that this template extends another template. In this case it is layout.html.  

NOTE: You can't define multiple {% block %} tags with the same name in the same template. 


















BEN



GORDON