MARK

# Installation

Flask depends on two external libraries, Werkzeug and Jinja2. The easiest way to
install everything quickly is through Virtual Environment, or virtualenv.

Virtualenv is probably what you want to use during development. The more projects you have, the more likely it is that you will be working with different versions of Python itself, or at least different versions of Python libraries. Virtualenv enables multiple side-by-side installations of Python, one for each project.


To install type in bash:

> sudo pip install virtualenv

After this, create a project folder and a venv folder within:

> $ mkdir myproject

> $ cd myproject

> $ virtualenv venv


Whenever you want to work on a project
> $ . venv/bin/activate

Now you can just enter the following command to get Flask:
> pip install Flask

(Pip stands for Python Install Package)

This will creates a folder which contains all the necessary executables to use the packages that a Python project would need, and a copy of the pip library which you can use to install other packages.

At this point to just get a basic helloworld app up and running you just need to create a python file, like hello.py and in that app include:

> from flask import Flask
> app = Flask(__name__)

> @app.route('/')
> def hello_world():
>     return 'Hello World!'
> 
> if __name__ == '__main__':
>     app.run()

Once this is saved you can go to bash to start the server by running:

> $ python hello.py
>  * Running on http://127.0.0.1:5000/

Then go to the site http://127.0.0.1:5000/ and if all worked well you should be up and running at the site and display Hello World.

To place in debugging you can either run: app.run(debug=True) 
or app.debug = True


To access database type sqlite3 /tmp/flaskr.db < schema.sql



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

**{{ Template Inheritance }}**

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
##Python and You

The biggest difference between Flask and other frameworks we have used so far is that Flask is written in a completely different language: Python. Although syntactically similar to Ruby, there are a few key differences between the languages. This section will not be a general introduction to Python for someone new, but just a short list of the differences that you need to know coming from Ruby.

####Data Types

Ruby and Python share many of the same data types; however they often have different names. Here's a quick breakdown of Ruby -> Python naming conventions.

-	`Arrays` in Ruby are called `Lists` in Python.
-	`Hashes` in Ruby are called `Dictionaries`, or `Dicts` in Python.
-	`Booleans` in Ruby are 'true' and 'false', in Python they are capitalized as 'True' and 'False'. Also, empty strings, lists, dicts, etc are truthy in Python, unlike Ruby.
-	`Null` in Ruby is `None` in Python

####Functions and Loops
-	`Function` definitions and `Loops` are ended in Python slightly differently than in Ruby. In Ruby you use the keyword `end`. But in Python the function is ended based on the indentation. This means you need to be very careful when typing. For Example:

		//Python Functions
		def get(x):
			return x

		def output(y):
			if y == True:
				return y

-	`For Loops` in Python are also slightly different, using the syntax `for [variable] in [object]:`. 

		//Python For Loop
		numbers = [1, 2, 3, 4]

		for x in numbers:
			print x
		
		//Output
		1
		2
		3
		4

	You can also iterate through strings and dicts with the same syntax

		//More For Loop
		dict = {a:1, b:2, c:3}

		for x in dict:
			print x

		string = "Hello"

		for x in string:
			print x

		//Output
		1
		2
		3
		H
		e
		l
		l
		o

The last thing that we need to go over for Flask are `Decorators`. This one is a little more complicated, so let's take it slowly.

- `Decorators` are, simply put, functions that take a different function as their argument, and return a new function. Let's look at a basic example.

		//A wrapper function that adds 1 to what a different function returns
		def wrapper(different_func):
			def new_func():
				print('I am running the function')
				output_variable = different_func()
				return output_variable + 1
			return new_func

		def number1_func():
			return 1

		decorated_func = wrapper(number1_func)

		decorated_func()

		//Output
		I am running the function
		2

- That code can get messy however, and you end up having to rename functions after decorating them. So Python has a syntax for automatically applying `Decorators` to functions using `@`.

		//Continuing from the code above
		@wrapper
		def number2_func():
			return 2

		number2_func()

		//Output
		I am running the function
		3

- This is the syntax that is used in Flask for route handlers.