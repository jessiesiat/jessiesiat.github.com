---
layout: post
title: Autoloading PSR-4 Standard
tags: PSR-4,Composer
comments: true
---

> Because I blog about PSR-0!

Why new autoloading standard? 

The reason is to simplify the creation of directory structure. Let's say I am creating a package `jessiesiat/magic` and we will use PSR-4 to autoload our classes.

But first let us see on how it is done using PSR-0.

### Using PSR-0

starting with the composer.json

	...
	{
		"autoload": {
			"psr-0": {
				"JessieSiat\\Magic\\": "src/"
			}
		}
	}
	...

our directory structure would be - *pay attention to the hierarchy*

	/src
		/JessieSiat
			/Magic
				Card.php
	/test
	..
	composer.json
	..

then our Card.php file definition

	<?php namespace Jessiesiat\Magic;

	class Card {

		// function definition here

	}

Were done, our class 'JessieSiat\Magic\Card' now exists!

At some point it is not neccessary to have that kind of directory structure. Why not define the classes directly under the `src/`, especially if you just need few classes. We can achieve that with PSR-4, using the same `namespace` as above. 

### Using PSR-4

as said, this is how our directory looks like

	/src
		Card.php
		..
	/test
	..
	composer.json
	..

our Card.php file definition would be the same - *see namespace keyword*

	<?php namespace Jessiesiat\Magic;

	class Card {

		// function definition here

	}


then our composer.json would be.

	...
	{
		"autoload": {
			"psr-4": {
				"JessieSiat\\Magic\\": "src/"
			}
		}
	}
	...


After running `composer dump-autoload` our class 'JessieSiat\Magic\Card' now exists, simplifying our directory!

_More info [here](http://seld.be/notes/psr-4-autoloading-support-in-composer)_