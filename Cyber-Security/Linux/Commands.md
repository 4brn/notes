
## 
```bash
pwd # current location
whoami # logged in user
cd # change directory 
ls # list contents 
ps # display running processes
ps aux # list all running processes

# Help
--help # help
-h # help
man # manual page 

# Finding stuff
locate # locate every occurance 
whereis # locate binaries + manpage location
which # locates only binaries in PATH

find <directory> <options> <expression> 
# example: find /➊ -type f➋ -name apache2➌

grep # filter
# example: ps aux | grep apache2

# Creating and modifying files
cat # print and concatenate on terminal
cat > filename # create and write to 'filename' until CTRL-D is pressed OR overwrite 'filename'
cat >> filename # append more content to 'filename'
touch # create file
mkdir # create directory
cp <file> <directory> # copy oldfile to directory
mv <file> <newfile> # move or rename file
rm <file> # remove file 
rmdir <directory> # remove EMPTY directory


```

` | ` or pipe - allows the output on a command to be used in another command:
	`cat names.txt | grep "Aleks"`


