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


BEN



GORDON