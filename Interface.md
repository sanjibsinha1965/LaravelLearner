
# How Interface Works 

class ConnectionRepositoryClass {
    
    /**
     * MySQL connection
     *
     * @var resource  Database connection using the MySQL original extension.
     */
    //protected $_connection;

    /**
     * Creates a database connection using the MySQL original extension.
     *
     * @param string $host  Database server name.
     * @param string $user  Database user account.
     * @param string $pwd   User account password.
     * @param string $db    Name of database to connect to.
     * 
     */
    protected $host;
    protected $user;
    protected $pwd;
    protected $db;
    
    public function __construct() {
        
        $this->host = 'localhost';
        $this->user = 'root';
        $this->pwd = 'pass';
        $this->db = 'sanjib';
        
    }
    
}
//end of ConnectionRepositoryClass.php

Secondly I get the 'ConnectionClass' in which I have two methods: one connects and other retrieves. The code is like this:


include 'ConnectionInterface.php';
include 'ConnectionRepositoryClass.php';

class ConnectionClas extends ConnectionRepositoryClass implements ConnectionInterface {

    
    protected $table_name;
    protected $attribute_name;


    public function __construct() {
        
        parent::__construct();
        
    }


    public function Connection() {
        
        if (mysql_connect($this->host, $this->user, $this->pwd)){
            if (mysql_errno()) {
              throw new RuntimeException('Cannot access database: '.mysql_error());
            }
            else {
              mysql_selectdb($this->db);
            }
            return 'Connected' . '<br>';
      
        }
        else {
            return 'Database cannot be accessed'; 
        }
      
      }
      //return $con;

      public function getTable($table_name, $attribute_name) {
          
          $this->table_name = $table_name;
          $this->attribute_name = $attribute_name;
        
        $cat = mysql_query("SELECT *
        FROM `{$table_name}`
        LIMIT 0 , 30");
        if (!$cat){
            die ('Error');
        }
        //since we dont want to exit the loop without having</br>
        //all the table names, so we get our results in an array</br>
        $results = array();
        while ($row = mysql_fetch_array($cat)) {
            $results[] = $row["{$attribute_name}"];
        }
        //now it is time to go outside the loop and return all table names</br>
        return $results;
        
    }
}
//end of ConnectionClass

Next the contract: ConnectionInterface. The code is like this:


 interface ConnectionInterface {
     
     public function Connection();
     public function getTable($table_name, $attribute_name);
   
}
//end of ConnectionInterface

Next two small classes which is underdeveloped as we just need them to get the data from two tables: users and tasks.
First UserClass and the second is TaskClass, and the code is like this:
<?php 
class TaskClass extends ConnectionClas {  
}
//end of TaskClass
<?php
class UserClass extends ConnectionClas {   
}
//end of UserClass

And finally we need to instantiate the connection, user and table objects like this:


// Require the configuration before any PHP code as the configuration controls error reporting:
require('./Bengaliana/includes/config.inc.php');
require './Bengaliana/Connection/TaskClass.php';
require './Bengaliana/Connection/ConnectionClass.php';  
       $con = new ConnectionClas();
        echo $con->Connection();
        $user = $con->getTable('users', 'username');
        foreach ($user as $value) {            
            echo $value . '<br>';    
        }          
         $conn = new ConnectionClas();
         echo $conn->Connection();
        $task = new TaskClass();
        $tasks = $task->getTable('tasks', 'title');
        foreach ($tasks as $value) {            
            echo $value . '<br>';    
}
//end of code


