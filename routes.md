# All kind of routes used in the book #
/*
 * Routing funda
	it does not mattaer what you type in 
     * Route::get('this/that', controller@method);
     * you can write it as
     * Route::get('that/this', controller@method);
 * you can write
 * Route::get('sanjib-sinha', controller@method);
     * But inside that 
     * controller method 
     * return View::make('what is written here is important'); 
 * controller routing overrides the original routing!
|--------------------------------------------------------------------------
| Application Routes
|--------------------------------------------------------------------------
|
| Here is where you can register all of the routes for an application.
| It's a breeze. Simply tell Laravel the URIs it should respond to
| and give it the Closure to execute when that URI is requested.
|
 *
 *  

Route::get('/contact', function()
{
	return View::make('contact'); 
});
 * Route::get('/', function()
{
     $task = \Bengaliana\Task::find(1);
     var_dump($task->title);
});
 *  Route::get('/', function()
{
	return View::make('form');
});
 * Route::get('home/header', 'HomeController@Header');
Route::get('home/footer', 'HomeController@Footer');

//query building examples
Route::get('/', function()
{
    //$user = DB::table('users')->where('username', 'admin')->first();
//    $name = DB::table('users')->where('username', 'admin')->pluck('username');
//    var_dump($name);
    
    //$names = DB::table('users')->lists('username', 'password');
    //$users = DB::table('users')->distinct()->get();
//    $query = DB::table('users')->select('username');
//$users = $query->addSelect('age')->get();
    //$users = DB::table('users')->where('age', '>', 18)->get();
//    $query = DB::table('users')->where('username', 'debangshu');
//$users = $query->addSelect('age')->get();
   // $users = DB::table('users')->where('age', '>', 50)->orWhere('username', 'admin')->get();
    //$users = DB::table('users')->whereBetween('age', array(48, 100))->get();
   // $users = DB::table('users')->whereNotBetween('age', array(50, 100))->get();
//    $users = DB::table('users')
//->join('contacts', 'users.id', '=', 'contacts.user_id')
//->join('post', 'users.id', '=', 'post.user_id')
//->select('users.username', 'contacts.address', 'post.title')->get();
    //$users = DB::table('users')->leftJoin('post', 'users.id', '=', 'post.user_id')->get();
    $users = DB::table('users')
->where('username', '=', 'debangshu')
->orWhere(function($query)
{
$query->where('age', '>', 17)->where('username', '<>', 'admin');
})
->get();
    var_dump($users);
//    foreach ($names as $id => $username) {
//        $userid = $id+ 1;
//        echo "<a href='user/".$userid."'>$username</a> " . "<br>";
//        
//    }
});
*/

/*Route::post('home/regis', function()
{
    //$username = $_POST['username'];   
    
   //return \Illuminate\Support\Facades\Redirect::to('home/form');
   $data = Input::all();

// Build the validation constraint set.
$rules = array(
'username' => 'alpha_num|min:3',
    'email'=>array('email', 'not_in:@,.')
);

// Create a new validator instance.
$validator = Validator::make($data, $rules);

 if ($validator->passes()) {
// Normally we would do something with the data.
return 'Data was saved.';}
else{
    return 'You did not provide correct data';
}

return Redirect::to('/'); 
    
//return View::make('home.regis');
});
Route::get('test/test', array('before' => 'auth', function()
{
    // Only authenticated users may enter...
    
    
}));
Route::get('test/form', function()
{
    $data = array('red'=>'blue');
	
    return View::make('test.form')->with('data', $data);
});
Route::get('/', function()
{
    $user = User::find(10);
    
    if (Hash::check('pass', $user->password))
        {
            //return Redirect::to('test/test');
            return 'k';
        }
    
});
 * 
*/
Route::get('/', 'HomeController@home');

//Route::get('test/test', 'HomeController@test');

Route::get('test/test', function()
{
return View::make('test/test');
});

Route::post('testsessionandcookie', function()
{
Session::put('username', Input::get('username'));

$cookie = Cookie::make('city', Input::get('city'), 1);
return Redirect::to('session-and-cookie-test')->withCookie($cookie);
});

Route::get('session-and-cookie-test', function()
{
    $return = '<h1>Reload Now, You will Loose only Session data. '
            . 'If you Reload after ONE minute, You will Loose Session & Cookie data both!</h1>'; 
$return .= '<h2>Your user name, from a Session, is ' . Session::get('username') . '</h2><br><br>';

$return .= '<h2> You city, from a cookie, is ' .
Cookie::get('city') . '</h2>.<br><br>';
$return .= '<a href="session-cookie-loss">Reload</a>';
echo $return;
});

Route::get('session-cookie-loss', function()
{
$return = '';

if (Session::forget('username')) {
$return .= 'Your name, from a Session, is ' .
Session::get('username') . '. <br>';
} else {
$return .= 'User Name session is not set.<br>';
}
if (Cookie::has('city')) {
$return .= 'Your city, from a cookie, is ' .
Cookie::get('city') . '. <br>';
} else {
$return .= 'City cookie is not set.<br>';
}
;
$return .= '<a href="test/test">Back to Session and Cookie Test</a>';
echo $return;
});

Route::get('/regis', 'HomeController@regis');
//Route::get('user/{id}', 'HomeController@user');
Route::get('login', 'HomeController@login');

Route::get('/update', function(){
    $user = User::find(2);
    $user->password = password_hash('pass', PASSWORD_BCRYPT);
    $user->save();
    return 'Password of ' . $user->username . ' has been changed succesfully.';
});

	

Route::post('login', function(){
    Session::put('username', Input::get('username'));
    if(Auth::attempt(Input::only('username', 'password'))) {
    return Redirect::intended('/');
    } else {
    return Redirect::back()
    ->withInput()
    ->with('error', "Invalid credentials");
    }
});

Route::get('logout', function(){
    if (Auth::logout() && Session::forget('username')){
    return Redirect::to('/')->with('message', 'You are now logged out!');
    }
 else {
        return Redirect::to('login');
    }
    
    });

Route::group(array('before'=>'auth'), function(){
    Route::get('users/create', function(){
        //your code
    });
    Route::post('user', function(){
        //your code
    });
   Route::get('/', 'HomeController@home');
   Route::get('user/{id}', 'HomeController@user');

});

//using mail methods
Route::get('contact', function()
{
    return View::make('test/contact'); 
});

Route::post('contact', function()
{
    $data = Input::all();
    $rules = array(
    'subject' => 'required',
    'message' => 'required'
    );

    $validator = Validator::make($data, $rules);

    if($validator->fails()) {
    return Redirect::to('contact')->withErrors($validator)->withInput();
    }

     $emailcontent = array (
    'subject' => $data['subject'],
    'emailmessage' => $data['message']
    );

    Mail::send('emails.contactemail', $emailcontent, function($message)
    {
    $message->to('me@sanjib.me','Laravel Learner')
    ->subject('Contact via Form');
    });

    return 'Thanks! Your message has been sent successfully.';

});



//using autoload app/start/global.php
Route::get('shape', function()
{
$shape = new MyShapes;
return $shape->octagon();
});
//using autoload composer.json
Route::get('shapeagain', function()
{
$shape = new Custom\Shapes\MyShapes;
return $shape->triangle();
});

//using session

Route::get('session-one', function()
{
return View::make('session-one');
});
Route::post('session-one', function()
{
Session::put('email', Input::get('email'));
Session::flash('name', Input::get('name'));
$cookie = Cookie::make('city', Input::get('city'), 1);
return Redirect::to('session-two')->withCookie($cookie);
});
Route::get('session-two', function()
{
$return = 'Your email, from a Session, is ' . Session::get('email') . '. <br>';
$return .= 'You name, from flash Session, is ' . Session::get('name') . '. <br>';
$return .= 'You city, from a cookie, is ' .
Cookie::get('city') . '.<br>';
$return .= '<a href="session-three">Next page</a>';
echo $return;
});

Route::get('session-three', function()
{
$return = '';
if (Session::has('email')) {
$return .= 'Your email, from a Session, is ' .
Session::get('email') . '. <br>';
} else {
$return .= 'Email session is not set.<br>';
}
if (Session::has('name')) {
$return .= 'Your name, from a flash Session, is ' .
Session::get('name') . '. <br>';
} else {
$return .= 'Name session is not set.<br>';
}
if (Cookie::has('city')) {
$return .= 'Your city, from a cookie, is ' .
Cookie::get('city') . '. <br>';
} else {
$return .= 'City cookie is not set.<br>';
}
Session::forget('email');
$return .= '<a href="session-three">Reload</a>';
echo $return;
});

//    if (Schema::hasColumn('users', 'email'))
//    {
//        return 'Yes';
//    }
//    else
//    {
//        return 'No';
//    }

//    $roles = Role::find(1)->user;
//    foreach ($roles as $value) {
//        var_dump($value);
//    }

//    $posts = User::find(10)->post;
//    foreach ($posts as $value) {
//        echo "This Post made by User ID : {$value->user_id} <br>";
//        echo "Intro: " . $value->intro . "<br>";
//        echo "Article: " .$value->article . "<br>";
//        echo "Tags: " .$value->tag . "<br><br><br>";
//    }

//    $contacts = User::find(10)->contact;
//    var_dump($contacts);

//    $contact = Contact::find(4)->user;
//    var_dump($contact);

//    $users = User::where('age', '<', 28)->take(2)->get();
//    foreach ($users as $user)
//    {
//        var_dump($user);
//    }
    

//    $user = User::find(2);
//    $user->username = 'babu';
//    $user->save();
//    
//    return 'Saved!';

//    $users = User::where('age', '=', 27)->get();
//    foreach ($users as $user) {
//        var_dump($user);
//    }

    
//    $user = new User();
//    $user->username = 'NewUser';
//    $user->password = password_hash('pass', PASSWORD_BCRYPT);
//    $user->token = 'kljhnmbgfvcdsazxwetpouytresdfhjkmnbbvcdsxza';
//    $user->age = 27;
//    $user->created_at = time();
//    $user->updated_at = time();
//    
//    $user->save();
//    return 'Saved NewUser';

     
//    $users = User::where('age', '>', 17)->take(2)->get();
//    foreach ($users as $user)
//    {
//        var_dump($user->username);
//    }

   // $contact = Contact::all();
   // $usercontacts = Contact::find(1);
//   foreach ($contact as $value) {
//       echo "Contact ID = " . $value->id . "<br>";
//       echo "User ID = " . $value->user_id . "<br>";
//       echo "Address = " . $value->address . "<br>";
//       echo "Country = " . $value->country . "<br>";
//       echo "Phone = " . $value->phone . "<br><br><br>";
//       //var_dump($value) . "<br>"; 
//       
//   }
    
    
//Hash::make('yourpassword');
//Hash::check('yourpassword', $hashedPassword);
//Hash::needsRehash($hashedPassword);
//
//Auth::check();
//Auth::user();
//Auth::attempt(array('email' => $email, 'password' => $password));
//
//Auth::attempt($credentials, true);
//Auth::once($credentials);
//Auth::login(User::find(1));
//Auth::loginUsingId(1);
//Auth::logout();
//Auth::validate($credentials);
//Auth::basic('username');
//Auth::onceBasic();
//Password::remind($credentials, function($message, $user){});

//mail class
//Mail::send('email.view', $data, function($message){});
//Mail::send(array('html.view', 'text.view'), $data, $callback);
//Mail::queue('email.view', $data, function($message){});
//Mail::queueOn('queue-name', 'email.view', $data, $callback);
//Mail::later(5, 'email.view', $data, function($message){});
//Mail::pretend();






