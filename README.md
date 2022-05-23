## Disk-partition-guide-on-linux-for-Arch-Linux-installation on UEFI devices.

### THIS WILL ERASE DATA on Disk!!!
----------------------------------------------------------------------------------------------------------
NOTE: Im using fdisk utility to partition the disk.

#### 1. Open Your terminal and type

    ```fdisk -l``` <br>
----------------------------------------------------------------------------------------------------------

#### 2. Now you see the list of storage devices on your system.
   Select the device as below command.
   
   ```fdisk /dev/sdX```
   
   Note X here represents the disk alphabet. X may be sda/sdb/nvmep01/etc...

NOTE: https://wiki.archlinux.org/index.php/Installation_guide#Partition_the_disks refer this for partition table schema. 

----------------------------------------------------------------------------------------------------------<br>

#### 3. Now Follow below steps.

#### EFI partition

    ```d``` -> hit d and select partition number until all the partitions are deleted <br>

    ```g``` -> creates new gpt label for disk. <br>

    ```n``` -> new partition <br>
    
    ```hit from 2048---end``` -> starting sector. <br>
    
    when fdisk asks for +/-/ end type
    
    ```+512M``` -> EFI partition size of 512MB (At least 260 MiB ) 
    
    hit yes for removing signature of existing partitons.<br>
    
    ```t``` -> to change the type of the partition
    -> select partition number 1,2,3 etc. 
    
    ```L``` to list types -> and press Q to quit the list and select 1 on the prompt for - EFI 
    
    ----------------------------------------------------------------------------------------------------------<br>
    
   #### SWAP partition.
    
   ```n``` - > new partition.
    
    Hit enter for starting sector
    
    when fdisk asks for +/-/ end type

    ```+your RAM-size + 1G``` -> for Hibernate Support
    example: if your ram size is 8GB then ```+9GB```
    
    ```+4G``` or ```+8G``` -> Common swap partition. (Without Hibernate support).
    
    hit yes for removing signature of existing partitons.
    
    ```t``` -> to change the type of the partition
    -> select partition number 1,2,3 etc. (2 in this case)
    
    ```L``` to list types -> and press Q to quit the list and select 19 on the prompt for - EFI 
    
----------------------------------------------------------------------------------------------------------<br>

#### Root partition

   ```n``` - > new partition.
    
    Hit enter for starting sector
    
    when fdisk asks for +/-/ end hit enter this is the last partition and end of disk.
    
    This is the root partitions so it must be in Linux File System type.
    
    ```t``` -> to change the type of the partition
    -> select partition number 1,2,3 etc. 
    
    ```L``` to list types -> select 20 - Linux File System.
        
    NOW to write the partitions
    
    ```w``` -> this will write partition
    
----------------------------------------------------------------------------------------------------------

### Disk-partitions-done now formatting.
    
1. For EFI Partition  

```mkfs.fat -F 32 /dev/sdX1```  
    
2. For root partition  

```mkfs.ext4 /dev/sdX2```
    
3. For Swap Partition.  

```mkswap /dev/sdX3```
    `                          
```swapon /dev/sdX3```
    
   
