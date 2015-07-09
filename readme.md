MARK


ANI


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