`ansible all -m ping` - module "ping" for check connection

`ansible all -m setup` - module "setup" print out all info about our servers from inventory files. In our case "all" - print information about all servers from inventory file "hosts"

`ansible all -m shell -a "uptime"` - this module "shell" execute shell commands on servers from inventory file hosts , option "-a" means 'argumenst', which we pass to our module "shell" for executiob on remote servers. In our case we execute "uptime" command.

`ansible all -m command` - exactly the same, as "shell" module, but it execute not from a remote shell of servers, so becaues of this, it`s module does not use environment varuables on remote machines and also shell operators

`ansible all -m copy -a "src=privet.txt dest=/home/ec2-user"` - this module "copy" just copy files or dirs to remote servers, where "-a" arguments, which include src i.e.source location of file and dest i.e. destination,where files to copy.(in our case to /home/ec2-user/ dir)

Error "Destination not writable" - this mistake means that we execute commnd on remote servers without sudo, since we need escallation of privileges for this operation copy to "/home/ec2-user/" dir. To fix it: `ansible all -m copy -a "src=privet.txt dest=/home/ec2-user mode=777" -b` - "mode" - set rwx(777) permission on file, "-b" argument menas "become" - escalation of privileges to 'root' (sudo) 

`ansible all -m file -a "path=/home/ec2-user/privet.txt state=absent"` - this module "file" designed for working with files(many many operations with files), in our case we try to remove file "privet.txt" from our servers, which registered in our inventory file "hosts"; "-a" means arguments, "path" - path to our file(full path), "state"it`s state for our file, in this case state is "absent" - it means that we want to remove remote file "privet.txt" 

`ansible all -m get_url -a url="https://collectors.sumologic.com/rest/download/linux/64 dest=/home/" -b` - this module "get_url" used when we need to download the file  from the Internet, where "url" - is an argument to which we pass URL-link, "dest" argument is used to pass the path where we save the downloaded file, "-b" - become sudo for escallation of privileges.

`ansible all -m yum -a "name=stress state=latest"` - this module "yum" designed for installation programms and tools on RedHat like systems, such as RedHat, Oracle, CentOS, Fedora and etc... Arguments 1) "name" -  specify packet name 2) "state" - install state, in our case is "latest", bacause we want to install latest version of tool.


`ansible all -m uri -a "url=http://www.adv-it.net return_content=yes"` - this module "uri" designed for reading content of web-resource. Argument "uri" - is url for web-resourсe, argument "return_content" with value = "yes" means that we want to get content of web-page.

`ansibla all -m service -a "name=httpd state=started enabled=yes" -b` - this module "service" designed for service managment(like systemd in Linux OS), argument "name" specify service name, in our case it is "httpd" - apache2, argument "state" specify state for service, in our case we need start our service, argument "enabled" means specify autostart state.

`ansible all -m shell -a "ls /" -v` - this module "shell" also execute shell commands on servers, but this example for debuging by "-v" option, you may use "-vv" or "-vvv" for advanced debugging commands


`ansible-doc -l` - list all available commands and modules for ansible



