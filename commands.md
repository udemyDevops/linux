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
