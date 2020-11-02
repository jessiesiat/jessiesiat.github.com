---
layout: post
title: Warning when using Laravel cursor
date:  2020-11-02 18:40:18 +0800
tags: laravel, lazy collection, cursor
comments: true
---

The use of [`cursor`](https://laravel.com/docs/8.x/eloquent#using-cursors) in eloquent is to reduce the memory usage especially when working on large amount of data. You may be tempted to replace all your model `get()` calls to `cursor()` because of that. You should not do that because the later is only advisable to be used on the given scenario above and it may make your application slower if you do so. 

`get()` will return a `Illuminate\Support\Collection` class while `cursor()` will return `Illuminate\Support\LazyCollection`. First we'll define lazy collection. 

### Lazy Collection

Lazy collection is only a supplement to the already existing `Collection` class. It leverages php generators and for use when working on large datasets so that you can still keep your memory usage low. 

We'll go through the scenario below to better understand the difference between the two.

### Benchmark 

For this test scenario I seeded the users table with 60,000 records.
Let's compare the query below. 

Using regular collection:

	// Memory usage: ~131mb, Request duration: ~1.08s, DB queries: 1
	$users = User::get();
	$aUser = $users->sum(function($u) {
		return Str::startsWith($u->name, 'A') ? 1 : 0;
	});

Using lazy collection:

	// Memory usage: ~57mb, Request duration: ~2.14s, DB queries: 1
	$users = User::cursor();
	$aUser = $users->sum(function($u) {
		return Str::startsWith($u->name, 'A') ? 1 : 0;
	});

As you can see, using lazy collection really consumes less memory but slower than a regular collection. But not only that, the more you work on lazy collection returned by the query builder `cursor`, the slower it will be. Let see another example below.
	
Using regular collection:

	// Memory usage: ~131mb, Request duration: ~1.52s, DB queries: 1
	$users = User::get();
	$aUser = $users->sum(function($u) {
		return Str::startsWith($u->name, 'A') ? 1 : 0;
	});
	$bUser = $users->sum(function($u) {
		return Str::startsWith($u->name, 'B') ? 1 : 0;
	});
	$cUser = $users->sum(function($u) {
		return Str::startsWith($u->name, 'C') ? 1 : 0;
	});
	$dUser = $users->sum(function($u) {
		return Str::startsWith($u->name, 'D') ? 1 : 0;
	});


Using lazy collection:

	// Memory usage: ~57mb, Request duration: ~7.71s, DB queries: 4
	$users = User::cursor();
	$aUser = $users->sum(function($u) {
		return Str::startsWith($u->name, 'A') ? 1 : 0;
	});
	$bUser = $users->sum(function($u) {
		return Str::startsWith($u->name, 'B') ? 1 : 0;
	});
	$cUser = $users->sum(function($u) {
		return Str::startsWith($u->name, 'C') ? 1 : 0;
	});
	$dUser = $users->sum(function($u) {
		return Str::startsWith($u->name, 'D') ? 1 : 0;
	});

For regular collection there is only a slight increase in request duration but for lazy collection the request duration multiplies because of the number of database queries also increases in corelation to number of `sum()` calls.

Laravel actually has `remember()` method for lazy collection which will only execute a single query given the example above but its no better for the scenario. Memory usage will be ~163mb and request duration is ~2.37s.

### Closing

Only use `cursor` when you are to iterate over a large amount of data or depending on your use case. A sample for this is when you added a column on a table after it was
released to production and updating its value is not feasible on mass update but instead you need a copy of each model instance.

This is not to be confused with lazy collection itself because it is a very good addition to the framework. You just have to identify yourself on where it applies best. 

That's it! Hit me up on twitter if I missed something on this post. 
