# Named Routes

//example of named routes
Route::get('/', function(){
    
    return link_to_route('session/create', 'Log in');
    
});

Route::get('session/create','SessionController@create');

But all these are normal procedure that we have seen before. Then where is the named route? You might have asked.
Okay here it is:

//this
Route::get('session/create', ['as'=>'create', 'use'=>'SessionController@create']);
//equivalent to 
Route::get('/', function(){
    
    return route('create');
    
});

Route::get('register', [
    
    'before'=>['guest'],
    'as'=>['register'],
    'use'=>['SessionController@register']    
]);

//you can write it like this also

Route::get('register', [
    'as'=>['register'],
    'use'=>['SessionController@register']    
])->before('guest'); 
