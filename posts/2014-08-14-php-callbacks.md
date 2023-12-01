---
layout: post
title: PHP callbacks
tags: callbacks, callable
date:  2014-08-14
---

First what is a callback? 

> In computer programming, a callback is a piece of executable code that is 
> passed as an argument to other code, which is expected to call back (execute) 
> the argument at some convenient time.
>
> [definition](http://en.wikipedia.org/wiki/Callback_(computer_programming)) from wikipedia 

Clearly said. 

Callbacks can be declared using a user-defined function including anonymous function or an array of Object at index[0] and a method at index [1]. e.g.

	$function_callback = function($x) {
		return $x * 2;
	}

	$object_method_callback = array($object, 'method');
	// -- or -- for static methods
	// array('MyClass', 'method')
	// 'MyClass::method'

> Callback is denoted by `callable` type hint

This is usefull when using built-in PHP functions that accepts callbacks as one of its parameter. Functions such
as `array_filter`, `usort`, `call_user_func`, `call_user_func_array`, `forward_static_call`, `forward_static_call`, etc. 

Example using `array_filter` to filter elements in an array. 

Syntax:

	/**
	 * @param $array     array  	The array to filter
	 * @param $callback  callable	The callback  
	 * @returns array
	 */
	array_filter ( array $array [, callable $callback ] );

Below we use [anonymouse](http://php.net/manual/en/functions.anonymous.php) function for the callback.

	// create array with values from 1 to 20
	$array = range(1, 20);

	$new_arr = array_filter($array, function($value) {
		return ($value % 2) == 0;
	});

	// prints new set of array which is divisible by 2
	print_r($new_arr);

...is accomplished with the same code below by passing the name of callback function as second argument.

	function divisibleByTwo($value) {
		return ($value % 2) == 0;
	}

	$array = range(1, 20);

	$new_arr = array_filter($array, 'divisibleByTwo');

	print_r($new_arr);

How about callback using an array of Class and method? Example below.

	class Number {
		public static function divisibleByTwo($value) {
			return ($value % 2) == 0;
		}
	}
		
	$array = range(1, 20);

	$new_arr = array_filter($array, array('Number', 'divisibleByTwo'));

	print_r($new_arr);

Callback is such a powerfull tool, and as always learning the basics would give you a good foundation. 




