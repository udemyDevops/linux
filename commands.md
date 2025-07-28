* check the details of a process
```
ps -ef | grep <process name>
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

* mount the partion to selected directory... before mounting move the data in the directory to another directory to backup, cuz any existing data in the directory will not be visible when the partition is mounted to the directory. So by taking backup the data can be copied back once the partition is unmounted 
```
mount <partition name> <directory path>
```
  eg: mount /dev/xvdf1 /var/www/html/images
