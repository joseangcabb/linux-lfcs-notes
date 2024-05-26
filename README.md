# Linux LFCS

The Linux Foundation Certified System Administrator (LFCS) certification is a professional credential designed to validate a candidate's knowledge and skills in managing and administering Linux systems.

- [Getting help](docs/getting_help.md)
- [File management](docs/file_management.md)
- [Storage management](docs/storage_management.md)
- [Networking](docs/networking.md)

## Administrator privileges
Members of the 'wheel' group are granted the ability to execute commands with elevated privileges.
``` sh
sudo ls /root
```

Opening a shell with specific privileges.
``` sh
su -  # Open a root shell.
su - <username>  # Open a user shell.
```

## Essential commands
``` sh
whoami  # Get username that is currently authenticated.
ls      # List files.
cd      # Change directory
ip a    # Get IP address.
cat     # Show text.
passwd  # Set a password.
touch   # Create empty files.
pwd     # Print working directory.
history # Command history
```

The --help option is commonly used in many command-line commands on Unix and Linux systems to provide detailed information on how to use a specific command.
