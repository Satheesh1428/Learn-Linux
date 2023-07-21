# Learn-Linux
SSH -i <Private key> usrname@ipaddress

PWD --present working directory 

CD: Change directory : CD /, CD..

ls : Listing :  ls -l, ls - lr, ls -lt, ls - ltr

touch : to create file : touch  <file name>

mkdir : to create directory : mkdir <directory name>              

cat : to write a data inside the existing empty file/ to create file and write content in file/ to replace existing content of file:  
       cat > (file name) + enter + write content + press (control+d ) command
      
      to view content in file cat (file name)

      to append contenet to existing contenet of file cat >> (file name)
      
      to merge files into another file: cat (file1) (file2) > (file3)

CP : to copy : cp (file/directoty)  (directory name)
     to copy recursivly cp -r (file/directoty)  (directory name)

MV: to cut and paste : mv (file/directoty)  (directory name)

rm : to remove directory rm (directory name)
     
     to remove directory recursively: rm -r (directory name)

grep: to find varaible  grep (variable name) (file name)

      to find varible without case sensitive grep -i  (variable name) (file name)

head  to find first 10 lines : head (filename)
  
      to find first n line  : head -n file name
tail  to find last 10 lines : tail (filename)
      to find last n line  : tail -n file name
****************************************************************************************************
*echo for printing on screen : echo (hi linux)                                                     *
*     echo $? is to find last command is success or not ( 0 --success, other than zero is failure) *
****************************************************************************************************
wget : to install softwares : wget (link)
       wget install : sudo yum install wget -y 

curl : to see text at run time on screen 

Ownership and permissions:
==========================
U -- User, G-- group, O-- Other

R-- Read value=4
W-- Write value=2
X-- execute value=1

chmod U+X filename -- to add / chmod U-X filename   -- to remove 
chmod r+X filename -- to add / chmod r-X filename   -- to remove 
chmod o+w filename -- to add / chmod o-w filename   -- to remove   etc

chmod 754  file name ( 4+2+1  4+1  4) 

chmod 400  file name  (4 0 0 )

=======================================================
VIM:

https://github.com/techworldwithsiva

Installing VIM : sudo yum install vim -y

Modes of VIM :

insert mode(i) <---------->  esc mode(esc) <------------> colon mode(:)

:/ search field   search from top 

:? search field   search from bottom

:set nu it will display the numbers
:set nonu it will remove numbers
:set ic it will do case sensitive
:set noic it will do no case sensitive
:noh -- don't highlight
:q -- to come out from file 
:wq + enter  --to come out from file with saving
:q!  to comeout from file with out saving written content 
:n  here n is any line number that we want to go 
i -- to write something in file 
for replace:
==========
:%S/target field name/replace name
:nS/target field name/replace name
:%S/target field name/replace name/g (meaning global)

In ESC mode: U-- undo, YY--yank/copy, dd--cut(nDD, p-- paste(nP) 

Processmanagement:
==================

assign a task  ---->  check the result ------> close the task  and repeat from begining 

Evry thing is process inside linux , for each task linux will create process id and fetch the results for us 

*TOP command to see the process id and to come out Q
* PS process from our terminal
*ps -e  to see all the process
*ps -ef to see all the process full details

PID ---process instance id, PPID -- Parent PID

FOREGROUND: which runs in the terminall itself-- slepp 20 
background: which runs in the background----sleep 20 &

ps -ef | grep (search filed name)

kill (PID )  -- REQUEST TO STOP THE PROCESS

Kill -9(PID) -- REQUEST TO STOP THE PROCESS WITH FORCE

User management:
====================
How to create user : Go to root ---> useradd < user name >

Seeting password :  passwd <username> + enter + password + retype password

read the user name : id  -- it will give current user info , root user id is "0" and other users ids are other than "0".
                     id <user name> it will give info about usrname given 
                     when we created the user with same user name group will be created as well .

		     Every user will have 2 groups: 1) Primary group 2) secondary groups

How can we see all the user infomation in the system? : VIM /ETC/PASSWD or getent passwd (for safe)


Group information:
=======================
How can we add group : groupadd <group name>
How can we get entried of group: getent group 

" Give access to the group and add users to group "

How to add user to group? 
            USERMOD -a -G <GROUP NAME> <USER NAME>  --- it will add to secondary groups
	    USERMOD -g <GROUP NAME> <USER NAME>  --- it will add to Primary group

How to remove user from gropup?
            GPASSWD  -d <USER NAME> <GROUP NAME>   -- it is working when user is added to secondary group, it won't work when it is added to primary group

if user wants to work in another group for few days : usermod -a -G <new group name> < username>

How to delete group ? groupdel <group name>.

User exit organization:
=======================
remove him from primary and secondary groups with 

usermod -g <user name> <username> -- user will be deleted from all teh groups
userdel <username> 

deleting group : groupdel <groupname>

User login process:

ssh username@ipaddress  -- 

Note:  by default linux will  allow users to login with private key , if we want to login with password we have to disable that approach

Step1:
we have to modify file vim /etc/ssh/sshd-config    -- passwordauthentication should be YES.
Step2: systemctl restart sshd
Step3: ssh username@ipaddress  then password


User joins the organiation:
============================
admin will ask him to give his public key 

then user will do ssh -keygen -f linux and then it will cretae to keys one is private and public key 

user will provide public key to admin 

su -linux this will do linux will become root

mkdir .ssh   --- chmod 700 .ssh -R 

cd .ssh/

touch authorized_keys

vim authorized_keys

cat linux.pub   -- it will show public key copy this key into authorized_keys

chmod 400 authorized_keys

exit -- it will make comeout from linux root

Now we are at root use 

now user will login with ssh -i linux linux@ipaddress   -- user can login with kumar user id now.


When new user trying to become root user it will ask password

then administrater will do sudo su - 
vim /etc/sudoers

at without password comments give as below 

linux  all=(all)  nopassword: ALL 

checking sudo yum install wget -y 

or 

usermod -a-G wheel linux   now user will have sudo access

set passwd linux 

checking sudo yum install wget -y 

Package management:
========================

yum -- yellow dog utility manager  earlier it is rpm-- redhat package management 

RPM :

for ex you want to install one game which runs on java .. 

step1: install jave
step 2: install the game

YUM: 

Install the game automatically YUM will understand the dependency and it will automatically install java 

How YUM is able to recognize dependencies?

/etc/yum.repos.d/

yum list installed -- it will give all the packages installed

yum installed | wc -l   -- it will give count 

yum list all 

yum update -y 

yum list available 

yum remove nginx


IN REDHAT /FEDORA package extension is RPM
