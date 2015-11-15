---
layout: post
title: Javascript Modules
tags: Javascript, Modules
comments: true
---

Modules in javascript is a way to structure your code thats more maintainable, easy to extend and debug. Defining your code into modules helps you not to polute the global scope with the things that you define in modules because it has its own scope.

Below is an example of module expression:

	(function() {
		// variables define here are only available within this scope
		// but still has access to globals
	}())

The expression above is what is called IIFE - [Immediately-invoked function expression](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression)

### Module Export

Say we want our module to be use on other parts of our code and not just within the module scope itself. This is where module export come into play.

	var ModuleA = (function() {
		var obj = {}, lists = [];

		obj.add = function(item) {
			lists.push(item)
		    console.log(lists);
		}
		obj.remove = function(item) {
			var index = lists.indexOf(item);
			if (index >= 0) lists.splice(index, 1);
			console.log(lists);
		}

		return obj;
	}())

With this module definition we are exporting two methods `add` and `remove` from our `ModuleA`. That means we can do the following:

	ModuleA.add('learn js');
	// ['learn js']

	Module.add('learn jquery')
	// ['learn js', 'learn jquery']

	Module.remove('learn js')
	// ['learn jquery']

### Global Import (Passing Another Modules as Dependencies)

	(function(A) {
		// We alias ModuleA as A here
		// we can access ModuleA exported methods as A.add() and A.remove()
	}(ModuleA))

### Augmenting Modules

Just like javascript objects that we can add another method to an existing object, the same is true to modules. 

	var Module = (function(mod) {
		mod.methodB = function() {
			// your code here
		}
		return mod;
	}(ModuleA))

For a more in deep learning on js modules, read on [JS Modules](http://eloquentjavascript.net/10_modules.html)

### What's Next

There are more to improved on the pattern we discussed above and it will be addressed on the next version of javascript.

Modules will then be supported natively in the [next version of javascript](http://wiki.ecmascript.org/doku.php?id=harmony:modules). 
There are two format use by developers today on writing modular javascript and that is [AMD](https://en.wikipedia.org/wiki/Asynchronous_module_definition) and [CommonJS](http://wiki.commonjs.org/wiki/CommonJS). 
If you are interested, I recommend an article [Writing Modular Javascript](http://wiki.commonjs.org/wiki/CommonJS) by Addy Osmani.
