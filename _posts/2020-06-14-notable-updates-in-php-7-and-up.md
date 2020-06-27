---
layout: post
title: Notable updates in PHP version >= 7
date:  2020-06-27 21:28:18 +0800
categories: php7
comments: true
---

As of this writing the latest PHP version is 7.4, I will update this post when i found notable updates in PHP v7.x releases.

### Return type declarations

The same types are available for return type declarations as are available for argument type declarations.

	function arraysSum(array ...$arrays): array
	{
	    return array_map(function(array $array): int {
	        return array_sum($array);
	    }, $arrays);
	}

Nullable return types are also allowed by prefixing the type name with a question mark.

### Null coalescing operator

	$username = isset($_GET['user']) ? $_GET['user'] : 'nobody';
	
	// is equivalent to ...
	$username = $_GET['user'] ?? 'nobody';

	// can also be more ...
	$username = $_GET['user'] ?? $_POST['user'] ?? 'nobody';

### Spaceship operator
The code below returns -1, 0 or 1 when $a is respectively less than, equal to, or greater than $b

	echo $a <=> $b;

### Anonymous classes
You can now create a class without a name, perfect for closure type as the example below.

	$app = new Application;
	$app->setLogger(new class implements Logger {
	    public function log(string $msg) {
	        echo $msg;
	    }
	});

### Symmetric array destructuring

The shorthand array syntax `([])` may now be used to destructure arrays for assignments (including within foreach), as an alternative to the existing `list()` syntax, which is still supported.

	$data = ['Juan', '28'],

	// list() style
	list($name, $age) = $data;

	// [] style
	[$name, $age] = $data;
	
For array with non-integer or non-sequential keys, you can specify keys in `list()` or `[]`

	$keysData = ["age" => 1, "name" => 'Juan'];

	// list() style
	list("id" => $age, "name" => $name) = $keysData;

	// [] style
	["id" => $age, "name" => $name] = $keysData;

### Multi catch exception handling
Multiple exceptions per catch block may now be specified using the pipe character `|`. This is useful for when different exceptions from different class hierarchies are handled the same.

	<?php
	try {
	    // some code
	} catch (FirstException | SecondException $e) {
	    // handle first and second exceptions
	}

### Typed properties
Class properties now support type declarations.

	<?php
	class User {
	    public int $id;
	    public string $name;
	}

### Arrow functions
Arrow functions provide a shorthand syntax for defining functions with implicit by-value scope binding.

	$y = 1;
	$func1 = fn($x) => $x + $y;

	// equivalent to using $y by value:
	$func2 = function ($x) use ($y) {
	    return $x + $y;
	};

### Null coalescing assignment operator
Assign a value when not yet set, empty or undefined.

	<?php
	$array['key'] ??= $someValue;

	// is roughly equivalent to
	if (!isset($array['key'])) {
	    $array['key'] = $someValue;
	}

### Unpacking inside arrays

Basically unpacking array inside another array. Example below explains it very clear.

	<?php
	$parts = ['apple', 'pear'];
	$fruits = ['banana', 'orange', ...$parts, 'watermelon'];
	// ['banana', 'orange', 'apple', 'pear', 'watermelon'];
