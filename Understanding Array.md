# Understanding Array

## First a commonfunction.php in my 'lib' folder

//code starting
class myArray implements ArrayAccess {<br></br>

    protected $array = array();<br></br>

    function  offsetSet($offset, $value) {<br></br>
        if(!is_numeric($offset)){<br></br>
            throw new Exception("Invalid key {$offset}") ;<br></br>
        }<br></br>
        $this->array[$offset] = $value;<br></br>
    }<br></br>

    function  offsetGet($offset) {<br></br>
        return $this->array[$offset];<br></br>
    }<br></br>

    function  offsetUnset($offset) {<br></br>
        unset ($this->array[$offset]);<br></br>
    }<br></br>

    function  offsetExists($offset) {<br></br>
        return array_key_exists($this->array, $offset);<br></br>
    }<br></br>

}<br></br>
//end of code

## Second arrayfunctions.php
//code starting
    include_once 'lib/commonfunction.php';<br></br>

$msg="";<br></br>
$msg=$_REQUEST['msg'];<br></br>
echo "{$msg}";<br></br>

mysql_connect('localhost', 'root', '');<br></br>
mysql_select_db('appababa');<br></br>

$query = mysql_query('SELECT * FROM comments');<br></br>

$obj = new myArray();<br></br>

while ($obj = mysql_fetch_array($query)) {<br></br>

    for ($i=0; $i<=$obj[0]; $i++){<br></br>
        $num=0;<br></br>
        $num=$i;<br></br>
        $num;<br></br>
    }<br></br>
}<br></br>
echo "Total number of comments : ".$num;<br></br>

$row = new myArray();<br></br>
$query1 = mysql_query("SELECT * FROM comments WHERE `comments`.`is_published`='Y'");<br></br>
$results = array();<br></br>
while ($row = mysql_fetch_array($query1)) {<br></br>
    $results[]=$row[0];<br></br>
    echo $row['description']." = "."&lt;a href='http://localhost/ClassesAndObjects/update.php?id={$row['id']}'&gt;UNPUBLISH&lt;/a&gt;";<br></br>
}<br></br>

echo "Total number of published comments : ".count($results);<br></br>

$row = new myArray();<br></br>
$query1 = mysql_query("SELECT * FROM comments WHERE `comments`.`is_published`='N'");<br></br>
$results = array();<br></br>
while ($row = mysql_fetch_array($query1)) {<br></br>
    $results[]=$row[0];<br></br>
    echo $row['description']." = ".&lt;a href='http://localhost/ClassesAndObjects/update1.php?id={$row['id']}'&gt;PUBLISH&lt;/a&gt;";<br></br>
}<br></br>

echo "Total number of published comments : ".count($results);<br></br>
//end of code

Next and finally two php file where I update comments table, ie; either publish it or unpublish it.
//code starting

$id = $_REQUEST['id'];<br></br>
mysql_connect('localhost', 'root', '');<br></br>
mysql_select_db('appababa');<br></br>
$query = "UPDATE  `appababa`.`comments` SET  `is_published` =  'N' WHERE  `comments`.`id` ='".$id."' LIMIT 1";<br></br>
$results = mysql_query($query);<br></br>
if($results){<br></br>
    //echo "Your comments successfully updated";<br></br>
    header('Location: http://localhost/ClassesAndObjects/arrayfunctions.php?msg="Your comments successfully unpublished"');<br></br>
}
 else {<br></br>
    echo "Failed! Try again.";<br></br>
}<br></br>

//update1.php<br></br>

$id = $_REQUEST['id'];<br></br>
mysql_connect('localhost', 'root', '');<br></br>
mysql_select_db('appababa');<br></br>
$query = "UPDATE  `appababa`.`comments` SET  `is_published` =  'Y' WHERE  `comments`.`id` ='".$id."' LIMIT 1";<br></br>
$results = mysql_query($query);<br></br>
if($results){<br></br>
    //echo "Your comments successfully updated";<br></br>
    header('Location: http://localhost/ClassesAndObjects/arrayfunctions.php?msg="Your comments successfully published"');<br></br>
}
 else {<br></br>
    echo "Failed! Try again.";<br></br>
}
</code>
<p>
    You change the database name and table accordingly. But to create a comments table like me I give the sql file below.
    You may run it and test it how it works
</p>
