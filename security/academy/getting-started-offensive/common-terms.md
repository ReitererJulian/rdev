# Information Security

In a nutshell, infosec is the practice of protecting data from unauthorized access, changes, unlawful use, disruption, etc.

## Risk Management Process

- `Identifying the Risk`
- `Analyze the Risk`
- `Evaluate the Risk`
- `Dealing with Risk`
- `Monitoring Risk`

## Red Team vs. Blue Team

In the simplest terms, the `red team` plays the attackers' role, while the `blue team` plays the defenders' part.

### Red Team

The most common task on the red teaming side is penetration testing, social engineering, and other similar offensive techniques.

### Blue Team

On the other hand, the blue team makes up the majority of infosec jobs. It is responsible for strengthening the organization's defenses by analyzing the risks, coming up with policies, responding to threats and incidents, and effectively using security tools and other similar tasks.

### Shell

On a Linux system, the shell is a program that takes input from the user via the keyboard and passes these commands to the operating system to perform a specific function.

### Port

A Port can be thought of as a window or door on a house, if a window or door is left open or not locked correctly, we can often gain unauthorized access to a home.

Ports are virtual points where network connections begin and end.

Each port is assigned a number, and many are standardized across all network-connected devices. For example, `HTTP` messages (website traffic) typically go to port `80`, while `HTTPS` messages go to port `443`.

|Port(s)|Protocol|
|---|---|
|`20`/`21` (TCP)|`FTP`|
|`22` (TCP)|`SSH`|
|`23` (TCP)|`Telnet`|
|`25` (TCP)|`SMTP`|
|`80` (TCP)|`HTTP`|
|`161` (TCP/UDP)|`SNMP`|
|`389` (TCP/UDP)|`LDAP`|
|`443` (TCP)|`SSL`/`TLS` (`HTTPS`)|
|`445` (TCP)|`SMB`|
|`3389` (TCP)|`RDP`|

### TCP

`TCP` is connection-oriented, meaning that a connection between a client and a server must be established before data can be sent

### UDP

`UDP` utilizes a connectionless communication model. There is no "handshake" and therefore introduces a certain amount of unreliability since there is no guarantee of data delivery.

### Risk, Vulnerability, Weakness

> In essence, a risk represents the potential for damage, a threat is what can cause that damage, and a vulnerability is the weakness that allows the threat to cause damage.

### Service

A service is an application running on a computer that performs some useful function for other users or computers. These special machines are called "servers".

Computers are assigned an IP address, which allows them to be uniquely identified and accessible on a network. The services running on these computers may be assigned a port number to make the service accessible.

To access a service remotely, we need to connect using the correct IP address and port number and use a language that the service understands. Manually examining all of the 65,535 ports for any available services would be laborious, and so tools have been created to automate this process and scan the range of ports for us. One of the most commonly used scanning tools is Nmap(Network Mapper).