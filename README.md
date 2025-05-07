<h1>Active Directory Project - Part 3</h1>

<p align="center">
<img src="https://snipboard.io/yGjrI1.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h2>Description</h2>
<br />
<p align="center">
Welcome to part three of five for the series on the active directory project. If you haven't seen the previous parts where we go over how to build out our diagram for this lab and install our virtual machines, I highly recommend that you go and see that first.
<br />
<br />
<img src="https://snipboard.io/K7SXd5.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
  Today's objective is to install and configure both Sysmon and Splunk onto our Windows target machine and Windows Server so they can start collecting telemetry and send logs over to our Splunk server. Let's get started. 
<br />
<br />
<img src="https://snipboard.io/5rq4A8.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
  To begin you want to head over to our Virtual Box and we want to make sure that our network settings are set to NAT network. This way our virtual machines can be on the same network and still have internet access. To do this, we can click on tools and then click on the bullet points. You want to make sure that you're selecting "Network".
  <br />
<br />
<img src="https://snipboard.io/XMrqDI.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/UvPQsN.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/usWcvM.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
  Over to the tabs there is "Host-only Networks", "NAT Networks", and "Cloud Networks". You want to select "NAT Network" and click on "Create". At the the bottom, I'll go ahead and name this to whatever you want but for me, I'll name it as "AD-Project" and I'll have the ipv4 prefix as the IP that we put in our diagram. If you recall it is '192.168.10.0/24'. I'll leave "Enable DHCP" checked and I will hit "Apply".
<br />
<br />
<img src="https://snipboard.io/yWdiG4.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/s7wCXl.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/WzTyhk.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Perfect, so now we created our own NAT network called "AD-Project". Let's head over to our Splunk server and we want to select "Settings" because now we want to change our "Network" settings over to NAT Network. Currently, if we select "Network" we do see our adapter attached to "NAT". We can select the drop-down and make sure we select "NAT Network".
<br />
<br />
<img src="https://snipboard.io/eAlCQT.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/x2ghUj.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
As for our name, if you have multiple networks make sure you select the one that you just created. For me, I only have one network called "AD-Project", so it automatically selects that for me. I'll go ahead and hit "OK" and we can do this for all of them.
<br />
<br />
<img src="https://snipboard.io/Vjv3zK.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So under our Active Directory Server, I'll select "Settings". Head over to "Network". Change it from "NAT" to "NAT Network", and hit "OK". I'll do this for my Windows machine as well, and finally my Kali machine. 
<br />
<br />
<img src="https://snipboard.io/RKEgkv.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/KnBCkh.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/MDh5kW.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/VzjmGt.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
  So heading into my Splunk machine. If I type in "ip a". We'll get an IP address of '192.168.10.9'. Again, from our diagram, we set the static IP of '.10'. So that means we'll have to set up a static IP on our Splunk server. To do that, we'll have to type in "sudo nano /etc/netplan/00-installer-config.yaml".
<br />
<br />
<img src="https://snipboard.io/eQFWbX.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/mltciV.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/g3oqwX.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Under the DHCP setting, currently, it is set to true, so we'll go ahead and replace it with "no". Indicating I do not want any DHCP. 
<br />
<br />
<img src="https://snipboard.io/tVROh3.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/b4EXTG.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
  I'll go ahead and press "Enter" for a new line and then I'll hit "Tab" three times. I'll type in "addresses: ". Now we enter in our IP address, so I want it '192.168.10.10/24'. If you are not sure what a '/24' is, I would encourage you to find some learning material on networking as this is extremely important to know.
<br />
<br />
<img src="https://snipboard.io/lLfV2b.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/jEU5cX.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
  Next, I'll hit "Enter" and hit "Tab" three times again. I'll type in "nameserver:". Then, I'll hit "Enter" again for a new line and this time I'll hit "Tab" five times. Similar to above, I'll type in "addresses:" and enter in the DNS IP that you want. I will use '8.8.8.8', which is Google's DNS. 
<br />
<br />
<img src="https://snipboard.io/m5tQyA.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/s6A1vV.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
  Hit "Enter" again. Hit "Tab" three times and we'll type "routes:" because we want to include a default route. Press "Enter" for a new line and hit "Tab" five times. Then I'll type in "- to: default" to indicate the default route. Let's create another new line and hit "Tab" six times. I'll type in "via: '192.168.10.1'" since we want to enter in our gateway.   Now we can go ahead and save out this configuration by holding cntrl + X. 
<br />
<br />
<img src="https://snipboard.io/oGNi7g.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/s1voXh.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/qceKnb.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
At the bottom, you'll see "Save modified buffer?", and you want to say yes. So type in "y" and hit "Enter".   So I just noticed a mistake that I made for "nameserver". We need to add an "s" at the end. So I'll do that, and now we can go ahead and save that out.
<br />
<br />
<img src="https://snipboard.io/kqfesd.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/a4xG0b.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/a6fVwX.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Clear out the screen and type in "sudo netplan apply", then hit "Enter". Now we will get a couple of warnings about permissions, but since we are in a lab environment it's fine to ignore them. I'll go ahead and clear out the screen.
<br />
<br />
<img src="https://snipboard.io/7wGiLj.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/UaejXv.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now I'll type in "ip a" again, and we now should see our IP address as '192.168.10.10'. We can type "ping google.com" and we'll see that there is a connection. I'll cancel that out by holding cntrl + c.
<br />
<br />
<img src="https://snipboard.io/0lmG4F.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/MdBeTj.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/ZVQPo0.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/uBkSwE.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
If you don't have any connectivity or you can't ping "google.com", do recheck your formatting. Now that we have connectivity and we have our static IP set, we can begin installing Splunk on your host machine. So your host, not your virtual machine. You want to head over to "splunk.com" and sign up with an account and log in. 
<br />
<br />
<img src="https://snipboard.io/mrvqSd.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So I'm over at "splunk.com" and you want to select sign up if you do not have an account. Once you're signed in, head over to "Products" and you want to click on "Free Trials and Downloads". Scroll down to "Splunk Enterprise". Click on "Get My Free Trial".
<br />
<br />
<img src="https://snipboard.io/qaE3O1.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/SmytDA.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/pz9d0T.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
You want to make sure you select Linux as your operating system. The one that we're interested in is the ".deb" file, so go ahead and select "Download Now". You want to save this in a directory of your choice. So for me, I'll save it under the directory of "Active-Directory-Project".
<br />
<br />
<img src="https://snipboard.io/wj5f4R.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/9WMOrI.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
The next step is to go back to our Splunk virtual machine and install the guest add-ons for virtual box. To do that, I'll clear out the screen and then I'll type in "sudo apt-get install VirtualBox" and then I'll hit "Tab" to see what kind of options are available.
<br />
<br />
<img src="https://snipboard.io/sildmp.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/pNx93c.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/5VTfct.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
We're interested in the "guest-additions-iso". So let's go ahead and type that out. Then I'll go ahead and hit "Enter". Type "y" for yes and hit "Enter". This will take some time depending on your download speeds. Once you see this screen go ahead and hit "Enter".
<br />
<br />
<img src="https://snipboard.io/fgHkh6.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/gbqZec.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/sX3qRh.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/MIgZOr.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now our package should be installed. We'll go ahead and clear out the screen and on the top you want to click on "Devices". Head over to "Shared Folders" and click on "Shared Folder Settings". Now we want to add a folder by clicking on this icon over here.
<br />
<br />
<img src="https://snipboard.io/QbW20u.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/LNt9pA.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/R5AhDe.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
For the folder path, we want to select the folder where we put our Splunk installer. So in my case, I download Splunk under the directory of "Active-Directory-Project". So I went ahead and selected that as my folder path. For my folder name, I'll leave it as default. 
<br />
<br />
<img src="https://snipboard.io/cp0ryG.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
As for the options, I'll select "read-only", "Auto-mount", and "Make Permanent". Then I'll hit "OK". Back onto our Splunk virtual machine, I'll go ahead and type in "sudo reboot" to reboot our virtual machine. We want to log back in using "mydfir" as the username and then the password. 
<br />
<br />
<img src="https://snipboard.io/XCye8L.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/wcPah0.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/o2y3S9.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, we want to add our user to the Virtual Box SF group and to do that we type in "sudo adduser" and then type in the username. So mine is "mydfir". Again, yours might be different depending on what you put. Then, I'll type in "vboxsf" and hit "Enter".
<br />
<br />
<img src="https://snipboard.io/dQu5ca.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Type in the password. Now, you might get the "group 'vbox SF' does not exist". There might be some additional guest installations that virtual box offers that we did not install yet. So we can type in "sudo apt-get install VirtualBox". Hit "Tab" again and we notice that there's "guest-utils".
<br />
<br />
<img src="https://snipboard.io/THu5v9.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/i7QPr9.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/hDwOFG.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Let's go ahead and type in "guest-utils" and hit "Enter". Go ahead and clear out the screen and I will reboot one more time. Log back in. Now let's try and add our user to that group. I'll type in "sudo adduser mydfir vboxsf". Now our user is added to that group.
<br />
<br />
<img src="https://snipboard.io/o8kVu2.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/m4MkLB.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/sLlJFq.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/iFGcDR.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
The next step is to create a new directory called "share" and to do that I'll type in "mkdir share". Hit "Enter". Type in "ls" and now we have the directory that we created called "share". We want to run the following command to mount our shared folder onto our directory called "share". To do that, we type in the command "sudo mount -t vboxsf -o uid=1000,gid=1000".
<br />
<br />
<img src="https://snipboard.io/8IXthP.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/aB1co8.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/4CqThg.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Then, we'll type in our shared folder name. In my case, it was "Active-Directory-Project", then I will point it to the "share" name that we just created. Now if you forget what your shared folder name is, you can go ahead and select "Devices", "Shared Folders", and "Shared Folders Settings...".
<br />
<br />
<img src="https://snipboard.io/hv87sA.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/7m2ajE.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/AxrhsJ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Double-click your "shared" folder and under folder name, this is the one that you want to use. In my case, it is "Active-Directory-Project" and I'll go ahead and hit "Enter". Now if you get an error for whatever reason, go ahead and try exiting the session to log out and then log back in. When you add your user into a new group, it doesn't take effect until you log out. 
<br />
<br />
<img src="https://snipboard.io/qxcHWU.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/GebWnN.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll type in "ls- la" and we can see that our "share" is now highlighted. So let's go ahead and change directories into that "share" and I'll type in clear to clear the screen.
<br />
<br />
<img src="https://snipboard.io/4kHhsX.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/ljySgQ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/GTvhdn.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Then type in "ls- la" and we get all of the files listed in that directory, including our Splunk installer. To install Splunk, we'll type in "sudo dpkg -i" and then point it over to our Splunk installer. Hit "Enter" and it should go out and do its thing. Now, once you see the word complete, we should be good to go to change into the directory of where Splunk is located onto our server.
<br />
<br />
<img src="https://snipboard.io/6EqrK0.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/lrCLPq.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/1JMEmF.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/ikTRh3.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
This will be under "cd /opt/splunk". So I'll change into that directory and then I'll type in "ls- la". Now you'll notice that all of the user and group belongs to "splunk". Which is a good thing as it limits the permissions to that user.
<br />
<br />
<img src="https://snipboard.io/p8n3GO.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/5eDboS.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/PSnuKh.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/s8S3gR.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Let's change into the user "splunk" by typing in "sudo -u splunk bash" and now we are acting as the user "splunk". Change into the directory called "cd bin" as the files listed in here, are all the binaries that Splunk can use.
<br />
<br />
<img src="https://snipboard.io/xriRog.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/CHkYa3.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/UE7jkR.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/HfUnhE.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
The one that we'll use is the "./splunk" and I'll type in "start" to run the installer. We'll get a license and terms agreements. We can go ahead and hit "q" and then type in "y" to accept.
<br />
<br />
<img src="https://snipboard.io/J4viAO.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/zt7I4G.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/JoH0Os.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
As for the administrative username, I'll type in "mydfir" and I'll enter in a password. Now that the installation is completed, let's run one more command to make sure that our Splunk starts up every time our virtual machine reboots. So I will type in "exit" to exit out of the user "splunk".
<br />
<br />
<img src="https://snipboard.io/4FZv2p.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/KtCN6h.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll change into the directory of "bin" and type in "sudo ./splunk enable boot-start " and I will put in the user flag as "splunk". This will make it so anytime the virtual machine reboots, Splunk will run with the user "splunk". 
<br />
<br />
<img src="https://snipboard.io/MDFmRg.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/EOBJ1V.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/1GgIBi.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/kFjQbS.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now that we have Splunk up and running, we want to install Splunk Universal Forwarder and Sysmon on both our Target machine and our server. I'll leave the server for you to install to get some hands-on experience. It is essentially the same process as the target machine.
<br />
<br />
<br />
<br />
On our target machine, I want to change up a couple things. First, I want to change our host name to call it "target" and to do that, we can search for "PC" and select "Properties". You want to click on "Rename this PC". so I'll type in "target-PC" for my computer name and I'll hit "Next". Then we'll go ahead and restart the computer. 
<br />
<br />
<img src="https://snipboard.io/OM3zfE.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/vfEU6i.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/U8OFhN.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/0Ef54F.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Once we're back in, let's double-check our computer name by typing in "PC" again. Click on "Properties" and we see that our device name is now "target-PC". The next thing we want to do is search for "cmd" and click on "Command Prompt. We want to take a look at our IP address by doing typing "ipconfig".
<br />
<br />
<img src="https://snipboard.io/x3Gs1z.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/Xda5nc.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/VUzvS4.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/qNxJ4v.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now if we take a look the IP address is '192.168.10.7'. If you recall, our diagram '10.7' is going to be our Windows Server. So I will actually go ahead and change this into a different IP address. To do that, I'll right-click the "Network" icon.
<br />
<br />
<img src="https://snipboard.io/kmD81O.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/Bd9fsO.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Click on "Open Network and Internet settings". Scroll down to "Change adapter options". I'll right-click the adapter. Click on "Properties" and double-click the "Internet Protocol version 4" or you can go ahead and just select "Properties".
<br />
<br />
<img src="https://snipboard.io/5Dl9oY.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/jAbvWg.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/F7cfMb.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/jAJ9Ci.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I'll use the following IP address and then I'll set a static IP. So let's say '192.168.10.100'. Now my network is a '/24', so that means it's a '255.255.255.0' and the default gateway is '192.168.10.1'. For the DNS server, let's put in '8.8.8.8'. For now, I'll hit okay and close it out.
<br />
<br />
<img src="https://snipboard.io/0xwvBd.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now if we go ahead and type in 'ipconfig' again, we should have an updated IP address of '192.168.10.100'. So there won't be any IP conflict happening. We can also go ahead and open up a web browser and let's try accessing our Splunk server. So our Splunk was on '192.168.10.10' on Port '8000'. Just as an FYI, Splunk listens on Port '8000' so make sure that you specify the port otherwise you will not connect to Splunk and as you can see we can access its login page.
<br />
<br />
<img src="https://snipboard.io/CD5ZmL.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/5xPwUG.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/DNxs2P.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/AWtYn5.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now let's install Splunk Universal Fowarder by heading over to "splunk.com". So I'll go to "splunk.com" and then we'll log in using the account that we just created or if you have an existing account. Once you're signed in, you want to select "Products". Head over to "Free Trials and Downloads" and scroll all the way down until you see "Universal Fowarder".  Click on "Get My Free Download" and you want to make sure that you select the correct operating system. Since my target machine is running on a 64-bit Windows operating system, I'll select 64-bit.
<br />
<br />
<img src="https://snipboard.io/EzhtB0.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/Aw5SRe.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/rcsxuq.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Once the download is completed, you can go ahead and select "Downloads" and double-click the MSI file. Click on "Check this box to accept the License Agreement". Make sure that you're selecting the first option, which is "An on-premises Splunk Enterprise instance". Hit "Next".
<br />
<br />
<img src="https://snipboard.io/IOsn8i.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/YPmo9I.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
For the username, I'll just type in "admin" and I'll leave the "Generate random password" checked. Click on "Next". For the deployment server, we don't have one so we can go ahead and skip that. As for the receiving indexer, this is going to be our Splunk server.
<br />
<br />
<img src="https://snipboard.io/4d1xu0.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/aoKdIV.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/2OMNmZ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So the IP of the Splunk server is '192.168.10.10'. The default port for Splunk is '9997' when it's receiving events. So I'll leave that as '9997'. Select "Next" and "Install". We want to start downloading Sysmon, so I'll go ahead and just search up "Sysmon" and we'll select "Sysmon - Sysinternals". 
<br />
<br />
<img src="https://snipboard.io/qyBxDe.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/1Gz0Ki.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/RZ3XiV.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Scroll down and click on "Download Sysmon" and I'll go ahead and let that download. The Sysmon configuration, that we'll be using is by Olaf. So search up "Sysmon olaf config" and we'll click on the GitHub. Scroll down, and we want to select "sysmonconfig.xml".
<br />
<br />
<img src="https://snipboard.io/brJuS8.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/xsQ54R.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/7NpurB.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Click on "Raw" on the right-hand side. Then right-click "Save as" and I'll save it under my downloads directory. Now let's head over to our downloads directory and we should see Sysmon downloaded. So we'll right-click it and click on "Extract All".
<br />
<br />
<img src="https://snipboard.io/O415i2.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/xAnvDa.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/eAui4q.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/MUJgbQ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Click "Extract". What I'll do is click on the file explorer bar and then right-click "Copy". Now I'll open up Powershell with administrative privileges. So search up "Powershell" and select "Run as administrator". Now the reason why I copied the file path is so I can just go ahead and type in "cd" to change the directory and paste the file path.
<br />
<br />
<img src="https://snipboard.io/RZd7zw.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/hxC6SR.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/3xEoMk.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/Qifol2.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now that I'm in that directory, we can type in "sys" and hit "Tab". We'll use "-i" flag to indicate that I want to specify a configuration file. Now, if you take a look at my directory, it is currently set as "C:\Users\bob\Downloads\Sysmon". My Sysmon config is located under my downloads directory.
<br />
<br />
<img src="https://snipboard.io/FTJcj3.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So that means I need to go back a directory and to do that we can specify two dots to indicate that I want to go back one directory, followed by a backslash. Now, I can type "sysmon". Keep hitting "Tab" until you get your Sysmon "config.xml". Now, go ahead and hit "Enter" and this will install Sysmon for you once you've hit "Agree".
<br />
<br />
<img src="https://snipboard.io/wozy4i.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/wozy4i.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, that it says "Sysmon64" started and we see an MSI orange icon indicating that Universal forwarder was successfully installed, close it out by clicking on "Finish". I'll close out Powershell and now here is the most important part. We need to instruct our Splunk forwarder on what we want to send over to our Splunk server.
<br />
<br />
<img src="https://snipboard.io/rPm5np.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
To do this, we must configure a file called "inputs.conf". This file is located under the "C:drive" program files. Click on "SplunkUniversalFowarder". Next, click on "etc". Then, click on "system". Finally, click on "default" and here's the file, "inputs.conf". 
<br />
<br />
<img src="https://snipboard.io/9q4Qgi.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/rzylHe.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/vmyobJ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/h3s6fE.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, we can go ahead and right-click copy but instead, I'm going to create a new file under the "local" directory because you do not want to edit the "inputs.conf" file under the default directory. That is there just in case you mess anything up, you can replace that with the default config. 
<br />
<br />
<img src="https://snipboard.io/CEMZAf.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/0BFgLp.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So just to make sure that we're all on the same page because this is an important step, "do not edit the inputs.conf" file under the default directory. Instead, we will create a new file under the local directory and we'll name it as "inputs.conf".
<br />
<br />
<img src="https://snipboard.io/0BFgLp.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, this directory requires administrative privileges. As you can see, I cannot create anything other than a folder. So what I'll do is search up "notepad" and I'll run this as administrator. Now I've copied the contents in my "inputs.conf" file that I'll leave in the description down below where you can go and copy all of that content and paste it into your virtual machine.
<br />
<br />
<img src="https://snipboard.io/V9bqkp.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/UlYSkT.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/9p2qOa.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
This is instructing our Splunk Forwarder to push events related to application, security, system, and Sysmon over to our Splunk server. Take note of the index that we're using. In my configuration file I have the index pointing to an index name called "endpoint". This is important to know because whatever events fall under these categories, will be sent over to Splunk and placed under the index endpoint. If our Splunk server does not have an index-named endpoint, it will not receive any of these events.
<br />
<br />
<br />
<br />
Now if you want to learn more about this, I recommend you read Splunk's documentation. Again, I'll leave a link down below for you to go ahead and just copy all of this to make sure it works. Now I will save this notepad file under "Program Files", "Splunk Universal Forwarder", "etc", scroll down to "system" and put it into the local directory.
<br />
<br />
<img src="https://snipboard.io/4my0YT.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/0YlEWA.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I will call this "inputs" and change the "Save as type" to "All Files" and I'll put an extension as ".conf", short for configuration. Click on "Save". Exit this out and now we should see "inputs.conf" under our local directory. 
<br />
<br />
<img src="https://snipboard.io/nebyBN.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/mnGugH.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/mn1aZC.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Do note that anytime you update your "inputs.conf" file, you must restart Splunk's Universal Forwarder service. In order to do that, we'll go ahead and just search up "Services". Then, run as administrator. Type in "s" to look for Splunk's Forwarder service. 
<br />
<br />
<img src="https://snipboard.io/4LbHqD.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/rRI1GC.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/j4bRLB.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, one thing to keep in mind is if you scroll to the right, under the column of "Log On As". If you see "NT SERVICE", we'll go ahead and just double click it and click on "Log On". If you notice that it's using this account "NT SERVICE\SplunkFowarder", it might not be able to collect logs due to some of the permissions.
<br />
<br />
<img src="https://snipboard.io/ze1Bs9.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/AiC8LE.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
So instead, you want to select "Local System account" and hit "Apply". It'll say "The new log-on name will not take effect until you stop and restart the service." Which is what we'll do because we updated our "inputs.conf" file. I can't stress this enough, if you update your "inputs.conf" file, you must restart your Splunk Fowarder service otherwise it won't take effect.
<br />
<br />
<img src="https://snipboard.io/caR48C.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/RLmu4a.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Click on "OK" and now if you look at our column "Log On As", it is now "Local System". That is exactly what we want and just to verify, if we scroll down just a little bit, we do see "Sysmon64" and it is running. Let's go ahead and right-click "SplunkFowarder" and you can click on "Restart" or you can click on restart right on the top left.
<br />
<br />
<img src="https://snipboard.io/1wFVHE.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/Hb6Mg0.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/1h3RQu.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, you might get hit with a warning saying that "Windows cannot stop the SplunkFowarder service on the Local Computer." That's okay, just go ahead and hit "Ok" and start the service. Now, we have our Sysmon and Splunk Universal forwarder installed, along with our updated "inputs.conf" file.
<br />
<br />
<img src="https://snipboard.io/S8xoKm.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/i2HCtg.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Now, we can finalize our Splunk server configuration. Let's head over to our Splunk web portal and log in using the credentials that we created during the Splunk install on our server. So my username was "mydfir". Then, my secure password. When we're presented with this screen, we want to select "Settings" at the top.
<br />
<br />
<img src="https://snipboard.io/DQK1VW.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/lynpQO.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/etqVFa.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Then, head over to "Indexes". Now, if you recall the "inputs.conf" file, all of the events are being sent over to an index called "endpoint". This is where we create that index. So if we scroll down, if you look to the left, these are all of the indexes that Splunk has. However, as you can see, we do not see an index called "endpoint". So let's go ahead and create that. 
<br />
<br />
<img src="https://snipboard.io/fHC7lG.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/eVH1jn.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Scroll up and click on "New Index". As for the name, I'll type in "endpoint" and click on "Save". Now, a new index named "endpoint" should be created. To double-check, just scroll down and we should see the "endpoint" index. Perfect.
<br />
<br />
<img src="https://snipboard.io/JXLjBf.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/wh9EtC.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/O0pSDI.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Next, we need to make sure that we enable our Splunk server to receive the data. To do that, we need to click on "Settings". Click on "Forwarding and receiving". Under the receive data, we want to click on "Configure receiving". Click on "New receiving Port".
<br />
<br />
<img src="https://snipboard.io/32z9oT.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/ZDAmaY.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/owr6Ui.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
If you recall, during our setup we mentioned the default port is '9997'. So let's type in '9997' and hit "Save". If we have everything set up correctly, we should start seeing data coming in from our target machine. Click on "Apps" on the top left corner and select "Search and Reporting".
<br />
<br />
<img src="https://snipboard.io/t3U48W.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/Uun3dS.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
In the search bar, we'll type in "index=endpoint" and take a look at our time frame. It has "Last 24 hours", which is perfectly fine. Now, I'll click on the search button and we'll see some events.
<br />
<br />
<img src="https://snipboard.io/aeKzlX.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/P8hbfW.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/eCyBfT.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
If we scroll down just a little bit, we see one host and the value is "TARGET-PC". We also see some sources, Source types, our "inputs.conf" file. Aswell as the specifically mentioned "Security", "Application", "System", and the Sysmon data.
<br />
<br />
<img src="https://snipboard.io/EiCm79.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/vjc6A2.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
You have successfully installed and configured Sysmon and Splunk. If you do want to learn more about Splunk, I do recommend you take a look at their documentation as they are quite detailed. Now it is your turn to set up the server to have both Sysmon and Splunk installed and configured. Make sure that you're using the same "inputs.conf" file as the target machine, and you can grab a copy down below. Remember to restart the Splunk service after you have your "inputs.conf" updated. 
<br />
<br />
<br />
<br />
On the server, let's change the computer name to "ADDC01". To do that, you want to search "PC" and right click click on "Properties". Then, you want to select "Rename this PC". We want to type in "ADDC01". Click on "Next" and restart. Once that is completed, you can then move on to installing Sysmon and Splunk.
<br />
<br />
<img src="https://snipboard.io/N5Ki9y.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/NCwbie.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://snipboard.io/BT1vJH.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
If you have everything set up correctly in Splunk, you should see two hosts. One for the "TARGET-PC" and the other for "ADDC01".
<br />
<br />
<img src="https://snipboard.io/WKh2Vi.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
I hope that everything went smoothly for you and you have learned some new things about Splunk. If you did come across something that you aren't too sure of or want to learn more about, do try and research it. Now, we went over a lot of material and configuration so I am sure that there will be some errors along the way, but you and I will get through it together. In part four, we will begin to install and configure your active directory. That will be it for the video. Remember to stay curious and do things differently.
