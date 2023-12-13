# Linux LFCS

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

## Help with man (Systems programmers manual)

Install and load man packages.
``` sh
sudo pacman -S man-db man-pages
sudo mandb
```

Usage of man.
``` sh
man whoami
man man
```

Man pages have section and some important sections are: _end-user commands (1), root commands (2), configuration files (3)_.

### Search in man pages
Search for specific term in man pages: /term and use 'n' for next occurrence of the term and 'N' for previous occurrence.

### Keyword searches in man
``` sh
# Search in page descriptions.
man -k <term>
man apropos <term>
man -k user | less
man -k user |

# Search in specific section.
# man <section> <term>
man 1 user
man -l user | grep 8  # Filter only lines containing 8.
```

### Other systems for help
The documentation can also be seen with 'pinfo'.
``` sh
pinfo '(coreutils) ls invocation'
```

Docs for packages and programs in /usr/share/doc
``` sh
cd /usr/share/doc
ls
cd <program>
```

tldr, display simple documentation with examples
``` sh
sudo pacman -S tldr
tldr ls
tldr git commit
tldr grep
```
