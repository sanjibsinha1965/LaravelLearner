# HomeController.php #

interface HomeInterface {
    public function Home();   
    public function User($userid);
    public function test();
    public function Regis();
    public function Login();
    public function hello();
}

class HomeController extends BaseController implements HomeInterface {

    public $_ID;
    public $layout = 'home.layout';
    

    public function Home(){
            
            $users = DB::table('users')->get();
            $view = View::make('home.default')->with('users', $users); 
            $this->layout->title = 'Contact Title';
            $this->layout->csscore = 'css/bootstrap.min.css';
            $this->layout->cssround = 'css/round-about.css';
            $this->layout->content = $view; 
           
       }     
       
       public function User($userid) {
           
            $this->_ID = $userid;
            $id = User::find($this->_ID);
            $view =  View::make('home/contact', compact('id')); 
            $this->layout->title = $id->username;
            $this->layout->csscore = '/css/bootstrap.min.css';
            $this->layout->cssround = '/css/round-about.css';
            $this->layout->content = $view;                   
           
       }
       
       public function test(){        
          
          return Redirect::to('test'); 
           
       }
       
       public function hello(){        
          
          return View::make('test.hello'); 
           
       }
       
       public function Regis(){
           
            $view = View::make('home.regis'); 
            $this->layout->title = 'Login Title';
            $this->layout->csscore = '/css/bootstrap.min.css';
            $this->layout->cssround = '/css/round-about.css';
            $this->layout->content = $view;          
           
       }
       
       public function Login(){
            
            $view = View::make('home/login'); 
            $this->layout->title = 'Logout Title';
            $this->layout->csscore = '/css/bootstrap.min.css';
            $this->layout->cssround = '/css/round-about.css';
            $this->layout->content = $view;          
           
       }
       
       
    
 

}
