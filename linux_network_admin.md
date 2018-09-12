## Notes on Linux Network Administration

### Commands
* `hostname` : reports the hostname of the machine on which your
  shell is attached.

* `systemctl` : start, stop, restart or check status of services.

* `nmtui` : this command allows you to configure Network Manager
  within a shell environment, but with GUI-like controls.

* `ssh -p [port_no] [user]@[host]` : connect to `host` as `user`
  and on the port number `port\_no`

* `scp -p filename hostname:path` : copies file `filename` with
  preserving modification times, to `path` of the host with hostname
  `hostname`.

* Use `-P` flag with `scp` to specify port number.

* Use `-L` flag with ssh to forward a local port to a specific
  port on the other end(server). Example usage;
  ```
  ssh -L <local-port>:localhost:<remote-port> <username>@remote_address
  ```

* `ssh-keygen` : Allows setting up keys for authentication over SSH.

* `ssh-copy-id` : Used to copy the ssh key of the local system to
  the remote system. Example;
  ```
  ssh-copy-id -i ~/.ssh/id-rsa.pub <remote host IP or name>
  ```
  This command will copy your public key into the `authorized_keys` file
  under your `~/.ssh` folder on the target machine. This file stores all
  the keys that the machine knows about.

* To keep SSH from disconnection configure the the `ServerAliveInterval`
  setting. This can be done on a per user basis or for the entire hosts
  that we connect as follows;
  1. Per user basis in `~/.ssd/config`
  ```bash
  Host icarus
  ServerAliveInterval 60  # send an alive packet every 60 seconds.
  Hostname 10.10.10.76
  Port 22
  User jdoe
  ```
  2. For all host we connect to, then at the top of the config file.
  ```bash
  Host *
  ServerAliveInterval 60
  ```
* `/etc/ssh/ssh_config` : This file will impact all users whom make
  outbound connections. Think of this as client configuration file.

* `/etc/ssh/sshd_config` : This is the global config file for the server.

### Special Files in Linux
* `/etc/hosts/` : the file a linux host will check first to resolve
  hostnames. If an entry for the host you're contacting isn't included
  there, your machine will then contact its configured primary DNS
  server in order to find an IP address for the name that you entered.

* `/etc/nsswitch.conf` : Used to determine the order in which host
  resolution occurs.

* `/etc/network/interfaces` : the file that controls the network
  devices by default. Check `interfaces(5)`. For example;
  ```
  #Wired connection eth0
  auto eth0 #Automatically load this interface.
  iface eth0 inet static #Assign static IP
    address 10.10.10.12
    netmask 255.255.248.0
    network 10.10.10.0
    broadcast 10.10.10.255
    gateway 10.10.10.1

  #To make this take effect use command
  systemctl restart networking.service
  ```
* `~/.ssh` : directory created when SSH is used first time. Contains
  useful files for SSH client, which include `known_hosts`, `id_rsa`
  , and `id_rsa.pub` once keys are generated.

* `~/.ssh/config` : not created by default. If you have one or more
  hosts that you connect to frequently, you can fill this file with
  the specifics for each host without having to enter the details
  each time. For example the file can contain;
  ```
  Host icarus
  Hostname 10.10.10.76
  Port 22
  User jdoe

  Host daedalus
  Hostname 10.10.10.88
  port 65000
  User duser

  Host dragon
  Hostname 10.10.10.99
  Port 22
  User jdoe
  ```
* `~/.ssh/id_rsa` : generated when executng ssh-keygen, contains the
  private key. Should not be transmitted or shared in public place.

* `~/.ssh/id_rsa.pub` : Also generated when executing ssh-keygen.
  Contains the public key.

### Networking concepts
* *DNS Record Types*
  | Record Type  | Description                                                                          |
  | ------------ | ------------------------------------------------------------------------------------ |
  | A Record     | Translates machine names into IPv4 addresses                                         |
  | AAAA Record  | Translates machine names into IPv6 addresses                                         |
  | MX Record    | Specifies the names of the mail servers that handles mail for a specified domain.    |
  | NS Record    | Specify the name servers for a specified domain.                                     |
  | PTR Record   | These are mainly used for reverse lookups translating IP addresses to machine names. |
  | CNAME Record | These simply redirect to another machine name, like an alias.                        |

* _Static lease_ the DHCP server will provide the same IP address for
  a particular MAC address each time. With a static lease, the node's
  IP configuration is not tied to its configuration with its installed
  distribution. Even if the node is booted from live media, or even
  if the distribution is reinstalled, the node will still recieve the
  same IP address each time its interface comes up. An additional
  benefit of a static lease is that you can configure the static IPs
  of all your nodes in one central place (on the DHCP server).

* SSH by default uses port 22 to communicate.

* An SSH tunnel allows you to access services locally that originate
  from another computer or server. This allows to bypass local DNS
  filtering, or even access an IRC server that is segregated(set apart
  from the rest or from each other; isolate or divide) within
  your company, from home.

### Packages for Networking
* iproute2
* net-tools
* The three most common methods of sharing files from one linux system to
  another are:
  1. *Network File System (NFS)* : is a great choice within a Linux-based
     environment; however, it doesn't handle mixed environment as well.
  2. *Samba* : allows to share files between all three major platforms
     (Windows, Linux and Mac OSX) and is a great choice within mixed
     environment. Uses the *SMB* protocol. There is some extra work required
     when sharing files between windows and linux nodes, to handle 
     permissions. So it is not always the best choice when dealing with
     UNIX or Linux nodes that need to retain specific permissions.
  3. *Secure Shell File System (SSHFS)* : is primarily geared toward sharing
     files between linux nodes. It is possible to connect and access from
     windows, but only with third-party utilities, as no built-in method
     exists in Windows. It is popular for its ease of use and security due
     to encryption. There is nothing to configure on the server other than
     SSH itself. Also it can be created and disconnected on-demand very
     quickly.
