


### Netstat

Netstat (Network Statistics) is a command used to know/print the connections established by the host and some details related to connections like protocol, local ip and port, foreign ip and port, state of connection, program id used for connection.
```
Flags
	- a => shows all the current active connection 
	- p => shows which program uses this connection ;in the form of program id
	- n => shows data in numeric form. without resolving hostname, fqdn, ports
	- l => shows the listening ports only
	- t => for tcp connection only
	- u => for udp connection only
	- x => for unix ports
	- s => print statistics for all protocols
	- r => routing information
	- i => interface information

```




### Telnet

Telnet is a command used to connect to remote host. It has low security as it uses clear plain text for communication. So, it is not much use. I can also be used to check if a port is open or not . It allows 2 way communication between hosts.




### Firewall




### ufw




### /etc/passwd

This file include users and its associated data.A whole single line describes about a user. This file contains :-
1. users
2. password
3. user id
4. group ids
5. user info
6. home directory
7. user shell (which is started when user login to the system)

### chmod




### chown




### top




### ps

#### running process


#### dead process





### useradd
This command is used to create a new user.
```
Flags:
- l => login (change username)
- u => user id
- s => shell
- a => append
- G => groups
- d => path to home directory
- g =>

```

![](Images/d4-useradd.png)

### userdel 
This command is used to delete a user.

![](Images/d4-userdel.png)


### usermod
This command is used to modify a user account.

![](Images/d4-usermod.png)








### sysytemctl




### journalctl








### Shell Scripting


Shell Script is an program which include list of commands which is used by the operating system (shell) to perform certain tasks for automation of tasks and testing purpose.
It is an interpreter based program.



### Questions

###  Create a user tom having sudo privilege and home directory as /home/tom.





###  Create user cat without sudo privilege and without home directory.




###  Create a file from user tom and edit it from cat user.




###  Write a script named helloworld.sh to display “Hello World”.




###  Write a script named display.sh to prompt for a number and display it.




###  Write a script to determine if a user-inputted number is positive, negative, or Zero.

