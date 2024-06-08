# Help

```bash
# Help
<command> --help # help
<command> -h # help
man <command> # manual page
```

## Essentials

```bash
# Essentials
pwd # current location
whoami # logged in user
cd # change directory
ls # list contents

# Pipe - allows the stdout on a command to be used as stdin in another command:
cat names.txt | grep "Aleks"
```

## Finding Stuff

```bash
# Finding Stuff
locate # locate every occurance
whereis # locate binaries + manpage location
which # locates only binaries in PATH
find <directory> <options> <expression>
find / -type f -name apache2
```

## Creating and Modifying Files

```bash
# Creating and Modifying Files
cat # print and concatenate on terminal
cat > filename # create and write to 'filename' until CTRL-D is pressed OR overwrite 'filename' #nicetoknow
cat >> filename # append more content to 'filename' #nicetoknow
echo # display text (> and >> work the same)
touch # create file
mkdir # create directory
cp <file> <directory> # copy file to directory
mv <file> <newfile> # move or rename file
rm <file> # remove file (-rf deletes everithing (recursive and forced))
rmdir <directory> # remove EMPTY directory
shred <file> # overwrite and delete a file #nicetoknow
```

## Text Manipulation

```bash
# Text Manipulation
head # shows first 10 lines of a file (Change number to show more or less)
  head -20 # change number to show more or less
tail # shows last 10 lines of a file (Change number to show more or less)
  tail -20 # change number to show more or less
nl <file> # displays a file with line numbers
tee <file/s> # copy result to each file/s but also print it on the screen #nicetoknow
grep <pattern> # filters out a file for matching pattern
  cat login_info | grep password
sed # stream edditor
  sed s/<to_be_replaced>/<replacement>/g <file># 's' - search ; 'g' - globally #nicetoknow

more <file> # read through a file a page at a time
less <file> # similar to more but allows for word searching with /<word>
```

## Analyzing And Managing Networks

```bash
# Analysing and managing networks
ifconfig # examines active network interfaces (eth0, wlan0, ...)
iwconfig # examies active WIRELESS network interfaces (more indepth)
dhclient <interface> # DHCP client - Assign new IP addresses #nicetoknow
dig # DNS lookup utility
 dig <website> <option> # look up the IP of <website> #nicetoknow
```

### Changing Network Information

```bash
# Spoofing IP, netmask, broadcast address
ifconfig <interface> <IP> # change IP assigned to that interface
ifconfig <interface> netmask <mask>
ifconfig <interface> broadcast <broadcast_address>
 # This commands can be combined :
 ifconfig <interface> <IP> netmask <mask> broadcast <broadcast_address>
```

```bash
# Spoofing MAC Address
ifconfig <interface> down # brings down the ingerface
ifconfig <interface> hw <ether/wifi> <MAC_Address> # change MAC address
ifconfig <interface> up # bring up the interface
```

```bash
# Assign new IP address from the DHCP server
dhclient <interface>
```

```bash
# Changing DNS server
echo "nameserver <DNS_IP>" > /etc/reslov.conf #nicetoknow
OR
edit /etc/reslov.conf , replacing the DNS address with the new one.
```

```bash
# Changing the hosts file:
# The hosts file acts as a local dns. You can assign IP/website pairs
echo <IP> <name> >> /etc/hosts # 192.0.23.1 bankofamerica.com
```

## Adding And Removing Software

```bash
apt search <package> # search for a package
apt install <package> # install a package
apt remove <package> # uninstall a package
apt purge <package> # uninstalls package and config files
apt update # updates packages
apt upgrade # upgrades packages
```

```bash
# Adding new repositories
echo <repository> >> /etc/apt/sources.list #nicetoknow
```

## Controlling File And Directory Permissions

```bash
# Granting ownershp to an individual user
chown ➊<user> ➋<file> # chown = change owner

# Granting ownershop to a group
chgrp ➊<group> ➋<file>

```

### Changing Permissions with Decimal Notation

| Binary | Octal | rwx |
| ------ | ----- | --- |
| 000    | 0     | --- |
| 001    | 1     | --x |
| 010    | 2     | -w- |
| 011    | 3     | -wx |
| 100    | 4     | r-- |
| 101    | 5     | r-x |
| 110    | 6     | rw- |
| 111    | 7     | rwx |

```bash
chmod <owner_num><gropu_num><other_users_num> <file>
  chmod 777 virus.py # grants rwx permission to owner, group, everyone else


# SUID
# Grant temporary owner-level permission to anyone using the file
chmod 4<owner><group><others> <file> #nicetoknow

# SGID
# Grant temporary group-level permission to anyone using the file
chmod 2<owner><group><others> <file> #nicetoknow

```

### Changing Permissions with UGO

```bash
chmod <u/g/o/a><+/-/=><r/w/x> <file>
  # -rwxrwxrwx  1 user user   90 Aug  9 11:29 animals.txt
  chmod a=r animals.txt
  # -r--r--r--  1 user user   90 Aug  9 11:29 animals.txt
```

| attribute | explanation                                     |
| --------- | ----------------------------------------------- |
| u         | user/owner of the file                          |
| g         | group                                           |
| o         | others (not part of group)                      |
| a         | all users                                       |
| +         | add a permission                                |
| -         | remove a permission                             |
| =         | add selected permission/s and remove all others |
| r         | read permission                                 |
| w         | write permission                                |
| x         | execute permission                              |

### umask

`umask is a 3 digit number that is subtracted from the file's permission`

`edit /home/<username>/.profile and add umask <number>`

```bash
echo umask 022 >> /home/user/.profile #nicetoknow

777 - umask = 755 / rwxr-xr-x
666 - umask = 644 / rw-r--r--
```

## Process Management

```bash
ps # display running processes
  ps aux # list all running processes
top # list hungry processes
nice # Change priority of a process #nicetoknow
renice # Change priority of a RUNNING process #nicetoknow
  renice <priority_amount> <PID>
kill <PID> # terminates a process
killall <Process_name> # kill a process using name instead of PID
<command> & # runs the command in the background #nicetoknow
fg <PID> # move process to the foreground #nicetoknow

at <time> # execute a command at a specific time ONCE #nicetoknow
  at> <command/script> # enter command/script
```

## Managing User Environment Variables

```bash
# Viewing environment variables
env # View all default environment variables
set # Vew ALL environment variables #nicetoknow
  set | more
  set | grep <variable>

# Modifying environment variables
variable=value # Change env variable ONLY for this session
export variable # Export the variable to the rest of the system making it permanent
  HISTSIZE=1000
  export HISTSIZE

# Adding to a variable
variable=$variable:value #nicetoknow
  PATH=$PATH:/root/newhackingtool

# Creating a variable
VARIABLENAME=value # The name of the variable should be CAPS

# Deleting a variable
unset <variable>
```

## Bash Scripting

```bash
#!/bin/bash

# ! - shebang (Used at the start of a script to indicate
# which shell interpreter is being used for the script)

```

```bash
read <variable> # writes the user input into <variable> #nicetoknow
```

## Compressing And Archiving

```bash
# Archiving
tar # combining files into one
 tar -cf <name>.tar <file1><file2><file3>... # Combine
 tar -xf <name>.tar # Extract files from .tar file

# Compressing files
gzip # Best (.tar.gz / .tgz)
 gzip <file>.tar
gunzip # uncompress
 gunzip <file>.tar

bzip2 # 2nd (.tar.bz2)
bunzip2 # uncompress

compress # 3rd (.tar.z)
uncompress # uncompress

# Creating bit-by-bit copies of storage devices
dd #nicetoknow
 dd if=<inputfile> of=<outputfile>
  dd if=/dev/sdb of=/root/flashcopy
```

## Filesystem And Storage Device Management

```
/ (root)
/bin (user binaries)
/sbin (system binaries)
/ets (configuration files)
/dev (device files)
/proc (process information)
/var (variable files)
/tmp (temporary files)
/usr (user programs)
/home (home directories)
/lib (system libraries)
/opt (optional add-on apps)
/mnt (mount directory)
/media (removable devices)
/srv (service data)

```

| Device file | Description            |
| ----------- | ---------------------- |
| sda         | First SATA hard drive  |
| sdb         | Second SATA hard drive |
| sdc         | Third SATA hard drive  |
| sdd         | Fourth SATA hard drive |

| Partition | Description                        |
| --------- | ---------------------------------- |
| sda1      | 1st partition on first drive (sda) |
| sda2      | 2nd partition on sda               |
| sda3      | 3rd partition (sda)                |
| sda4      | 4th partition (sda)                |

```bash
# crw------- 1 root root 10,175 May 16 12:44 agpgart
 'c' -> charcter device # Devices sending and recieving data character by character (mice, keyboards)
 'b' -> block device # Devices sending and recieving data in blocks (multiple bytes at a time) (hard drives, DVD drives)
```

```bash
fdisk -l # Lists all partition of all drives
lsblk # Display devices with multiple partition in a tree-like structure
  mount point -> the position at which the drive was attacked to the filesystem

mount <device> <location> # mount a device from /dev to a locaiton
  mount /dev/sdc1 /media
umount <device> # unmount a device (eject)
df # Lists basic information on any mounted devices
fsck <device> # filesystem check (searches and fixes errors) - device needs to e unmounted
```

## Understanding And Inspecting Wireless Networks

- AP (access point) - The device wireless users connect to for internet access
- SSID (service set identifier) - The name of the network
- ESSID (extended service set identifier) - Name that can be used for multiple APs.
- BSSID (basic service set identifier) - The unique identifier of each AP (it is the same as the MAC address of the device).
- Channels - WIFI can operate in 1-14 channels

```bash
iwlist <interface> scan # Scan all nearby networks
nmcli # Network Manager Command Line Interface - same as iwlist but adds more information
  nmcli dev <networktype> # View all WIFI APs near you + their key data
  nmcli dev wifi connect <AP-SSID> password <APpassword> # connect to an AP
```

```bash
# WIFI Recon with aircrack-ng
```
