# File management

## Linux filesystem

``` sh
# Description of filesystem hierarchy.
man hier
```

- /: The root directory where everything else resides.
- /root: The home directory for the root user.
- /bin: Contains essential binary executables (ls, cat, mv, rm, etc).
- /sbin: Contains binary files for system maintenance and/or administrative tasks (fdisk, ifconfig, reboot, etc).
- /etc: Contains configuration files required by all programs.
- /home: Contains home directories for users.
- /var: Contains variable data files such as logs and databases.
- /usr: Contains read-only user data; a secondary hierarchy for read-only user data.
- /boot: Contains files needed to start up the system.
- /dev: Contains device files (hardware).
- /lib: Contains library files that can be used by the binaries located in /bin and /sbin
- /tmp: Contains temporary files created by system and users. The data in this directory is cleared each time the system is rebooted.
- /mnt: Temporary mount point for mounting file systems (for instance when USB is connected it will appear there).
- /proc: A virtual filesystem providing process and kernel information as files. In other words, it contains information about running processes.
- /run: A tmpfs (temporary file system) directory that stores volatile runtime data for programs. It's cleared at each reboot.
- /sys: A virtual filesystem that provides a lot of information about the system hardware and associated device drivers.
- /srv: This directory contains server-specific data that is served by the system.

Regular users have write-access to two directories only:
- /home
- /tmp

### Listing files
``` sh
# Current directory name.
pwd

# Lists directory contents.
ls
ls -l  # Long format.
ls -a  # List hidden files also.
ls -ld  # Display properties and not contents of directory (-d).
ls -lrt  # Display time-sorted list of files.
```

### Wildcards (globbing)

``` sh
ls b*  # List all files starting with 'b'.
ls a?*  # List all files starting with 'a' and at least one more character.
ls a[nm]*  # List all files starting with 'an' or 'am'
ls a[a-e]*  # List all files starting with 'aa', 'ab', 'ac', 'ad', or 'ae'.
```

``` sh
touch file{1..100}  # Create 100 files, from file1 to file100.
mkdir /data/{sales,account}  # Create two directories in the /data folder.
```

### Copy files and directories

``` sh
cp file1 dest_file  # Copy file to another location.
cp dir1/ dest_dir/  # Copy a directory.
cp file1 dest_dir/  # Copy a file into a directory.
cp file1 file2 dest_dir/  # Copy many files into a directory.
cp -p file1 dest_file  # Copy a file and preserve its attributes (like timestamp).
cp -v file1 new_file  # Verbose mode.
cp -i file1 file2  # Interactive mode.
```
