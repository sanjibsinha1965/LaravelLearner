# Anonymous Functions

<code>
        function hello()
        {
            echo "hello everyone";
        }
        //now call this function
        hello();
        //done, it will echo - hello everyone.
    </code>
    
    Every function in PHP return value. Whether you explicitly cause it or not.
    <code>
        function hello()<br></br>
        {<br></br>
            return "hello everyone";<br></br>
        }<br></br>
        //now call this function<br></br>
        echo hello();<br></br>
        //done, it will echo - hello everyone.<br></br>
    </code>
    <code>
        //let us see another example<br></br>
        function hello($you)<br></br>
        {<br></br>
            echo "I love {$you}";<br></br>
            if ($you == "12reach"){<br></br>
                return; //nothing is processed<br></br>
            }<br></br>
            echo ", what about you?";<br></br>
        }<br></br>
        //now call this function<br></br>
        hello("12reach"); // Displays I love 12reach<br></br>
        hello("PHP"); // Displays I love PHP, what about you?<br></br>

    </code>
</p>
<p>
Variable scope is very important. You may use $_GLOBAL super global array.
    <code>
        $a = "Hello";<br></br>
        $b = "Everyone";<br></br>
        function hello()<br></br>
        {<br></br>
            global $a, $b;<br></br>
            echo "$a $b";<br></br>
        }<br></br>
        hello(); // Displays "Hello Everyone<br></br>
    </code>
    You may write it this way.
    <code>
        $a = "Hello";<br></br>
        $b = "Everyone";<br></br>
        function hello()<br></br>
        {
        echo $GLOBALS['a'] .' '. $GLOBALS['b']<br></br>
        }<br></br>
        hello(); // Displays "Hello Everyone"<br></br>
    </code>
<br>
You can create a function, that accepts variable number of arguments. And it is extremely useful. 
<code>
    function reach() {<br></br>
    if (func_num_args ()>0){<br></br>
        $arg = func_get_arg(1);//<br></br>
        echo "You want to reach {$arg}";<br></br>
    }<br></br>
    else {<br></br>
            echo "12reach is want to reach!";<br></br>
        }<br></br>
    }<br></br>
    reach("12reach", ", or somewhere else?");//displays- You want to reach , or somewhere else?<br></br>

    reach();//Displays- 12reach is want to reach!<br></br>
</code>

//end of coding
