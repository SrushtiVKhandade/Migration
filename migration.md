### Migration
Data from one region to another using snapshot
migration of data through replication
 
make three instance using three ami's with same key and security group
inbound rules-nfs
connect machine in terminal
rum commands 
aws-sudo su -
yum update -y
cat /etc/os-release
rpmquery nfs-utils
 
redhat->sudo su -
cat /etc/os-release
yum install nfs-utils
 
ubuntu->
sudo su -
cat /etc/os-release
apt update
apt install nfs-common
 
go to efs-
create file system
open file system
network
manage
add security 
group that we have made
attach efs file
mount via ip
check region with instance
 
go to node3(ubuntu)
mkdir /nfs-data
paste mount command frm efs 
replace efs with /nfs-data in command
cd /nfs-data
make file -touch
 
go to node2
mkdir /efs-data
mount.........../efs-data
cs /efs-data/
touch file

make another instance in region where you want to replicate
make file system
disable file protection from edit
 
go in previous region replicate file
in existing file system
select zone
browse and select file system created in 2nd efs
replicate
after replication attach efs to instance by mount via ip command after makinf directory in new instance
check by df -h








Create 3 instances (linux , redhat , ubuntu )
2 instances can have one availability zone: eg :1a and 1 instance can have a different availability zone: eg: 1b
#edit security group: add nfs 2049

After creating instances open your terminal:
Linux : 
Cat /etc/os-release
Rpmquery nfs-utils
Mkdir /nfs-data
#go to your aws console : 
Open EFS > new file system > refresh > sec group - add your own secgroup inplace of default > edit disable file protection > attach
Sudo mount ….. /nfs-data/
Df -h
Cd /nfs-data/
Touch glenn.txt{1..10}
Ll
Now open Redhat instance  :
Cat /etc/os-release
Yum install nfs-utils -y
Rpmquery nfs-utils
Mkdir /efs-data
Sudo mount ….. /nfs-data/
Df -h
Cd /nfs-data/
Touch glenn.txt{1..10}
Ll
Ubuntu:
Apt update 
Apt install nfs-common
Mkdir /remote-data/
Sudo mount /remote-data/
Ll

Go on your aws : 
Choose a new region and a create a new instance 
Create a fs and disable fsp > go to networking and check security group , chose the sec group you assigned
#inbound rules : add nfs 2049 
Go to old region > create replica >choose dest >browse efs >create replica
Go to your terminal 
Df -h
Mkdir /data-mum
Sudo mount 
Cd /data-mum
Ll
