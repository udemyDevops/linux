* check the details of a process
```
ps -ef | grep <process name>
```

* To see which process is using a directory
```
lsof <directory path>
```

* check the open ports opened for aa process
```
ss -tunlp | grep <process Id>
```

* check the available/connected hard disks
```
fdisk -l
```
* list the partitions mounted to respective hard disk
```
df -h
```
* create a partition in a disk
```
fdisk <disk name>
```
        eg: fdisk /dev/xvdf

        disk name --- name of the disk where the new partition is to be created.

- command mode for fdisk will open
- m -- help in fdisk utility, list of commands
- partion will be created using the commands but it is a raw volume and do not have any format (ext/xfs - popular in linux)
    xfs -- used for large volumes or faster I/O.... root volume
    ext -- used for general purpose
* list the available formats
```
mkfs
```
* format the partion with respective format
```
<format> <partition name>
```
        eg: mkfs.ext4 /dev/xvdf1

* mount the partion to selected directory... before mounting move the data in the directory to another directory to backup, cuz any existing data in the directory will not be visible/accessible when the partition is mounted to the directory. So by taking backup the data can be copied back once the partition is mounted.
```
mount <partition name> <directory path>
```
        eg: mount /dev/xvdf1 /var/www/html/images

- but this is a temporary mount meaning when the server is rebooted the mount point will be detached.
- To make a permanent mount, first unmount the directoty after checking no process is using the directory 'lsof' command
```
umount <directory path>
```
                eg: unmount /var/www/html/images
* To add a permanent mount
```
vim /etc/fstab
```
- add a new line in the file for the partition and directory in columns
```
<partion name>tab<directory path>tab<format>tab<defaults>tab<0 - for fsck>space<0 - for dump>
```
                eg: /dev/xvdf1        /var/www/html/images        ext4        defaults        0 0

- now the 'df -h' command will not show the mount point. fstab file should be reaad again to execute the entries
```
mount -a
```
- restart the respective service after completing the mount
- eg: systemctl restart httpd

* To detach the volume, first unmount the directoty after checking no process is using the directory 'lsof' command to check which process is using, 'kill' command to kill the process and also remove the line related to the directory in '/etc/fstab' file
