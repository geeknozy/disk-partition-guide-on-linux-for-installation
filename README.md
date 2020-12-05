## Disk-partition-guide-on-linux-for-Arch-Linux-installation on UEFI devices.

NOTE: Im using fdisk utility to partition the disk.

1. Open Your terminal and type

    ```fdisk -l```

2. Now you see the list of storage devices on your system.
   Select the device as below command.
   
   ```fdisk /dev/sdX```
   
   Note X here represents the disk alphabet. X may be sda/sdb/nvmep01/etc...

NOTE: https://wiki.archlinux.org/index.php/Installation_guide#Partition_the_disks refer this for partition scheme table. 

3. Now Follow below steps.

    ```d``` -> hit d and select partition number until all the partitions are 

    ```g``` -> creates new gpt label for disk.

    ```n``` -> new partition
    
    ```hit from 2048---end``` -> starting sector.
    
    when fdisk asks for +/-/ end type
    
    ```+512M``` -> EFI partition size of 512MB (At least 260 MiB ) 
    
    hit yes for removing signature of existing partitons.
    
    ```t``` -> to change the type of the partition
    -> select partition number 1,2,3 etc. 
    
    ```L``` to list types -> select 1 - EFI 
    
    
    
