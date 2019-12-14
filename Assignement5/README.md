# Assignement 5 - Main

# Part 1 - QEMU MIPS Debian Wheezy
Let's run the same command as in the previous assignement but with all right ports forwarded
```bash
qemu-system-mips -M malta -kernel vmlinux-3.2.0-4-4kc-malta -hda debian_wheezy_mips_standard.qcow2 -append "root=/dev/sda1 console=tty0" -net user,hostfwd=tcp::20022-:22 -net user,hostfwd=tcp::20080-:80 -net user,hostfwd=tcp::20443-:443 -net nic
```

## QEMU process running (in Parrot)
![](img/qemu-ps.png)

## QEMU netstat (in Parrot)
![](img/qemu-netstat.png)

## QEMU ssh
![](img/qemu-ssh.png)

If a try to ssh directely after the QEMU booted, this makes my entire computer crash. I need to first log into the machine with the emulated terminal, and ask for the status of the ssh server like so :
```bash
service ssh status
```
This does not really seem to resolve the problem. But it has allowed me to do it. 

# Part 2 - Simulate firmware
## QEMU process running (in QEMU)
![](img/qemu-ssh-ps.png)

## QEMU netstat (in QEMU)
![](img/qemu-ssh-netstat.png)

## QEMU - Starting firmware
The start of the firmware went pretty well!

![](img/qemu-ssh-start-firm.png)

## QEMU - process running (in QEMU, firmware running)
![](img/qemu-ssh-firm-ps.png)

## QEMU - netstat (in QEMU, firmware running)
![](img/qemu-ssh-firm-netstat.png)


## Additional questions to answer:

What type of emulation did you just employ?

QEMU performs hardware virtualization, it's a full system emulation. 

What type of kernel does this XXX-emulation uses ?

QEMU also can be used with KVM (Kernel-based Virtual Machine) to run virtual machines at near-native speed. It is in the generic system
emulator category where the generic kernel is used. So the KVM-emulation used the Linux kernel since the kernel version 2.6.20, which was released on February 5, 2007.

What new processes appeared as a result of emulation? 


What new network ports/services appeared as a result of emulation? 

25/exim4

111, 886/rpcbind

51356, 68, 65471/dhclient

936, 57880, 41968, 51905, 34866/rpc.statd


For each new process and network service, detail few words what you think it is, what vulnerabilities it may contain and what tools of dynamic analysis you may be able to use to find vulnerabilities in it.

#### Exim4:
Exim4 is another Message Transfer Agent (MTA) developed at the University of Cambridge for use on Unix systems connected to the Internet. 

Vulnerabilities : Exec Code Overflow, DoS and +Priv.

Tools : Rapid7, AFL

#### rpcbind:
The rpcbind utility is a server that converts RPC program numbers into universal addresses.

Vulnerabilities : DoS

Tools : Peach Fuzzer, yersinia

#### dhclient:
The Internet Systems Consortium DHCP Client, dhclient, provides a means for configuring one or more network interfaces using the Dynamic Host Configuration Protocol, BOOTP protocol, or if these protocols fail, by statically assigning an address. 

Vulnerabilities : DoS, Exec Code, Overflow

Tools : yersinia, AFL

#### rpc.statd:
rpc.statd is a daemon that listens for reboot notifications from other hosts, and manages the list of hosts to be notified when the local system reboots.

Vulnerabilities : Exec Code

Tools : rpc.statd remote root xploit
