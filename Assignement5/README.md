# Assignement 5 - Main

## Part 1 - QEMU MIPS Debian Wheezy
Let's run the same command as in the previous assignement but with all right ports forwarded
```bash
qemu-system-mips -M malta -kernel vmlinux-3.2.0-4-4kc-malta -hda debian_wheezy_mips_standard.qcow2 -append "root=/dev/sda1 console=tty0" -net user,hostfwd=tcp::20022-:22 -net user,hostfwd=tcp::20080-:80 -net user,hostfwd=tcp::20443-:443 -net nic
```

### QEMU process running (in Parrot)
![](img/qemu-ps.png)

### QEMU netstat (in Parrot)
![](img/qemu-netstat.png)

### QEMU ssh
![](img/qemu-ssh.png)

If a try to ssh directely after the QEMU booted, this makes my entire computer crash. I need to first log into the machine with the emulated terminal, and ask for the status of the ssh server like so :
```bash
service ssh status
```
This does not really seem to resolve the problem.

## Part 2 - Simulate firmware
### QEMU process running (in QEMU)
![](img/qemu-ssh-ps.png)

### QEMU netstat (in QEMU)
![](img/qemu-ssh-netstat.png)

### QEMU - Starting firmware
The start of the firmware went pretty well!

![](img/qemu-ssh-start-firm.png)

### QEMU - process running (in QEMU, firmware running)
![](img/qemu-ssh-firm-ps.png)

### QEMU - netstat (in QEMU, firmware running)
![](img/qemu-ssh-firm-netstat.png)