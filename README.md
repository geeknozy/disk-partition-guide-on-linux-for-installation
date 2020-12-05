## Disk-partition-guide-on-linux-for-Arch-Linux-installation on UEFI devices.

### THIS WILL ERASE DATA on Disk!!!

NOTE: Im using fdisk utility to partition the disk.

1. Open Your terminal and type

    ```fdisk -l```

2. Now you see the list of storage devices on your system.
   Select the device as below command.
   
   ```fdisk /dev/sdX```
   
   Note X here represents the disk alphabet. X may be sda/sdb/nvmep01/etc...

NOTE: https://wiki.archlinux.org/index.php/Installation_guide#Partition_the_disks refer this for partition table schema. 

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
    
    NEXT is Root partition.
    
    ```n``` -> new partition
    
    Hit enter for starting sector
    
    when fdisk asks for +/-/ end type

    ```-your RAM-size + 1G``` -> keep last part of your disk for SWAP partition. (Hibernate Support)
    
    ```4G``` or ```8G``` -> Common swap partition. (Without Hibernate support).
    
    hit yes for removing signature of existing partitons.
    
    This is the root partitions so it must be in Linux File System type.
    
    ```t``` -> to change the type of the partition
    -> select partition number 1,2,3 etc. 
    
    ```L``` to list types -> select 20 - Linux File System.
    
    NEXT is SWAP partition.
    
   ```n``` - > new partition.
   
    Hit enter for starting sector
    
    when fdisk asks for +/-/ end hit enter this is the last partition and end of disk.
    
    NOW to write the partition 
    
    ```w``` -> this will write partition 
    
    
    ### Disk-partitions-done now formatting.
    
1. For EFI Partition  

```mkfs.fat -F 32 /dev/sdX1```  
    
2. For root partition  

```mkfs.ext4 /dev/sdX2```
    
3. For Swap Partition.  

```mkswap /dev/sdX3```
    `                          
```swapon /dev/sdX3```
    
   
