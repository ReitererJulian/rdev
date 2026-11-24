# Tools

## SHH

Secure Shell (SSH) is a network protocol that runs on port `22` by default and provides users such as system administrators a secure way to access a computer remotely.
SSH can be configured with password authentication or passwordless using public and private keys.

## Netcat

Netcat, `ncat`, or `nc`, is an excellent network utility for interacting with TCP/UDP ports. Its primary usage is for connecting to shells. `netcat` can be used to connect to any listening port and interact with the service running on that port. For example, `SSH` is programmed to handle connections over port 22 to send all data and keys. We can connect to TCP port 22 with `netcat`:

```
reiti@htb[/htb]$ netcat 10.10.10.10 22
SSH-2.0-OpenSSH_8.4p1 Debian-3
```

## Nmap

Suppose that we want to perform a basic scan against a target residing at 10.129.42.253. To do this we should type `nmap 10.129.42.253` and hit enter.
Nmap will only scan the 1,000 most common ports by default when not given any other parameters. The scan output reveals that ports 21, 22, 80, 139, and 445 are available (Meaning ready to receive data)

```
reiti@htb[/htb]$ nmap 10.129.42.253

Starting Nmap 7.80 ( https://nmap.org ) at 2021-02-25 16:07 EST
Nmap scan report for 10.129.42.253
Host is up (0.11s latency).
Not shown: 995 closed ports
PORT    STATE SERVICE
21/tcp  open  ftp
22/tcp  open  ssh
80/tcp  open  http
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds

Nmap done: 1 IP address (1 host up) scanned in 2.19 seconds
```

Under the `PORT` heading, it also tells us that these are TCP ports. By default, `Nmap` will conduct a TCP scan unless specifically requested to perform a UDP scan.  
The `STATE` heading confirms that these ports are open. Sometimes we will see other ports listed that have a different state, such as `filtered`. This can happen if a firewall is only allowing access to the ports from specific addresses.

We can use the `-sC` parameter to specify that `Nmap` scripts should be used to try and obtain more detailed information. The `-sV` parameter instructs `Nmap` to perform a version scan