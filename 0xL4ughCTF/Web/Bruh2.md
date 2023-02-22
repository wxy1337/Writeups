# Bruh2

![](images/2023-02-22-21-42-29.png)
```php
<?php

$servername = "127.0.0.1";
$username = "ctf";
$dbname = "login";
$password = "ctf123";

// Create connection
$conn = new mysqli($servername, $username, $password,$dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

if(!empty($_GET['username']) && !empty($_GET['password']))
{
    $username=mysqli_real_escape_string($conn,$_GET['username']);
    $password=mysqli_real_escape_string($conn,$_GET['password']);
    if (preg_match("/admin/i",$username) && $_SERVER['REMOTE_ADDR']!=="127.0.0.1")
    {
        die("Admins login are allowed locally only");
    }
    else
    {
        $res=$conn->query("select * from users where username='$username' and password='$password'"); # admin admin
        if($res->num_rows > 0)
        {
            $user=$res->fetch_assoc();
            echo ($user['username']==="admin")?"0xL4ugh{test_flag}":"sorry u r not admin";
        }
        else
        {
            echo "Error : Wrong Creds";
        }

    }
}
else
{
    echo "Please Fill All Fields";
}
?>
```    

和Bruh(Basic)相比可以看出在username的匹配中

```php
if (preg_match("/admin/i",$username) && $_SERVER['REMOTE_ADDR']!=="127.0.0.1")`
```

加入了修饰符i所以大小写是相同的（a和A相同），然而许多sql中默认有latin1字符集，很多字符都可以表示a如`å`，`Á`，`à`

*参考[Latin1字符集](https://www.shuzhiduo.com/A/ZOJP1RbE5v/)*

故测试输入
```
?username=àdmin&password=admin
```
![](images/2023-02-22-21-52-27.png)

**0xL4ugh{My_Broo_Ag@in_fREE_pALESTINE}**

![](images/2023-02-22-21-53-23.png)