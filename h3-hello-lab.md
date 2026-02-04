# Hello Lab - Week 3

This week, I start building my own hacking lab. The goal is to learn hacking by hacking.  
Assignment instruction available at: https://terokarvinen.com/information-security/

---

## Summary of the articles

### **Karvinen 2021: Installing Debian on VirtualBox**

A straightforward walkthrough on grabbing the Debian ISO file.

- Create a new virtual machine with enough memory and a generously sized virtual hard drive.
- Attach the ISO as a virtual CD and start the VM from it.
- Before committing to the installation, try the live desktop to make sure everything behaves as expected.
- Launch the installer, pick English and Finnish as your language/region choices, and fill in the user details.
- Once the system is installed, sign in and bring everything up to date using terminal commands.
- To fix the tiny display resolution and enable features like copy-paste between host and guest, install the VirtualBox Guest Additions package.

### **My reflections**

I did not know what an ISO actually was before this, but it turns out it is basically a digital version of a CD.

Allocated 6GB of RAM and a 60GB virtual disk, and it seemed to run without issues.

The whole process went pretty smooth after the class-demo of installation, otherwise I might have issues.


**Reference:**  
Terokarvinen.com. . (2024). *Install Debian on Virtualbox - Updated 2024.* Available at: https://terokarvinen.com/2021/install-debian-on-virtualbox/

---

### **Karvinen 2020: Command Line Basics Revisited**

The command line has been around forever, but it remains incredibly practical.

- Commands like `pwd`, `ls`, and `cd` help you navigate through directories.
- `nano filename` opens a simple text editor right inside the terminal.
- `mkdir`, `mv`, `cp`, and `rm` handle creating, moving, copying, and deleting files or folders.
- `rm -r` is powerful but dangerous-once it deletes something, there is no undo button.
- SSH allows you to log into other machines remotely.
- `scp` lets you transfer files between computers.
- Your command history keeps track of what you've run before, and `Ctrl + R` lets you search through it quickly.
- Key directories to know include `/home/`, `/etc/`, `/media/`, and `/var/log/`.
- `sudo` gives you administrative privileges when needed.
- You can install new software with `sudo apt-get install packagename`.

### **Thoughts**

I've almost never used the command line before, so it was extremely helpful to revisit some tools I don't use regularly in such a precise way.

I learned more about the major system directories, though I am still figuring out how each one is used in practice.

**Reference:**  
Terokarvinen.com. (2020). *Command Line Basics Revisited.* Available at: https://terokarvinen.com/2020/command-line-basics-revisited/

---

## a) Can't Fish

I used the command `ping -c 3 8.8.8.8` to test connectivity.  
When the network adapter was enabled, the ping command returned ICMP replies, showing that packets reached Google’s DNS server and came back.

<img width="414" height="269" alt="VirtualBox_InfoSecurity_Taska1" src="https://github.com/user-attachments/assets/92a45416-1418-4b23-9fd6-0081e3a9a2a8" />

Disable networking and show that packets don’t go through.

Successfully disabled networking and demonstrated that packets cannot traverse outside the local system.
I did it by configuring the UTM VM network mode to "Host Only" to restrict external network access

After disabling the network adapter in the VM settings, running the same command produced the error - "Network is unreachable":

<img width="413" height="64" alt="VirtualBox_InfoSecurity_Taska2" src="https://github.com/user-attachments/assets/3a31b814-4c3d-49f5-95e1-e1c2319ea1ec" />

This shows that the VM cannot send packets outside, proving that the environment is isolated and safe for testing.

---

## b) Local Only

I ran `sudo nmap -A localhost` to scan my own machine.  
Nmap found that **port 631/tcp is open and running CUPS 2.4**, which is the Common UNIX Printing System. CUPS provides printing services on Linux and listens on port 631 using the Internet Printing Protocol (IPP).

All other ports were reported as closed, which means no other services are accepting connections. This is expected for a fresh Debian installation. The scan confirms that my system is not exposing unnecessary services.
Below is the detailed output of the scan:

<img width="1280" height="800" alt="VirtualBox_InfoSecurity_Taskb" src="https://github.com/user-attachments/assets/4a49cab6-7c99-4161-b341-06fb3014e161" />

My computer has "doors" called ports. I checked which doors are open. Only one door (631) was open, and it belongs to the printing system. All the other doors were closed, so nothing else can come in.

### Why I Saw the DNS Warning

mass_dns: warning: Unable to determine any DNS servers.

This is normal because I disconnected the network adapter (as required for the assignment). Nmap tries to do reverse DNS lookups, but since there was no internet, it can not. This does not affect the port scan.

---

## c) Daemon Scan

**The difference**

After installing and starting the Apache daemon, I ran `sudo nmap -A localhost` again.  
The new scan showed that **port 80/tcp is now open and running Apache httpd**, which did not appear in the previous scan. Output of the scan:

<img width="1280" height="800" alt="VirtualBox_InfoSecurity_Taskc" src="https://github.com/user-attachments/assets/0b478721-b810-4be6-9e19-14f4c10b7583" />

This demonstrates that installing a daemon opens a new network port and makes the system accessible in a new way.

### Conclusion: How installing software increases the attack surface

Every daemon that runs on a system opens a port and listens for incoming connections. This increases the "attack surface," meaning there are more possible entry points for attackers.

Before installing Apache, my system had only one open port (631 for CUPS).  
After installing Apache, port 80 became open, which means there is now an additional service that could be targeted if it had vulnerabilities.

Before installing Apache, my computer had only one door open.  
After installing Apache, I added another door (port 80).  
More doors mean more ways someone could try to get in.

---

## d) Bandit oh-five



