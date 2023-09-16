# shell_in_C
shell in C
# Filesystem

C code compiles with:

```gcc -Wall -Werror --std=c99 <filename>```

A user space portable index-allocated file system that provides the user with 2<sup>26</sup> bytes of drive space in a disk image. Users will have the ability to create the filesystem image, list the files currently in the file system, add files, remove files, and save the filesystem. Files will persist in the file system image when the program exits.

The following commands shall are implemented:

|Command|Usage|Description|
|-------|-----|-----------|
|insert|```insert <filename>```|Copy the file into the filesystem image|
|retrieve|```retrieve <filename>```|Retrieve the file from the filesystem image and place it in the current working directory|
|retrieve|```retrieve <filename> <newfilename>```|Retrieve the file from the filesystem image and place it in the current working directory using the new filename|
|read|```read <filename> <starting byte> <number of bytes>```|Print \<number of bytes\> bytes from the file, in hexadecimal, starting at \<starting byte\>
|delete|```delete <filename>```|Delete the file from the filesystem image|
|undel|```undelete <filename>```|Undelete the file from the filesystem image|
|list|```list [-h] [-a]```|List the files in the filesystem image. If the ```-h``` parameter is given it will also list hidden files. If the ```-a``` parameter is provided the attributes will also be listed with the file and displayed as an 8-bit binary value.|
|df|```df```|Display the amount of disk space left in the filesystem image|
|open|```open <filename>```|Open a filesystem image|
|close|```close```|Close the opened filesystem image|
|createfs|```createfs <filename>```|Creates a new filesystem image|
|savefs|```savefs```|Write the currently opened filesystem to its file|
|attrib|```attrib [+attribute] [-attribute] <filename>```|Set or remove the attribute for the file|
|encrypt|```encrypt <filename> <cipher>```|XOR encrypt the file using the given cipher.  The cipher is limited to a 1-byte value|
|decrypt|```encrypt <filename> <cipher>```|XOR decrypt the file using the given cipher.  The cipher is limited to a 1-byte value|
|quit|```quit```|Quit the application|

## Command Details 
### ```insert``` 
```insert``` shall allow the user to put a new file into the file system.
The command shall take the form:
```insert <filename>```
If the filename is too long an error will be returned stating:
```insert error: File name too long.```
If there is not enough disk space for the file an error will be returned stating:
```insert error: Not enough disk space.```

### ```retrieve``` 
The ```retrieve``` command shall allow the user to retrieve a file from the file system and place it in the current working directory.
The command shall take the form:
```retrieve <filename>```
and
```retrieve <filename> <newfilename>```
If no new filename is specified the ```retrieve``` command shall copy the file to the current working directory using the old filename.
If the file does not exist in the file system an error will be printed that states: 
```Error: File not found.```

### ```delete``` command
The ```delete``` command shall allow the user to delete a file from the file system
If the file does exist in the file system it shall be deleted and all the space available for additional files.

### ```undelete``` command
The ```undelete``` command shall allow the user to undelete a file that has been deleted from the file system
If the file does exist in the file system directory and marked deleted it shall be undeleted.
If the file is not found in the directory then the following shall be printed:
```undelete: Can not find the file.```

### ```list``` command 
The ```list``` command shall display all the files in the file system, their size in bytes and the time they were added to the file system
If no files are in the file system a message shall be printed: ```list: No files found.```
Files that are marked as hidden shall not be listed

### ```df``` command
The ```df``` command shall display the amount of free space in the file system in bytes.

### ```open``` command
The ```open``` command shall open a file system image file with the name and path given by the user.
If the file is not found a message shall be printed:
```open: File not found```

### ```close``` command
The ```close``` command shall close a file system image file with the name and path given by the user.
If the file is not open a message shall be printed:
```close: File not open```

### ```savefs command```
The ```savefs``` command shall write the file system to disk.

### ```attrib``` command
The ```attrib``` command sets or removes an attribute from the file.
Valid attributes are:

|Attribute|Description|
|---------|-----------|
| h       | Hidden. The file does not display in the directory listing|
| r       | Read-Only. The file is marked read-only and can not be deleted.|

To set the attribute on the file the attribute tag is given with a +, ex:
```mfs> attrib +h foo.txt```
To remove the attribute on the file the attribute tag is given with a -, ex:
```mfs> attrib -h foo.txt```
If the file is not found a message shall be printed:
```attrib: File not found```
```createfs command```

### ```createfs``` command 
```createfs``` shall create a file system image file with the named provided by the user.
If the file name is not provided a message shall be printed:
```createfs: Filename not provided```

### ```encrypt``` command 
The ```encrypt``` command shall allow the user to encrypt a file in the file system using the provided cipher.  This is a simple byte-by-byte [XOR cipher](https://en.wikipedia.org/wiki/XOR_cipher). [Cyber Chef](https://cyberchef.org/) can help verify your encryption.
The command shall take the form:
```encrypt <filename> <cipher>```
The cipher is required to be 256 bits.

### ```decrypt``` command 
The ```decrypt``` command shall allow the user to decrypt a file in the file system using the provided cipher.  This is a simple byte-by-byte [XOR cipher](https://en.wikipedia.org/wiki/XOR_cipher). 
The command shall take the form:
```decrypt <filename> <cipher>```

