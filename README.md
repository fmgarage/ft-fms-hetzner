# ft-fms-hetzner (was fmserver-cloud)

Run FileMaker Server 19 for Linux in the Hetzner Cloud. We will add more (like VPN) in the next days.







## 1. Register an Account

Go to Hetzner and register a free account. You get a € 20,– credit to play with if you [follow our referral link](https://hetzner.cloud/?ref=KzxqMaXk51C8). In case you stay  with Hetzner, we receive a € 10,– bonus that we will donate to the [Stiftung Bildung](https://www.stiftungbildung.com). 



## 2. Add a Server

In the [Console](https://console.hetzner.cloud/projects) create a project and add a new server. You will need Centos 7 and we strongly recommend adding the SSH key for you local machine. You can start with the smallest configuration and scale up later when you need it. Start the server and ssh into it. When scaling up, you can choose to maintain the resource limits (e.g. 20G SSD) so you can scale down again at any time. 



## 3. Installation 

We recommend downloading the installer from your Claris account, unzipping it and upload it to your web server. On the one hand downloads from Claris are sometimes very slow and you can also run the installer without having to download and unpack it first. As a good practice we rename the rpm file and put it in a hard-to-guess folder.

`yum localinstall https://yourdomain.com/d0nf2tzu9e/fms-linux-installer.rpm -y`

This installs FileMaker Server interactively but you can aswell follow the instructions in the installer's readme files for an assisted install. 

When complete, check if your desired ports (80, 443, 5003, 16000, 16001) are listening:

`netstat -tulpn`

if necessary restart the fmshelper and check again.

`systemctl restart fmshelper`

After that you should be good to go.



## 4. Optional Measures

We will add additional documents for the individual topics.



#### Save a Snapshot

Configure your FileMaker Server and save a snapshot of the virtual machine. Next time you need a fresh install, use the snapshot as base.



#### Assign a floating IP

In the Hetzner Console you can 'install' an IP address that can be assigned to any server in your account. This can be used to configure a subdomain like **fmserver.yourdomain.com** and install an SSL certificate for your server.



#### Harden the Server

Your server is now publically available and most likely under attack already. We recommend to close all the ports you do not need, [disable ICMP ping](https://www.thegeekstuff.com/2010/07/how-to-disable-ping-replies-in-linux/) and [move SHH to a non-standard port](https://blog.devolutions.net/2017/4/10-steps-to-secure-open-ssh).



#### Access the Admin Console through SSH

You can disable port 16000 and use a tunnel:

`ssh root@yourserverip -L 16001:localhost:16001`

The admin console is now available at http://localhost:16001 on your local machine.



#### Set up a VPN

You can install WireGuard on the server: https://www.wireguard.com/install and close all public ports. You can access you database using the [Roadwarrior setup](https://www.thomas-krenn.com/en/wiki/WireGuard_Basics).



https://support.claris.com/s/answerview?anum=000026067&language=en_US
