<h1>SOC Automation (Home Lab) - Part 1</h1>

<p align="center">
<img src="https://snipboard.io/6rb2ue.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h2>Description</h2>
<br />
<p align="center">
welcome to part three of five for the series on the active directory project if you haven't seen the previous Parts where we go over how to build out our diagram for this lab and install our virtual machines I highly recommend that you go and watch that first today's objective is to install and configure both sysmon and Splunk onto our Windows Target machine and Windows Server so they can start collecting Telemetry and send logs over to our Splunk server let's get started to begin you want to head over to our virtual box and we want to make sure that our network settings are set to natat network this way our virtual machines can be on the same network and still have internet access to do this we can click on tools and then click on the bullet points you want to make sure that you're selecting Network and over to the tabs there is hostonly network net Network and Cloud networks you want to select Nat Network and click on create at the the bottom I'll go ahead and name this to whatever you want but for me I'll name it as ad project and I'll have the ipv4 prefix as our IP that we put in our diagram if you recall it is 192.168.10.0 sl24 I'll leave enable DHCP checked and I will hit apply perfect so now we created our own natat network called ad project let's head over to our split L server and we want to select settings because now we want to change our network settings over to Nat Network currently if we select Network we do see our adapter attached to natat we can select the drop down and make sure we select Nat Network and as for our name if you have multiple networks make sure you select the one that you just created for me I only have one network called ad project so it automatically selects that for me I'll go ahead and hit okay and we can do this for all of them so under our active directory server I'll select settings head over to network change it from Nat to net Network make sure that it is selecting my network name and hit okay I'll do this for my Windows machine as well and finally my Cali machine net Network hit okay perfect so heading into my Splunk machine if I type in IP space a we'll get an IP address of 192.168 do10 9 and again from our diagram we set the static IP of10 so that means we'll have to set up a static IP on our Splunk server to reflect that and to do that we'll have to type in PSE sudo Nano Etsy SL net plan slash and then you can tab to autocomplete we should only have one file called installer dasc config so this is the correct one that we want under the DHCP setting currently it is set to true so we'll go ahead and remove that and I'll just type in no indicating I do not want any DHCP I'll go ahead and press enter for a new line and then I'll hit tab three times 1 2 3 and I'll type in addresses with a colon hit space and in square brackets we now enter in our IP address so I want it 192.168.10.10 followed by a sl24 if you are not sure what a sl24 is I would encourage you to find some learning material on networking as this is extremely important to know I'll close this off with another square bracket next I'll hit enter and hit three tabs again so 1 2 3 and I'll type in name server with a colon space I'll hit enter again for a new line and this time I'll hit tab five times 1 2 3 4 5 and similar to above I'll type in addresses colon and square bracket and enter in the DNS IP that you want I will use 8.8.8.8 which is Google's DNS hit enter again hit tab three times 1 2 3 and we will type in routes because we want to include a default route press enter for new line and hit tab five times 1 2 3 4 5 I'll add a dash and type two colon default to indicate default route and let's enter in another new line and hit tab six times 1 2 3 4 5 6 and I will type in Via colon 1 192 168 10.1 we want to enter in our Gateway now we can go ahead and save out this configuration by holding control X at the bottom you'll see save modified buffer with a question mark you want to say yes so just type in y and hit enter so I just noticed a mistake that I did for name server we need to add in an s so name servers and now we can go ahead and save that out clear out the screen and type in pseudo net plan apply hit enter now we will get a couple warnings about permissions but since we are in a lab environment it's fine to ignore I'll go ahead and clear out the screen and now I'll type in IPA again and we now should see our IP address as 192168 1010 we can try and ping google.com and we see that there is a connction ction I'll cancel that out by holding contrl C and if you don't have any connectivity or you can't ping google.com do recheck your formatting and if you do get any errors leave it down in the comment section below now that we have connectivity and we have our static IP set we can begin installing Splunk on your host machine so your host not your virtual machine you want to head over to splunk.com and sign up with an account and log in so I'm over at splunk.com and you want to select sign up if you do not have an account once you're signed in head over to products and you want to click on free trials and downloads scroll down to Splunk Enterprise click on get my free trial and you want to make sure you select Linux as your operating system the one that we're interested in is the Deb file so go ahead and select download now and you want to save this in a directory of your choice so for me I will save it under the directory of active directory project the next step is to go back to our Splunk virtual machine and install the guest add-ons for virtual box to do that I'll clear out the screen and then I'll type in pseudo apt get install virtual box and then I'll hit tab to see what kind of options are available we're interested in the guest additions ISO so let's go ahead and type that out guest Das editions now you can use tab for autoc completion and then I'll go ahead and hit enter type y for yes and hit enter and this will take some time depending on your download speeds once you see this screen go ahead and hit enter now our package should be installed we'll go ahead and clear out the screen and on the top you want to click on devices head over to Shared folders and click on shared folder settings and now we want to add a folder by clicking on this icon over here for the folder path we want to select the folder where we put our Splunk installer in so in my case I download loed Splunk under the directory of active directory project so I went ahead and selected that as my folder path for my folder name I'll leave it as default the one that it just populated and as for the options I'll select readon autom Mount and make permanent then I'll hit okay hit okay back onto our Splunk virtual machine I'll go ahead and type in pseudo reboot to reboot our virtual machine we want to log back in with using my dfir as the username and then the password and now we want to add our user to the vbox SF group and to do that we type in pseudo add user and then type in the username so mine is my dfir again yours might be different depending on what you put and then I'll type in vbox SF and I'll hit enter type in the password now you might get the group vbox SF does not exist there might be some additional guest installations that virtual box offers that we did not install yet so we can type in pseudo app get install virtual box hit tab again and we notice that there's guest Das utils let's go ahead and type in guest D utils and hit enter go ahead and clear out the screen and I will reboot one more time go ahead and log back in and now let's try and add our user to that group P sudo add user my dfir vbox SF and now our user is added to that group the next step is to create a new directory called share and to do that I'll type in mkdir and then type in share hit enter type in LS and we do have it is very hard to see but we do have the folder called share now that our directory has been created called share we want to run the following command to mount our shared folder onto our directory called share to do that we type in the command pseudo Mount DT vbox sf- o uid equal 1000 comma gal 1000 space and then we'll type in our shared folder name in my case it was active-directory Das project and I will point it to the share name that we just created now if you forget what your shared folder name is you can go ahead and select device shared folders shared folder settings double click your shared folder and under folder name this is the one that you want to use in my case it is active-directory d project and I'll go ahead and hit enter now if you get an error for whatever reason go ahead and try exiting the session to log out and then log back in because when you add your user into a new group it doesn't take effect until you log out I'll type in ls- LA and we can see that our share is now highlighted so let's go ahead and change directories into that share and I'll type in clear to clear with the screen and type in ls- LA and we get all of the files listed in that directory including our Splunk installer to install Splunk we'll type in pseudo dpkg dasi and then point it over to our Splunk installer hit enter and it should go out and do its thing now once you see the word complete we should be good to go to change into the directory of where Splunk is located onto our server this will be under SL opt SL Splunk so I'll change into that directory and then I'll type in ls- La now you'll notice that all of the user and group belongs to Splunk which is a good thing as it limits the permissions to that user let's change into the user Splunk by typing in pseudo- Splunk bash and now we are acting as the user Splunk change into the directory called bin as the files listed in here are all the binaries that Splunk can use the one that we'll use is the for SLS Splunk and I'll type in start to run the installer we'll get a license and terms agreements we can go ahead and hit q and then type in y to accept as for the administrative username I'll type in my dfir and I'll enter in a password now that the installation is completed let's run one more command to make sure that our Splunk starts up every time our virtual machine reboots so I will type in exit to exit out of the user Splunk I'll change into the directory of Bin and type in PSE sudo SLS spunk enable boot Dart and I will put in the user flag as Splunk this will make it so anytime the virtual machine reboots Splunk will run with the user Splunk now that we have Splunk up and running we want to install Splunk Universal forer and cismon on both our Target machine and our server I will leave the server for you to install to get some hands-on experience it is essentially the same process as the target machine on our Target machine I want to change up a couple things first and foremost I want to change our host name to call it Target and to do that we can search for PC and select properties and you want to click on rename this PC so I'll type in Target DPC for my computer name and hit next and then we'll go ahead and restart the computer once we're back in let's double check our computer Name by typing in PC again and click on properties and we see that our device name is now Target PC the next thing we want to do is search for CMD and click on command prompt we want to take a look at our IP address by doing ip config now if we take a look the IP address is 1 192.168.10.0 if you recall our diagram 10.7 is going to be our Windows Server so I will actually go ahead and change this into a different IP address to do that I'll rightclick the network icon click on open network and internet settings scroll down to change adapter options I'll right click the adapter click on properties and double click the the Internet Protocol version 4 or you can go ahead and just select properties I'll use the following IP address and then I'll set a static IP so let's say 1 192.168.1.100 now my network is a sl24 so that means it is a 255.255.255.0 and the default gateway is 1 192.168.1.1 for the DNS server let's put in 8.8.8.8 for now I'll hit okay and close it out now if we go ahead and type in IP config again we should have an updated IP address of 192.168.1.100 so there won't be any IP conflict happening we can also go ahead and open up a web browser and let's try accessing our Splunk server so our Splunk was on 192.168.10.10 on Port 8000 just as an FYI Splunk listens on Port 8 ,000 so make sure that you specify the port otherwise you will not connect to Splunk and as you can see we can access its login page now let's install Splunk Universal forer by heading over to splunk.com so I'll go to splunk.com and then we'll log in using the account that we just created or if you have an existing account once you're signed in you want to select products head over to free trials and downloads and scroll all the way down until you see un IAL for click on get my free download and you want to make sure that you select the correct operating system and since my target machine is running on a 64bit Windows operating system I will select 64-bit once the download is completed you can go ahead and select downloads and doubleclick the MSI file click on check this box to accept the license agreement make sure that you're selecting the first option which is an on premise Splunk Enterprise instance and hit next for the username I'll just type in admin and I'll leave the Generate random password checked click on next the deployment server we don't have one so we can go ahead and skip that as for the receiving indexer this
16:11
is going to be our Splunk server so the
16:14
IP of the Splunk server is
16:17
192168101 the default port for Splunk is
16:21
9997 when it's receiving events so I'll
16:24
leave that as 9997 and select next and
16:28
install we want to start downloading
16:30
cismon so I'll go ahead and just search
16:32
up cismon and we'll select the cismon by
16:36
sis internals scroll down and click on
16:38
download cismon and I'll go ahead and
16:40
let that download the cismon
16:42
configuration that we'll be using is by
16:44
Olaf so search up Olaf config and that's
16:48
the one we'll click on his GitHub scroll
16:50
down and we want to select cismon
16:54
config.xml click on Raw on the right
16:57
hand side and then then right click save
17:00
as and I'll save it under my downloads
17:03
directory now let's head over to our
17:05
downloads directory and we should see
17:06
cison downloaded over here so we'll
17:09
right click it and click on extract all
17:12
click extract and what I'll do is I'll
17:14
click on the file explorer bar and then
17:17
right click copy and now I'll open up
17:20
Powershell with administrative
17:22
privileges so search up Powershell and
17:25
select run as administrator select yes
17:28
now the reason why I copied the file
17:30
path is so now I can just go ahead and
17:33
type in CD to change directory and paste
17:36
in the file path and now I'm in that
17:38
directory so we can type in CIS and hit
17:41
tab until we hit cis1 64.exe we'll use
17:45
the - I flag to indicate that I want to
17:48
specify a configuration file now if you
17:51
take a look at my directory it is
17:53
currently set at C users Bob downloads
17:57
slsy my cismon config is located under
18:01
my downloads directory so that means I
18:04
need to go back one directory and to do
18:06
that we can specify two dots to indicate
18:09
that hey I want to go back One Directory
18:12
followed by a backs slash now I can
18:14
search cismon and hit tab keep hitting
18:17
tab until you get your cismon config.xml
18:21
now go ahead and hit enter and this will
18:23
install cismon for you once you hit
18:25
agree now that it says cismon 6 4
18:28
started and we see an MSI orange icon
18:32
over here indicating that hey Universal
18:34
forwarder was successfully installed
18:37
close it out by clicking on finish I'll
18:39
close out Powershell and now here is the
18:42
most important part we need to instruct
18:45
our Splunk forwarder on what we want to
18:48
send over to our Splunk server to do
18:52
this we must configure a file called
18:55
inputs. com this file is is actually
18:58
located under the C drive program files
19:02
Splunk Universal forer Etsy system
19:06
default and here's the file inputs. com
19:10
now we can go ahead and rightclick copy
19:13
but instead I'm actually going to create
19:15
a new file under the local
19:18
directory because you do not want to
19:20
edit the inputs. com file under the
19:23
default directory that is there just in
19:26
case you mess anything up you can
19:29
replace that with the default config so
19:31
just to make sure that we're all on the
19:33
same page because this is an important
19:35
step do not edit the inputs. comom file
19:40
under the default
19:42
directory instead we will create a new
19:46
file under the local directory and we'll
19:49
name it as inputs. comom now this
19:53
directory requires administrative
19:56
privileges as you can see I cannot
19:58
create anything other than a folder so
20:00
what I'll do is I'll search up notepad
20:03
and I will run this as administrator
20:06
click on yes now I've copied the
20:08
contents in my inputs. comom file that
20:11
I'll leave in the description down below
20:13
where you can go and copy all of that
20:15
content and paste it into your virtual
20:17
machine this is instructing our Splunk
20:20
forwarder to push events related to
20:24
application security and system as well
20:27
as syis on over to our Splunk server
20:31
take note of the index that we're using
20:33
in my configuration file I have the
20:35
index pointing to an index name called
20:37
endpoint this is important to know
20:39
because whatever events fall under these
20:41
categories will be sent over to Splunk
20:44
and placed under the index endpoint if
20:47
our Splunk server does not have an index
20:50
named endpoint it will not receive any
20:53
of these events now if you want to learn
20:55
more about this I recommend you read
20:57
Splunk
20:58
documentation again I'll leave a link
21:01
down below for you to go ahead and just
21:03
copy all of this to make sure it works
21:05
now I will save this notepad file under
21:07
program files Splunk Universal forer
21:10
Etsy scroll down to system and put it
21:14
into the local directory I will call
21:16
this inputs change the save as type to
21:20
all files and I'll put an extension as
21:23
do comp short for configuration click on
21:27
Save exit the out and now we should see
21:30
inputs. comom under our local directory
21:33
do note that anytime you update your
21:35
inputs. comom file you must restart
21:37
splunk's Universal forwarder service in
21:40
order to do that we'll go ahead and just
21:42
search up services run as administrator
21:45
and type in s and we want to look for
21:48
Splunk forwarder service right here now
21:51
one thing to keep in mind is if you
21:53
scroll to the right under the column of
21:55
log on as if you see n n service so
21:59
we'll go ahead and just double click it
22:00
and click on log on if you notice that
22:02
it's using this account ENT service
22:06
Splunk for it might not be able to
22:09
collect logs due to some of the
22:11
permissions so instead you want to
22:13
select local system account and hit
22:15
apply it'll say hey the new log on name
22:18
will not take effect until you stop and
22:20
restart the service which is what we'll
22:22
do because we updated our inputs. comom
22:25
file I can't stress this enough if you
22:27
update your inputs. comom file you must
22:29
restart your Splunk forward service
22:32
otherwise it won't take effect click on
22:35
okay and now if you look at our column
22:37
log on as it is now local system that is
22:41
exactly what we want and just to verify
22:44
we scroll down just a little bit we do
22:46
see cismon 64 and it is running let's go
22:49
ahead and right click Splunk for and you
22:52
can click on restart over here or you
22:54
can click on restart right here on the
22:56
top left now you might get hit with a
22:59
warning saying that windows cannot stop
23:01
the Splunk forer service on the local
23:03
computer that's okay just go ahead and
23:05
hit okay and just start the service now
23:08
we have our cismon installed and Splunk
23:11
Universal forwarder installed along with
23:14
our updated inputs. comom file now we
23:17
can finalize our Splunk server
23:20
configuration let's head over to our
23:22
Splunk web portal and log in using the
23:24
credentials that we created during the
23:27
Splunk is install on our server so my
23:29
username was my dfir then my password
23:33
when we're presented with the screen we
23:35
want to select settings at the top and
23:37
then head over to indexes now if you
23:39
recall the inputs. comom file all of the
23:42
events are being sent over to an index
23:45
called endpoint this is where we create
23:49
that index so if we scroll down if you
23:52
look to the left these are all of the
23:53
indexes that Splunk has and as you can
23:56
see we do not see an index index called
23:58
endpoint so let's go ahead and create
24:00
that scroll all the way up and click on
24:02
new index as for the name I'll type in
24:05
endpoint and click on Save now a new
24:08
index named endpoint should be created
24:10
to double check just scroll down and we
24:12
should see the endpoint index perfect
24:16
next we need to make sure that we enable
24:18
our Splunk server to receive the data in
24:21
order to do that we click on settings
24:24
click on forwarding and receiving under
24:27
the re receive data we want to click on
24:29
configure receiving click on new
24:32
receiving port and if you recall during
24:34
our setup we mentioned the default Port
24:37
of
24:38
9997 so let's type in 9997 and hit save
24:42
if we have everything set up correctly
24:44
we should start seeing data coming in
24:46
from our Target machine click on apps on
24:49
the top left corner and select search
24:51
and Reporting we'll go ahead and skip
24:53
this box here skip tour and under the
24:56
search bar we'll we type in index equals
24:59
endpoint and take a look at our time
25:01
frame it has last 24 hours which is
25:04
perfectly fine and I'll click on the
25:06
search button we do see some events
25:08
2,000 events and if we scroll down just
25:11
a little bit we see one host and the
25:13
value is Target PC we also see some
25:16
sources and Source type our inputs.
25:19
comom file specifically mentioned the
25:22
Security application system and syson
25:26
data and we see that all here you have
25:29
successfully installed and configured
25:31
sysmon and Splunk if you do want to
25:35
learn more about Splunk I do recommend
25:37
you take a look at their documentation
25:40
as they are quite detailed now in my
25:42
sock course we go over slunk and how to
25:45
build queries to look for evil which is
25:49
going to be a great experience if you
25:51
are interested in the course I'll leave
25:53
a link down below for you to sign up now
25:56
it is your turn to set set up the server
25:58
to have both cismon and Splunk installed
26:01
and configured make sure that you're
26:03
using the same inputs. comom file as the
26:06
target machine and you can grab a copy
26:08
on my GitHub page or in the description
26:11
down below remember to restart the spunk
26:14
service after you have your inputs.
26:17
comom updated on the server let's change
Change Server Name
26:20
the computer name to addc 01 to do that
26:24
you want to search PC and right click
26:27
click on properties and then select
26:29
rename this PC we want to type in ad
26:33
dc01 click on next and restart once that
26:36
is completed you can then move on to
26:39
installing sysmon and Splunk if you have
26:42
everything set up correctly in Splunk
26:44
you should see Two Hosts one for the
26:47
Target PC and the other for ad DC now
26:50
when you do get this window you just
26:53
click on continue I hope that everything
26:55
went smoothly for you and you have
26:57
learned learn some new things about
26:58
Splunk if you did come across something
27:01
that you aren't too sure of or want to
27:02
learn more about do try and research it
27:05
now we went over a lot of material and
27:09
configuration so I am sure that there
27:12
will be some errors along the way but
27:14
you and I will get through it together
27:17
as a reminder links to my sof course and
27:20
inputs. comom file will be in the
27:22
description Down Below in part four we
27:25
will begin to install and configure your
27:27
active directory if you stay till the
27:30
end I'll be doing a giveaway and to
27:32
enter all you really need to do is leave
27:34
a heart in the comment section down
27:36
below and that will be it for the video
27:39
remember to stay curious and do things
27:45
differently
