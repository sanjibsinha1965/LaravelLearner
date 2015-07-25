# A contact page specimen #

   <?php 
//
   if (Auth::check()){ echo "<h1>Welcome</h1>"; ?>
       {{{Auth::user()->username}}}
       {{link_to('logout', 'Log Out')}}
   <?php } else {?>
     {{link_to('login', 'Log In')}}
<?php } ?> 
                <h1 class="page-header"><?php echo " Detail of " . $id->username ?></h1>
            </div>
                <?php 
                    echo "User ID : " . "<h2>" . $id->id . "</h2>";
                    echo "Username : " . "<h2>" . $id->username . "</h2>"; 
                    echo "Password : " . "<h2>" . $id->password . "</h2>"; 
                    echo "Token : " . "<h2>" . $id->token . "</h2>"; 
                    echo "Created AT : " . "<h2>" . $id->created_at . "</h2>";             
                 ?> 
