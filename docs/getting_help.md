# Getting help

## Help with man

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

## Help from other sources
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

## Examples of how to use helps

### Update hostname
``` sh
# Search short descriptions and manual pages for hostname.
man -k hostname

# Manual pages for hostnamectl.
man hostnamectl

# More concie information than manual pages.
hostnamectl --help

# Set system hostname
hostnamectl hostname Archlinux

# Display current values
hostnamectl status
```

### IP setup
``` sh
ip --help
ip link help

ip address

sudo ip link set wlan0 down
sudo ip link set wlan0 up
```
