---
layout: post
title: Laravel, What???
comments: true
---

Ok, so what about Laravel? Who is Laravel? :D 

[Laravel](http://laravel.com/) is a PHP programming framework just like the popular [RoR](http://rubyonrails.org/) framework written in Ruby programming language.

It has taken the PHP community by storm and it is because of it's cool developer friendly syntax and is up to date with the latest PHP version release. 
Let me list down what I love about Laravel. 

* It has Fluent syntax
* and Eloquent ORM
* Based on latest PHP version release and component based (upcoming Laravel4)
* Community driven and with cool core developer leads

#### Fluent syntax

Laravel has a fluent query builder for building SQL queries and working with the database. Don't worry about SQL injection because it is protected upon and uses [prepared statements](http://en.wikipedia.org/wiki/Prepared_statement). Query a table as easy with this syntax: 

	$query = DB::table('users');

Here were using `table` method inside the `DB` class of Laravel. With this you can now retrieve, insert, update, or delete records from 'users' table.

For further reading [read here](http://laravel.com/docs/database/fluent)

#### Eloquent ORM

Laravel has the most advance PHP ORM(Object Relational Mapper) exists. 
All you need to do is to define a model for the table. 

	class User extends Eloquent {}

Without defining anything inside the class, Eloquent assumes that:

- the table has a primary key named *id*
- table name is the plural form of the model name

Now to find a record by its *id*:

	$user = User::find(1);

Getting excited! there's more [here](http://laravel.com/docs/database/eloquent) for further reading. 

#### Latest PHP and Component Based

PHP has a great dramatic improvement since the release of PHP5 that's why Laravel was born.

The upcoming release of Laravel4 will now be component based and will now utilize the tool [Composer](http://getcomposer.org/) as it's dependency manager.

#### Community driven and with cool core dev. leads

Laravel was created first by Taylor Otwell and now has some added cool members namely Dayle Rees, Eric Barnes, Ian Landsman, Jason Lewis and Shawn McCool. 

And many other [contributors..](https://github.com/laravel/laravel/graphs/contributors)


------------------------------------------------------












