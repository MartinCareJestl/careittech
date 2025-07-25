# Ubuntu CLI cheat sheet

## System
**System information**\
`uname -a` : Displays all system information.\
`hostnamectl` : Shows current hostname and related details.\
`lscpu` : Lists CPU architecture information.\
`timedatectl status` : Shows system time.
___
**System monitoring and management**\
`top` : Displays real-time system processes.\
`htop` : An interactive process viewer (needs installation).\
`df -h` : Shows disk usage in a human-readable format.\
`free -m` : Displays free and used memory in MB.\
`kill <process id>` : Terminates a process.
___
**Running commands**\
`<command> &` : Runs command in the background.\
`jobs` : Displays background commands.\
`fg <command number>` : Brings command to the foreground.
___
**Service management** \
`sudo systemctl start <service>` : Starts a service.\
`sudo systemctl stop <service>` : Stops a service.\
`sudo systemctl status <service>` : Checks the status of a service.\
`sudo systemctl reload <service>` : Reloads a service’s configuration without interrupting its operation.\
`journalctl -f` : Follows the journal, showing new log messages in real time.\
`journalctl -u <unit_name>` : Displays logs for a specific systemd unit.
___
**Cron jobs and scheduling**\
`crontab -e` : Edits cron jobs for the current user.\
`crontab -l` : Lists cron jobs for the current user.

## Files
**File management**\
`ls` : Lists files and directories.\
`touch <filename>` : Creates an empty file or updates the last accessed date.\
`cp <source> <destination>` : Copies files from source to destination.\
`mv <source> <destination>` : Moves files or renames them.\
`rm <filename>` : Deletes a file.
___
**Directory navigation**
`pwd` : Displays the current directory path.\
`cd <directory>` : Changes the current directory.\
`mkdir <dirname>` : Creates a new directory.
___
**File permissions and ownership**\
`chmod [who][+/-][permissions] <file>` : Changes file permissions.\
`chmod u+x <file>` : Makes a file executable by its owner.\
`chown [user]:[group] <file>` : Changes file owner and group.
___
**Searching and finding**\
`find [directory] -name <search_pattern>` : Finds files and directories.\
`grep <search_pattern> <file>` : Searches for a pattern in files.
___
**Archiving and compression**\
`tar -czvf <name.tar.gz> [files]` : Compresses files into a tar.gz archive.\
`tar -xvf <name.tar.[gz|bz|xz]> [destination]` : Extracts a compressed tar archive.
___
**Text editing and processing**\
`nano <file>` : Opens a file in the Nano text editor.\
`cat <file>` : Displays the contents of a file.\
`less <file>` : Displays the paginated content of a file.\
`head <file>` : Shows the first few lines of a file.\
`tail <file>` : Shows the last few lines of a file.\
`awk ‘{print}’ <file>` : Prints every line in a file

## Packages
**Package management (APT)**\
`sudo apt install <package>` : Installs a package.\
`sudo apt install -f –reinstall <package>` : Reinstalls a broken package.\
`apt search <package>` : Searches for APT packages.\
`apt-cache policy <package>` : Lists available package versions.\
`sudo apt update` : Updates package lists.\
`sudo apt upgrade` : Upgrades all upgradable packages.\
`sudo apt remove <package>` : Removes a package.\
`sudo apt purge <package>` : Removes a package and all its configuration files.
___
**Package management (Snap)**\
`snap find` <package> : Search for Snap packages.\
`sudo snap install` <snap_name> : Installs a Snap package.\
`sudo snap remove` <snap_name> : Removes a Snap package.\
`sudo snap refresh` : Updates all installed Snap packages.\
`snap list` : Lists all installed Snap packages.\
`snap info <snap_name>` : Displays information about a Snap package.

## Users & groups
**User management**\
`w` : Shows which users are logged in.\
`sudo adduser <username>` : Creates a new user.\
`sudo deluser <username>` : Deletes a user.\
`sudo passwd <username>` : Sets or changes the password for a user.\
`su <username>` : Switches user.\
`sudo passwd -l <username>` : Locks a user account.\
`sudo passwd -u <username>` : Unlocks a user password.\
`sudo chage <username>` : Sets user password expiration date.
___
**Group management**\
`id [username]` : Displays user and group IDs.\
`groups [username]` : Shows the groups a user belongs to.\
`sudo addgroup <groupname>` : Creates a new group.\
`sudo delgroup <groupname>` : Deletes a group.

## Networking
**Networking**\
`ip addr show` : Displays network interfaces and IP addresses.\
`ip -s link` : Shows network statistics.\
`ss -l` : Shows listening sockets.\
`ping <host>` : Pings a host and outputs results.
___
**Netplan configuration (read more at netplan.io)**\
`cat /etc/netplan/*.yaml` : Displays the current Netplan configuration.\
`sudo netplan try` : Tests a new configuration for a set period of time.\
`sudo netplan apply` : Applies the current Netplan configuration.
___
**Firewall management**\
`sudo ufw status` : Displays the status of the firewall.\
`sudo ufw enable` : Enables the firewall.\
`sudo ufw disable` : Disables the firewall.\
`sudo ufw allow <port/service>` : Allows traffic on a specific port or service.\
`sudo ufw deny <port/service>` : Denies traffic on a specific port or service.\
`sudo ufw delete allow/deny <port/service>` : Deletes an existing rule.
**SSH and remote access**\
`ssh <user@host>` : Connects to a remote host via SSH.\
`scp <source> <user@host>:<destination>` : Securely copies files between hosts.

## LXD
> LXD is a modern, secure and powerful tool that provides a unified experience forrunning and managing containers or virtual machines. Visit [https://canonical.com/lxd](https://canonical.com/lxd) for more information.


`lxd init` : initializes LXD before first use
___
**Creating instances**\
`lxc init ubuntu:22.04 <container name>` : Creates a lxc system container (without starting it).\
`lxc launch ubuntu:24.04 <container name>` : Creates and starts a lxc system container.\
`lxc launch ubuntu:22.04 <vm name> --vm` : Creates and starts a virtual machine.
___
**Managing instances**\
`lxc list` : Lists instances.\
`lxc info <instance>` : Shows status information about an instance.\
`lxc start <instance>` : Starts an instance.\
`lxc stop <instance> [--force]` : Stops an instance.\
`lxc delete <instance> [--force|--interactive]` : Deletes an instance.
___
**Accessing instances**\
`lxc exec <instance> -- <command>` : Runs a command inside an instance.\
`lxc exec <instance> -- bash` : Gets shell access to an instance (if bash is installed).\
`lxc console <instance> [flags]` : Gets console access to an instance.\
`lxc file pull <instance>/<instance_filepath> <local_filepath>` : Pulls a file from an instance.\
`lxc file pull <local_filepath> <instance>/<instance_filepath>` : Pushes a file to an instance.
___
**Using projects**\
`lxc project create <project> [--config <option>]` : Creates a project.\
`lxc project set <project> <option>` : Configures a project.\
`lxc project switch <project>` : Switches to a project.

## Ubuntu Pro
> Ubuntu Pro delivers 10 years of expanded security coverage on top of Ubuntu’s Long Term Support (LTS) commitment in addition to management and compliance tooling. Visit [https://ubuntu.com/pro](https://ubuntu.com/pro) to register for free on up to five machines.
___
**Activating Ubuntu Pro**\
`sudo pro attach <token>` : Attaches your machine to Ubuntu Pro using a specific token. This token is provided when you subscribe to Ubuntu Pro.
___
**Managing services**\
`sudo pro status` : Displays the status of all Ubuntu Pro services.\
`sudo pro enable <service>` : Enables a specific Ubuntu Pro service, like ESM, FIPS, or Livepatch.\
`sudo pro disable <service>` : Disables a specific Ubuntu Pro service.
___
**Extended Security Maintenance (ESM)**\
`sudo pro enable esm-infra` : Activates Extended Security Maintenance for infrastructure packages, providing security updates beyond the standard release cycle.\
`sudo pro enable esm-apps` : Activates ESM for applications, extending security coverage for specific applications.
___
**Livepatch service**\
`sudo pro enable livepatch` : Enables the Livepatch service, which applies critical kernel patches without rebooting.
___
**FIPS mode**\
`sudo pro enable fips` : Enables FIPS (Federal Information Processing Standards) mode, enforcing strict cryptographic standards and practices.
___
**Updating configuration**\
`sudo pro refresh` : Refreshes the Ubuntu Pro state to ensure the latest configuration and services are in place.
___
**Detaching Ubuntu Pro**\
`sudo pro detach` : Detaches the machine from Ubuntu Pro, disabling all services.

# Credits
Thanks a lot to Ubuntu for this Cheat Sheet

[System](#System)
