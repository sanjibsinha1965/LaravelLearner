# All codes related to chapter 4 - Routing 

Route::get('/', function()
{
	return View::make('home.index');
});

Route::get('/', function()
{
	return View::make('Hello, welcome guest.');
});

## For version Laravel 3.2
Route::controller(Controller::detect());
## Next for laravel 4.2 Onwards
Event::listen('404', function()
{
	return Response::error('404');
});

Event::listen('500', function()
{
	return Response::error('500');
});

Route::filter('before', function()
{
	// Do stuff before every request to your application...
});

Route::filter('after', function($response)
{
	// Do stuff after every request to your application...
});

Route::filter('csrf', function()
{
	if (Request::forged()) return Response::error('500');
});

Route::filter('auth', function()
{
	if (Auth::guest()) return Redirect::to('login');
});

Route::filter('before', function()
{
	return 'Hello.';
});

Route::filter('auth', function()
{
	if (Auth::guest())
    return Redirect::to('login');
});


The code of 'index.blade.php' now looks like this:

<!DOCTYPE html>
<html lang="en">

<head>

    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="">
    <meta name="author" content="">

    <title>Full Width Pics - Start Bootstrap Template</title>

    <!-- Bootstrap Core CSS -->
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- Custom CSS -->
    <link href="css/full-width-pics.css" rel="stylesheet">

    <!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!--[if lt IE 9]>
        <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
        <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->

</head>

<body>

    <!-- Navigation -->
    <nav class="navbar navbar-inverse navbar-fixed-top" role="navigation">
        <div class="container">
            <!-- Brand and toggle get grouped for better mobile display -->
            <div class="navbar-header">
                <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1">
                    <span class="sr-only">Toggle navigation</span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </button>
                <a class="navbar-brand" href="#">Start Bootstrap</a>
                
            </div>
            <!-- Collect the nav links, forms, and other content for toggling -->
            <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
                <ul class="nav navbar-nav">
                    <li>
                        <a href="#">About</a>
                    </li>
                    <li>
                        <a href="#">Services</a>
                    </li>
                    <li>
                        <a href="#">Contact</a>
                    </li>
                </ul>
            </div>
            <!-- /.navbar-collapse -->
            <img class="img-responsive img-center" src="img/intro-bg.jpg" alt="">
        </div>
        <!-- /.container -->
    </nav>

    
    <!-- jQuery -->
    <script src="js/jquery.js"></script>

    <!-- Bootstrap Core JavaScript -->
    <script src="js/bootstrap.min.js"></script>

</body>

</html>

I add a GET functionality as before; and the code is like this:
Route::get('home/about', function()
{
	return View::make('home.about');
});

The code is like this:

<!DOCTYPE html>
<html lang="en">

<head>

    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="">
    <meta name="author" content="">

    <title>Full Width Pics - Start Bootstrap Template</title>

    <!-- Bootstrap Core CSS -->
    {{ HTML::style('css/bootstrap.min.css') }}
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- Custom CSS -->
    {{ HTML::style('css/full-width-pics.css') }}
    <link href="css/full-width-pics.css" rel="stylesheet">

    <!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!--[if lt IE 9]>
        <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
        <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->

</head>

<body>

    <!-- Navigation -->
    <nav class="navbar navbar-inverse navbar-fixed-top" role="navigation">
        <div class="container">
            <!-- Brand and toggle get grouped for better mobile display -->
            <div class="navbar-header">
                <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1">
                    <span class="sr-only">Toggle navigation</span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </button>
                
                
            </div>
            <!-- Collect the nav links, forms, and other content for toggling -->
            <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
                <ul class="nav navbar-nav">
                    <li>
                        {{ HTML::link('/', 'Start Bootstrap') }}
                    </li>
                    <li>
                        {{ HTML::link('home/about', 'About') }}
                    </li>
                    <li>
                        <a href="#">Services</a>
                    </li>
                    <li>
                        <a href="#">Contact</a>
                    </li>
                </ul>
            </div>
            <!-- /.navbar-collapse -->
        </div>
        <!-- /.container -->
    </nav>

    <!-- Full Width Image Header with Logo -->
    <!-- Image backgrounds are set within the full-width-pics.css file. -->
  

    <!-- Content Section -->
    <section>
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <h1 class="section-heading">Section Heading</h1>
                    <p class="lead section-lead">Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
                    <p class="section-paragraph">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquid, suscipit, rerum quos facilis repellat architecto commodi officia atque nemo facere eum non illo voluptatem quae delectus odit vel itaque amet.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Fixed Height Image Aside -->
    <!-- Image backgrounds are set within the full-width-pics.css file. -->
    <aside class="image-bg-fixed-height"></aside>

    <!-- Content Section -->
    <section>
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <h1 class="section-heading">Section Heading</h1>
                    <p class="lead section-lead">Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
                    <p class="section-paragraph">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquid, suscipit, rerum quos facilis repellat architecto commodi officia atque nemo facere eum non illo voluptatem quae delectus odit vel itaque amet.</p>
                </div>
            </div>
            <!-- /.row -->
        </div>
        <!-- /.container -->
    </section>

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <p>Copyright &copy; Your Website 2014</p>
                </div>
            </div>
            <!-- /.row -->
        </div>
        <!-- /.container -->
    </footer>

    <!-- jQuery -->
    <script src="js/jquery.js"></script>

    <!-- Bootstrap Core JavaScript -->
    <script src="js/bootstrap.min.js"></script>

</body>

</html>

//END OF ABOUT.BLADE.PHP CODE


You might have noticed one minor change in this code. Instead of using: 
<link href="css/bootstrap.min.css" rel="stylesheet">
I have used:
 {{ HTML::style('css/bootstrap.min.css') }}
 
 The code of 'contact.blde.php' page is like this:

//START CONTACT.BLADE.PHP PAGE

<!DOCTYPE html>
<html lang="en">

<head>

    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="">
    <meta name="author" content="">

    <title>Full Width Pics - Start Bootstrap Template</title>

    <!-- Bootstrap Core CSS -->
    {{ HTML::style('css/bootstrap.min.css') }}
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- Custom CSS -->
    {{ HTML::style('css/full-width-pics.css') }}
    <link href="css/full-width-pics.css" rel="stylesheet">

    <!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!--[if lt IE 9]>
        <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
        <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->

</head>

<body>

    <!-- Navigation -->
    <nav class="navbar navbar-inverse navbar-fixed-top" role="navigation">
        <div class="container">
            <!-- Brand and toggle get grouped for better mobile display -->
            <div class="navbar-header">
                <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1">
                    <span class="sr-only">Toggle navigation</span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                    <span class="icon-bar"></span>
                </button>


            </div>
            <!-- Collect the nav links, forms, and other content for toggling -->
            <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
                <ul class="nav navbar-nav">
                    <li>
                        {{ HTML::link('/', 'Start Bootstrap') }}
                    </li>
                    <li>
                        {{ HTML::link('home/about', 'About') }}
                    </li>
                    <li>
                        <a href="#">Services</a>
                    </li>
                    <li>
                        <a href="#">Contact</a>
                    </li>
                </ul>
            </div>
            <!-- /.navbar-collapse -->
        </div>
        <!-- /.container -->
    </nav>

    <!-- Full Width Image Header with Logo -->
    <!-- Image backgrounds are set within the full-width-pics.css file. -->


    <!-- Content Section -->
    <section>
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                <h1 class="section-heading">Contact Us</h1>
 <p class="section-paragraph">
                        <?php echo Form::label('email', 'E-Mail Address'). "<br>" . Form::text('email', 'Type E-Mail Address'); ?>
                        </p>
                         <p class="section-paragraph">
                        <?php echo Form::label('message', 'Your Query'). "<br>" . Form::textarea('email', 'Write Your Query'); ?>
                        </p>
                          <p class="section-paragraph">
                        <?php echo Form::label('submit', 'Submit'). "<br>" . Form::submit('Click Me!'); ?>
                        </p>
                        
                       </div>
            </div>
        </div>
    </section>

    <!-- Fixed Height Image Aside -->
    <!-- Image backgrounds are set within the full-width-pics.css file. -->
    <aside class="image-bg-fixed-height"></aside>

    

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <p>Copyright &copy; Your Website 2014</p>
                </div>
            </div>
            <!-- /.row -->
        </div>
        <!-- /.container -->
    </footer>

    <!-- jQuery -->
    <script src="js/jquery.js"></script>

    <!-- Bootstrap Core JavaScript -->
    <script src="js/bootstrap.min.js"></script>

</body>

</html>

//END OF CONTACT.BLADE.PHP PAGE


Not a bad looking page! The trick is, I have used the form generating codes of laravel in the container section. Look at this part:

 <?php echo Form::label('email', 'E-Mail Address'). "<br>" . Form::text('email', 'Type E-Mail Address'); ?>
                        </p>
                         <p class="section-paragraph">
                        <?php echo Form::label('message', 'Your Query'). "<br>" . Form::textarea('email', 'Write Your Query'); ?>
                        </p>
                          <p class="section-paragraph">
                        <?php echo Form::label('submit', 'Submit'). "<br>" . Form::submit('Click Me!'); ?>
                        </p>


In Laravel 4.2, we can write down the route logic like this:




Route::get('/', function()
{
	return View::make('hello');
});

Route::get('/contact', function()
{
	return View::make('contact'); 
});



