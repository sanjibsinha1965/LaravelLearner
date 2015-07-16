# Routing Best Practices   

Route::when('*', 'csrf', ['post', 'put', 'patch']);

Route::get('test/test', 'HomeController@showTest');
Route::get('home/index', 'HomeController@showIndex');
Route::get('home/about', 'HomeController@About');
Route::get('home/contact', 'HomeController@showContact');
Route::get('php/php-training-in-kolkata', 'PhpController@showIndex');
Route::get('php/variable-and-data-type', 'PhpController@phpFirstPage');
Route::get('codeigniter/codeigniter-training-in-kolkata', 'CodeIgniterController@showIndex');
Route::get('codeigniter/how-to-start-codeigniter', 'CodeIgniterController@CIFirstPage');
Route::get('wordpress/how-to-start-wordpress', 'WpController@showIndex');

Route::get('wordpress/how-to-start-wordpress', 'WpController@showIndex');

Route::group(['prefix']=>'home', function()
{
	Route::get('/', 'HomeController@showIndex');
Route::get('/about', 'HomeController@About');
Route::get('/contact', 'HomeController@showContact');
});

To get hold of all 'home' controller we can do another thing. Considering that 'home' as my 'resource' I can write like that:

Route::resource('home', 'HomeController');

Suppose you have a folder structure like that:

app/routes/admin.php
app/routes/login.php
app/routes/register.php

Now we can declare this structure in your 'routes.php' in a single command like this:

foreach(File::allFiles(_DIR_, '/routes') as $partial)
{
	require_once $partial->getPathname;
}


