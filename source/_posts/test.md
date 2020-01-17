---
title: PHP入门
date: 2019-07-12 10:09:45
tags: 入门
categories: PHP
---
## 前言
第一篇博客把以前写的复制粘贴过来。
粗略记录一些PHP语法，以后写详细一点
<!-- more -->
## 内建函数
- print_r() 打印数组
- var_dump()打印数据类型
- strlen()计算字符串长度
```
<?php
$a="dhjakfl"
//md5($a)将$a内容进行MD5加密
echo "变量a经过MD5加密后输出：</br>".md5($a)."</br>";
$b="a4jkls";
echo "变量b的字符长度为：".strlen($b)."</br>;
?>
```
## 自定义函数
- 自定义函数以“function”开头：
function 函数名(){
代码块；｝
- 如需返回值，改成return语句。
function 函数名(){
代码块；
return $value;｝
```
<?php
function Student($name,$achievement){
if ($achievement>=80){
echo $name."考了".$achievement."分，可以过个好年了！！！</br>";
}else{
echo $name."考了".$achievement."分，不知道回家会不会挨打啊！！！</br>";
 }
}
Student("小敏",80);
Student("小娟",50);
Student("小杨",75);
Student("小明",99);
?>
```

## 日期
- date()函数用于对日期或时间进行格式化
- date_default_timezone_set("PRC")设置时间区

```
<?php
date_default_timezone_set('PRC'); //设置中国时区
echo "今天是".date("Y-m-d")."现在时间是".date("h:i:sa")."<>/br";
//strtotime()用来创建日期 但不完美
$d1=strtotime("December 31");
$d2=ceil(($d1-time())/60/60/24）;
echo "距离12月31号还有：".$d2."天<"; 
//输出周六的日期					 
$stratdate = strtotime("Saturday");
$enddate=strtotime("+6 weeks",$stratdate);
while ($stratdate<$enddate) { 	
echo date("M d",$stratdate)."<br>"; 
$stratdate=strtotime("+1 week",$stratdate);
 }
?>
```
## 类
- 类的变量成员为“属性”。变量前加关键字public/protected/private
- 类的成员方法,通过$this->property(property是属性名字)访问类的属性、方法，但是要访问类的静态属性或者在静态方法里
- PHP定界符的作用是按原格式输出在其内部的，任何特殊字符都不需要转义，定界符中的变量会被正常用值代替
```
<?php
//创建一个Student类
class Student{
//属性声明为共有的
public $a='sdfs';
public $b=array("a","b",3);
//php定界符 这里为AAA为定界标识符 里面的内容全部输出
public $c=<<<AAA
hello world
AAA;
//结束标识符 行手写且单占一行除了后面跟；结尾
}
$A =new Student();
print_r($A->b);
echo "</br>";
echo $A->a."</br>",$A->c;
?>
```
## 构造析构函数
_construct()构造函数，用来初始化对象
_destruct()析构函数，释放所暂用的内存
```
<?php 
class Car{
	function __construct(){
	print "构造函数被调用</br>";
	}
	function __destruct(){
		print "解析函数时被调用";
	}
}
$car = new Car();
//实例化时会自动调用构造函数
echo "使用后，准备销毁car对象</br>";
unset($car);//销毁时会调用解析函数
echo "</br>------分割线------</br>";
$car = new Car();
?>
```
## 访问控制
- 由关键字实现
public：类成员可以在任何地方被访问
protected：可以被其所在类的子类和父类访问
private：只能被所在类访问
__set当给不可访问或不存在属性赋值时被调用
__get读取不可访问或不存在属性时被调用
```
<?php 
class Student{
	//声明私有变量
	private $name;
	private $age;
	private $sex;
	//构造函数
    function __construct($name,$age,$sex){
    	$this->name=$name;
    	$this->age=$age;
    	$this->sex=$sex;
    }
    //对象无法访问私有属性，但是通过魔术方法可以改变这一点 __get() __set()
    function __get($proName){
    	return $this->$proName;
    }
    function __set($proName,$proValue){
      $this->$proName=$proValue;
    }
    //访问私有属性
    function may(){
    	  return "我叫：$this->name 年龄:$this->age 性别:$this->sex";
    }
    //析构函数用来释放内存
    function __destruct(){
    	echo "</br>运行结束，释放内存</br>";
    }
}
$A =new Student("白",22,"男");
echo $A->name."<br>";
echo $A->may();

?>
```
## 继承
```
<?php 
//创建父类Person
class Person{
	//创建父类方法
	function read($name){
		echo "[".$name."]喜欢三毛</br>";
	}
	function doIng($name){
		echo "[".$name."]喜欢打篮球</br>";
	}
}
//创建子类Student
class Student extends Person{
	//创建子类方法
	function eat($name){
		echo "[".$name."]喜欢糖</br>";
	}
	//当子类中有与父类同名的方法时，就会覆盖父类的方法
	function doIng($name){
		echo "[".$name."]喜欢打游戏</br>";
	}
}
$a = new Person();//创建父类对象
$H = new Student();//创建子类对象
$H->read("素白");//子类对象调用父类的方法
$H->eat("素白");//子类对象调用自己的方法
echo "------------我是分隔符-----------</br>";
$a->doIng("素白");//父类对象调用自己的方法
$H->doIng("素白");//子类对象调用与父类同名的方法
?>
```
## 条件判断
- if
```
<?php 
$a=1;
if (条件a){
代码块;}
if (条件b){
代码块;
}
?>
```
- if...else
```
<?php 
$a=1;
if (条件a){
代码块;}
else{
代码块;
}
?>
```
- if...elseif...else
```
<?php 
$a=1;
if (条件a){
代码块;}
elseif(条件b){
代码块;
}else{
代码块;
}
?>
```
- switch
```
switch(){
   case 条件a：...;
   break;
   case 条件b：...;
   break;
   default:...;}
   ```
 
## 大小写敏感
- 所有变量都对大小写敏感
- 所有用户定义的函数、类和关键词（例如if、else、echo）都不敏感
## 常量
- 定义常量用define (name,value,True/False)其中name是常量名称；第二个是常量的值；第三个对大小写是否敏感，默认为False敏感。
## 作用域
- global关键字可以使函数内变量成为全局变量
- static关键字可以用来保留函数内变量不被删除
## while循环
```
while
<?php  
$i=0;  //定义变量i并赋零
while ($i<10){  //当i<10时执行下列操作
	$i++; //i自加
	echo $i."</br>";输出i
}
?>
```
```
do...while
<?php
$i=0;  //定义变量i并赋零
do {
	$i++; //i自加
	echo $i."</br>"; //输出i
}while ( $i<10 ) 
?>
```
## 结构嵌套
- 条件里套条件，循环里加循环。
- Foreach遍历每个元素并循环代码块，美进行一次循环，当前数组元素就会复制给$value变量，并且数组指针会逐一移动，直到最后一个数组元素。
 - 这里用到的数组是关联数组（foreach ($Olimpic as $key => $value)中key视为数组“下标”“value”是数组分量）
- 首次运行代码时，页面出现中文乱码，在代码首部加入"header('Content-Type: text/html; charset=utf-8');"后，恢复正常。
- foreach ($array as $value){
        待执行代码块；｝
```
-<?php
header('Content-Type: text/html; charset=utf-8');
$Olimpic = array( //创建数组
'2012' => "英国 伦敦",
'2008' => "中国 北京",
'2004' => "希腊 雅典",
'2000' => "澳大利亚 悉尼",
'1996' => "美国 亚特兰大",
'1992' => "西班牙 巴塞罗那",
'1988' => "韩国 汉城",
'1984' => "美国 洛杉矶",
'1980' => "苏联 莫斯科",
'1976' => "加拿大 蒙特利尔",
);
function Sj($Sj){
	global $Olimpic; //global将数组设为全局
	foreach ($Olimpic as $key => $value){
		if ($Sj==$key){ //取出数组的key值 与提交的时间做判断
			echo $Sj."年，奥运会在【".$value."】举行。</br>";
		}
	}
}
Sj(1996);
Sj(2008);
?>
```
##  数组
- array()函数用于创建数组。
- print_r()函数用于打印数组。
```
-索引数组
<?php
$a = array("1","2",3);
$b[0] = "1";
$b[1] = "2";
$b[2] = "3";
echo "第一种显示为：</br>";
print_r($a);
echo"<br>";
echo "第二种显示为：</br>";
print_r($b)."</br>";
?>

```

```
关联数组
<?php
$a = array("A"=>"19","B"=>"14","C"=>"11");
$b['A'] = "19";
$b['B'] = "14";
$b['C'] = "11";
echo "第一种显示为：</br>";
print_r($a);
echo"<br>";
echo "第二种显示为：</br>";
print_r($b)."</br>";
?>
```
## 分页
```
header("Content-type:text/html; charset=utf-8");
//连接数据库
$link = mysql_connect("127.0.0.1","root","123456");
//选择数据库，连接fy数据库（是自己创建的数据库吧），失败则执行die语句

mysql_select_db('fy',$link) or die('数据库连接失败')；
//设置页面
$page=2;
//设置每页显示数据个数
$pagesize=2;
//计算每页第一个数据在数据库中的序数
$pagestart=($page-1)*$pagesize;
//数据库命令 limit(x,y) 查询从第x往后取y个
$select = mysql_query("select*from fyl limit $pagestart,$pagesize");
$data=array();
//将表中数据通过数组的形式打印出来
	while($row = mysql_fetch_array($select,MYSQL_ASSOC)){
		$data[]=$row;
	}
	echo '<pre>';
	print_r($data);
	echo '</pre>';
?>
```
## 访问控制
```
<?php
class student{
	//声明私有属性
	private $name;
	private $age;
	private $sex;
	//构造函数
	function_construct($name,$age,$sex){
		$this->name=$name;
		$this->age=$age;
		$this->sex=$sex;
	}
	//对象无法直接访问私有属性,但通过魔法方法可以改变这点__get() __set()
	function __get($proName){
		return $this->$proName;
	}
	function __set($proName,$proValue){
		$this->$proName=$proValue;
	}
	//通过函数访问私有属性
	function say(){
		return"我叫:$this->name 年龄:$this->age 性别：$this->sex"
	}
	//析构函数用来释放内存
	function __destruct(){
			echo"</br>运行结束，释放内存</br>"
	}
}
$A = new student("ss","dd","xx");//创建对象
echo $A->name"<br>"; //直接调用私有属性
echo $A->say();//调用函数访问私有属性

?>
```
## 正则表达函数
```
 <?php 
header("content-type:text/html;charset=utf-8");
date_default_timezone_set("PRC");
//需要匹配的字符串。date函数返回当前时间
$content = "今天是".date("Y-m-d h:i a").",天气不错.</br>";
echo $content;//输出原句与结果做对应
//preg_match()函数只做一次匹配，最终返回0或1的匹配结果数$matches[0]将包含于整个模式匹配的文本
if (preg_match("/\d{4}-\d{2}-\d{2} \d{2}:\d{2} [ap]m/",$content,$matches))
{
	echo '匹配的时间是：'.$matches[0]."</br>";
}
//由于时间的模式明显，也可以简单的匹配
if(preg_match("/([\d-]{10}) ([\d:]{5} [ap]m)/",$content,$matches )){
	echo "当前的日期是：".$matches[1]."\n";
	echo "当前的时间是：".$matches[2]."\n";
}      
?>
//////
<?php 
header("content-type:text/html;charset=utf-8");
//preg_replace(正则表达式，替换成，字符串，最大替换次数默认为所有，替换次数)   
$a="放学铃响了，小明背起小明的书包回家去了！";
$b=preg_replace("/小明/","小白",$a);
$c=preg_replace("/小明/","小白",$a,1); 
echo $a."</br>";
echo $b."</br>";
echo $c;
?>

```
## 匹配
```
<?php 
header("content-type:text/html;charset=utf-8");
//匹配实例
$user = array(
	'name' =>'spawww',
	'email' =>'ssss@kss.com',
	'moblie' =>'19998887722'
);
//进行一般性的验证
if(empty($user)){
	die('用户信息不能为空');
}
if(strlen(strlen($user['name'])<6)){
	die("用户名长度最少为6位");
}
//用户名必须为数字字母、数字、下划线
if(!preg_match('/^\w+$/i', $user['name'])){
	die("用户名不合法");
}
//验证邮箱格式是否正确
if(!preg_match('/^[\w\.]+@\w+\.\w+$/i',$user['email'])){
	die('邮箱不合法');
}
//手机号必须为11位的数字，且一1开头
if(!preg_match('/^1\d{10}$/i', $user['moblie'])){
	die('手机号不合法');
}
echo '用户信息验证成功';
?>

```
## 验证码
```
<?php
//imagecreatetruecolor(x_size,y_size) 生成图片
$img = imagecreatetruecolor(100,40);
//在画布上生成颜色
$black = imagecolorallocate($img,0x00,0x00,0x00);
$green = imagecolorallocate($img,0x00,0xFF,0x00);
$white = imagecolorallocate($img,0xFF,0xFF,0XFF);
imagefill($img,0,0,$white);
//生成随机的验证码
$code ='';
for($i = 0;$i<4;$i++){
	$code .= rand(0,9);
}
imagestring($img,5,35,10,$code,$black);
//添加像素点干扰,在随机的位子上出现黑色和绿色的点
for($i=0;$i<50;$i++){
	imagesetpixel($img,rand(0,100),rand(0,100),$black);
	imagesetpixel($img,rand(0,100),rand(0,100),$green);
}
//输出验证码
header("Content-type: image/png");//通知浏览器这不是文本而是图片
imagepng($img);//生成png格式的图片输出给浏览器
imagedestroy($img);//销毁图像资源，释放画布占用的空间
?>
```
## COOKIE与SESSION
- COOKIE与SESSION本质都是实现用来识别用户
```
setcookie('name','value',time()+60,'/');//创建cookie，时间为60秒
setcookie('name','',time()-1,'/');//销毁COOKIE

session_start();//使用session之前必须开启
$_SESSION['username'] = 'zhangsan';
$_SESSION['password'] = 123;
unset($_SESSION['username']);删除session
session_destroy();销毁

```
## 文件
```
  include 'filename';//文件包含，出错后继续执行后续代码
  require 'filename';//文件包含，出错后不执行后续代码
  readfile('a.txt');//直接读出文件内容
  file_get_contents($filename);//原样获取文件内容
  file_put_contents($filename, $data);//覆盖写入原来的内容or没有文件会自动创建写入文件
  fopen($filename, $mode);//返回资源句柄 mode='r'是只读模式，'r+'是读写模式，'w'写模式如文件不存在可自动创建，'a'累加写
  fwrite($handle, $string); //向文件写入字符串
  fseek($handle, $offset);//将指针指向offset
  fread($handle, $length);//读length个字节
  fclose($handle);//关闭资源
   
  pathinfo($path);//返回文件路径的信息
  basename($path);//返回路径中的文件名部分
  dirname($path);//返回路径中的目录部分
  http_build_query($query_data);//生成URL-encode之后的请求字符串
  parse_url($url);//解析URL返回其组成部分
  parse_str($str);//将字符串解析成多个变量
  file_exists($filename)//检查文件或目录是否存在
  is_file($filename);//判断给定文件名是否为一个正常的文件
  is_dir($filename);//判断给定文件名是否是一个目录
  is_writeable($filename);//判断给定的文件名是否可写
  is_readable($filename);//判断给定文件名是否可读
  is_executable($filename);//判断给定文件名是否可执行
  chmod($filename, $mode);//0777  r w x   最大模式
  
  mkdir($pathname);//mkdir('test/a/b/c',0777,true)创建重复文件夹
  rmdir($dirname);//删除
  opendir($path);打开目录句柄
  readdir();从目录句柄中读取条目
  closedir();closedi
  unlink($filename);//删除文件
  copy($source, $dest);//拷贝文件
  rename($oldname, $newname);//重命名
  
  //递归删除文件夹
  rm('test');
  function rm($path)
  {
      $dir=opendir($path);
      readdir($dir);
      readdir($dir);
      while($newFile=readdir($dir)){
          $newPath=$path.'/'.$newFile;
          if (is_file($newPath)){
              unlink(newPath);
          }else {
              rm($newPath);
          }
      }
  closedir($dir);
  rmdir($path);
  }
  
```
## PHP链接mysql
```
$link = mysqli_connect('localhost','root','123456');//连接数据库
if(!$link){exit('数据库链接失败')}；//判断是否链接成功
mysqli_set_charset($link,'utf8');//设置字符集
mysqli_select_db($link,'dbsname');//选择数据库
$sql = "select *from bbs_user";//准备sql语句，这里用查询
$res = mysqli_query($link , $sql);//发送sql语句
$result = mysqli_fetch_assoc($res);//处理结果集,每次只读一条数据，指向下一条
mysqli_close();//关闭数据库 
```