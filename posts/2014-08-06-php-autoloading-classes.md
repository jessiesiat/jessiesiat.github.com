---
layout: post
title: PHP Autoloading classes
date:  2014-08-06
---

At first I find autoloading a tricky thing to do, the way Composer does and frameworks but not anymore.
Today I will share the secret on how classes are loaded on demand. 

You can actually gain access to a class by including them in your bootstrap file but what if we have a lot of files? This time we will do autoloading and bootstrap only the files needed.
i.e.

`index.php`

	require 'bootstrap.php';

	// initialized class here and it will be autoloaded
	$foo = new Foo;
	$bar = new Bar;

Let's not imagine, but let's say this will be our working directory. Our target classes to be autolaoded will be under the services folder. 

	/project
		/services
			Foo.php
			Bar.php
			...
		bootstrap.php
		index.php

Let's now reveal our `bootstrap.php` file.

`bootstrap.php`

	spl_autoload_register(function($class) {
		if(file_exists($path = __DIR__.'/services/'.$class.'.php')) 
		{
			require_once $path;
			return true;
		}
		return false;
	});

You can do your implementation within the callable but in our example our target directory is the services folder where our classes is located.

`spl_autoload_register` accepts a [callable](http://php.net/manual/en/language.types.callable.php) as the first parameter.

	/**
	 * @param callable $autoload_function 
	 * @param bool     $throw 	whether to throw exceptions when the autoload_function cannot be registered.
	 * @param bool     $prepend 	whether to prepend the autoloader on the autoload stack
	 */
	spl_autoload_register(callable $autoload_function, $throw = true, $prepend = false)

Another way to do autoloading is the `__autoload()` function. We can achieve the same as above 
with the following code. 

`bootstrap.php`

	function __autoload(string $class) {
		if(file_exists($path =  __DIR__.'/services/'.$class.'.php')) {
			require_once $path;
		}
	}

By default `spl_autoload_register` replace the engine cache for `__autoload()` function. So if you
definde a `spl_autoload_register` then it will be use. 

The use of `__autoload()` is discourage and may be depreciated or remove later on in favor of `spl_autoload_register` because the later provides a more flexible alternative for autoloading classes.

Let me know your comments!











