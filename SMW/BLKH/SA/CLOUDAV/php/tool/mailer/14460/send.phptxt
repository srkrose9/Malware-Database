<?php
error_reporting(0);
date_default_timezone_set($_POST['config']['time_zone']);
$required = array(
	'letter','to','subject','header','config', 'note'
);
foreach ($required as $key => $value) {
	if ( !empty($_POST[$value]) ){
		$count[] = $_POST[$value];
	}
}
if(count($count) != count($_POST) || count($required) != count($count)){
	$status =  json_encode(array(
		'status'  => false,
		'message' => 'ada data yang kosong'
	));
	die($status);
}

$_POST['header']['header']['Date'] 		= date("r (T)");

foreach ($_POST['header']['header'] as $key => $value) {
	$headers[] = $key.": ".$value; 
}

//die(print_r($headers));

if( mail($_POST['to'], $_POST['subject'], base64_decode($_POST['letter']) , implode("\r\n", $headers)) ){
	$status =  json_encode(array(
		'subject' => $_POST['subject'],
		'status'  => true,
		'message' => 'Sukses',
		'note' 	  => $_POST['note'],
	));
}else{
	$status =  json_encode(array(
		'status'  => false,
		'message' => 'Gagal',
		'note' 	  => $_POST['note'],
	));
}
if($status){
	die($status);
}else{
	$status =  json_encode(array(
		'status'  => false,
		'message' => 'Kesalahan Server'
	));
	die($status);
}
?>
