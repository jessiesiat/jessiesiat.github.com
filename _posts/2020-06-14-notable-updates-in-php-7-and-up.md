---
layout: post
title: Notable updates in PHP version >= 7
date:  2020-06-14 12:28:18 +0800
categories: php7
---

### Return type declarations

The same types are available for return type declarations as are available for argument type declarations.

	function arraysSum(array ...$arrays): array
	{
	    return array_map(function(array $array): int {
	        return array_sum($array);
	    }, $arrays);
	}

### Null coalescing operator

	$username = isset($_GET['user']) ? $_GET['user'] : 'nobody';
	
	// is equivalent to ...
	$username = $_GET['user'] ?? $_POST['user'] ?? 'nobody';

### Spaceship operator

	// returns -1, 0 or 1 when $a is respectively less than, equal to, or greater than $b
	echo $a <=> $b;

### Anonymous classes

	$app = new Application;
	$app->setLogger(new class implements Logger {
	    public function log(string $msg) {
	        echo $msg;
	    }
	});



