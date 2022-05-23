## Disk-partition-guide-on-linux-for-Arch-Linux-installation on UEFI devices.

### THIS WILL ERASE DATA on Disk!!!
----------------------------------------------------------------------------------------------------------<br>
NOTE: Im using fdisk utility to partition the disk.

#### 1. Open Your terminal and type

```fdisk -l```<br>

----------------------------------------------------------------------------------------------------------<br>

#### 2. Now you see the list of storage devices on your system.<br>
Select the device as below command.<br><br>
   
   ```fdisk /dev/sdX```<br>
   
Note X here represents the disk alphabet. X may be sda/sdb/nvmep01/etc...<br>

NOTE: https://wiki.archlinux.org/index.php/Installation_guide#Partition_the_disks refer this for partition table schema. <br>

----------------------------------------------------------------------------------------------------------<br>

#### 3. Now Follow below steps.<br>

#### EFI partition<br>

- ```d``` -> hit d and select partition number until all the partitions are deleted <br>

- ```g``` -> creates new gpt label for disk. <br>

- ```n``` -> new partition <br>

- ```hit from 2048---end``` -> starting sector. <br>

- when fdisk asks for +/-/ end type<br>

-```+512M``` -> EFI partition size of 512MB (At least 260 MiB ) <br>

- hit yes for removing signature of existing partitons.<br>

- ```t``` -> to change the type of the partition<br>

- -> select partition number 1,2,3 etc. <br>

- ```L``` to list types -> and press Q to quit the list and select 1 on the prompt for - EFI <br>
    
----------------------------------------------------------------------------------------------------------<br>
   
#### SWAP partition.<br>
    
- ```n``` - > new partition.<br>
- Hit enter for starting sector<br>
- when fdisk asks for +/-/ end type<br>
- ```+your RAM-size + 1G``` -> for Hibernate Support<br>
- example: if your ram size is 8GB then ```+9GB```<br>
- ```+4G``` or ```+8G``` -> Common swap partition. (Without Hibernate support).<br>
- hit yes for removing signature of existing partitons.<br>
- ```t``` -> to change the type of the partition<br>
- -> select partition number 1,2,3 etc. (2 in this case)<br>
- ```L``` to list types -> and press Q to quit the list and select 19 on the prompt for - EFI <br>
    
----------------------------------------------------------------------------------------------------------<br>

#### Root partition<br>

```n``` - > new partition.<br>
Hit enter for starting sector<br>
when fdisk asks for +/-/ end hit enter this is the last partition and end of disk.<br>
This is the root partitions so it must be in Linux File System type.<br>
```t``` -> to change the type of the partition<br>
-> select partition number 1,2,3 etc. <br>
```L``` to list types -> select 20 - Linux File System.<br>
now write the partitions<br>
```w``` -> this will write partition<br>
    
----------------------------------------------------------------------------------------------------------<br>

### Disk-partitions-done now formatting.
    
1. For EFI Partition  

```mkfs.fat -F 32 /dev/sdX1```

2. For Swap Partition.  

```mkswap /dev/sdX2```
    `                          
```swapon /dev/sdX2```
    
2. For root partition  

```mkfs.ext4 /dev/sdX3```
    

    
   
