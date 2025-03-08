# Active-Directory
Set up and analyze AD domain compromises. Detect security events in Splunk. Perform brute-force attacks and analyze telemetry. Test Atomic Red Team techniques.
     		
            SOC PROJECT 1
          
            Active Directory 


                    Title: -
 creating a Active Directory Environment using a target machine (Windows 10) Attacker machine(kali) windows server (Active Directory) Ubuntu (Splunk) 






Created by: - 
Sudarshan Sinha


Objectives: -
The main objective of this setup is to give a knowledge about how in Active Directory the Domain I created and can be compromised so how to see that event in Splunk server which Is been connected over the network. Attempting a brute-force attack on to are target machine and see the telemetry generated on to our Splunk server and later test the Atomic Test form Atomic Red Team 
Logical Diagram of setup: -
Lab Environment Setup: -

Hardware requirement: -

Component	Minimum Requirement	Recommended Requirement
CPU	Intel i7 / AMD Ryzen 7 (8-core)	Intel i9 / AMD Ryzen 9 (12+ core)
RAM	8GB	12GB or more
Storage	512GB SSD	1TB+ NVMe SSD + 2TB HDD
Network	Standard Wi-Fi + 1GbE LAN	Multiple network interfaces (USB or PCIe NICs)
		
		
		
Software requirement: -
Virtualization and Hypervisor
To run multiple virtual machines (VMs) for attack/defense scenarios:
•	Hypervisor: VMware, VirtualBox, or KVM
•	Attacking machine – Kali Linux
•	Defending machine – Windows 10
•	Active Directory – Windows server 2022
•	Ubuntu machine – Splunk Server 
Virtualization installation: -
here I am using VirtualBox you can use other virtualization as per your choice.
 
Downloading virtual machine: -
1)	Visit the official site of VirtualBox: - 
  https://www.virtualbox.org/
2)	Select as per your Host OS. as I have Windows OS so I go with Windows hosts

3)	After downloading the VirtualBox you have to redirect to your downloads folder and search for VirtualBox and select it and
Press Enter.







Installing virtual machine: - 
1)after clicking to the VirtualBox you will be able to see this popup so,
    click next. 








2) In this you can choose your VirtualBox location but I will set it to default but you can change as per your prefer locations 
After selecting the path Press Next









3) Procced further with clicking on “Yes”.










4) In this Dependencies python core is missing So it will require Python to run VM if your PC contains python then it will not show you but I my PC it is not installed so it first installs python automatically then it will be able to run the VM.










	


4)	Here we complete with our installation process of VirtualBox 
“Click Finish”.










5)	After successfully completion of our installation we will able to see       this interface or dashboard to our screen










	


Windows 1o Setup: -
Downloading Windows 10 iso file: -
1)	Visit the Official Website of Microsoft and download windows 10 iso file: 
     https://www.microsoft.com/en-us/software-download/windows10/
2)	Download the ISO file and redirect to the folder where it is downloaded







3)	 click “yes” and proceed further…. 








4)	 “Accept” the license and move further with your installation








5)	Here two option is seen we have to select “Upgrade the PC now” as we don’t have install externally if we need to install our windows than we will create by other option seen below: - 












	
6)	let it be in default setting don’t change anything and click “Next”










7)	Select ISO file as we have to install internally and “click Next”. USB flash drive is used when we have to install windows externally with the help Pendrive or CD of compatibility. 










	

8)	Redirect to your folder where you have downloaded your windows ISO image in my PC I have download it into download folder you can change as per your choice: -










9)	Open VirtualBox 
>Click new
> Name your OS as per your choice.
>ISO Image: - select the ISO image which you have downloaded
 









10)	In Hardware setup set it to 4GB and in CPU set to default and check the checkbox and proceed further.


11)	Set it to 50 GB and click next










12)	 After setup of your hard drive space, you will able to see your windows setup to your left corner as my PC is Demo so now, we have to start our VM of windows for further process.


13)	 Install the Windows 10 click “Next” or you can select your language as per your preference…… 











14)	 click to “I don’t have a product key” and “click next”












15)	 Select “Windows 10 Pro” and “Click Next”











16)	select to custom and processed further…….










17)	  Here all partition will be seen as we have set to 50 GB hard disk Space so let it be and click next













18)	 Good to go all things are getting ready all installation will take some time have patience’s. 
After this it will setup the whole things and may restart few, time don’t be panic about that it takes time to do so …...








Kali Linux Setup: -
Download
1)	Visit the Official website of kali Linux
    https://www.kali.org/
2)	Click to Download






3)	Click to Virtual Machines as in that we don’t have to setup things it will have pre built things but if you want to setup manually than you can choose the Installer Images.









4)	Just check with your OS is it of 64 bit or 32 bits, in my PC 64 bit is supported so I go with 64 bit.
As we install VirtualBox so select the VirtualBox and download the file.
Note: - you can download as per your VMs 









5)	As the download has been done so we have to download 7-Zip file to extract 7-Zip file because the file which we have downloaded Is in format of 7-Zip format so to extract we to download
	Visit the website for 7-Zip download: - https://www.7-zip.org/
	click to download X64 








6)	After downloading the 7-Zip file, redirect to kali Linux download file to extract It with 7-Zip file 












7)	go to View -> file name extensions you will able to view the whole 
extension of the file 



8)	Doing so you are able to see the actual extension of the file here we have to click to. vbox extension file. It will simply add the kali Linux file to the VirtualBox.

	

9)	You will able to see the file is successfully added 
Its default credential is username – kali, Password-kali

Note: - You can change your username or password 

Network Configuration: -
There are few types of network settings one should know to setup their home labs according to their needs
Here's a table format for your VirtualBox Network Settings documentation:
Network Mode	What It Does	Good For	Limitations
NAT	Shares your computer’s internet connection with the VM.	Basic internet access; safe from outside connections.	Other devices can’t talk to the VM directly.
Bridged Adapter	Connects VM directly to your network like a separate device.	Communicating with other devices on the same network.	Less secure; exposed to network threats.
Host-Only Adapter	Only your computer and the VM can communicate.	Private VM-to-computer communication.	No internet unless extra setup is done.
Internal Network	VMs talk to each other but not your computer or the internet.	Creating an isolated network for VMs.	No connection to your computer or the internet.
NAT Network	Like NAT, but VMs can also communicate with each other.	VM-to-VM communication with internet access.	Requires extra setup.
Generic Driver	Custom networking setup for advanced users.	Special networking needs (rarely used).	Complex and requires special configuration.
Not Attached	No network connection for the VM.	Full isolation for testing in a secure environment.	No communication with any network.

 Diagrammatic representation: -










As I am setting up for a malware testing so I will set my VMs to Internal network so that the VMs doesn’t have the internet access but my VMs can communicate with each other 
	First, we setup for Windows 10 VM 
Just go to settings -> network -> select the Internal network option 
	Just give the name for the network in my VM I have given as “my_test”
	Click next

 


Now we will setup for kali Linux: -
	Go to setting click to network set it to Internal network and in name check for the network name which we setup for windows VM which Is “my_test”, After doing so both my windows and kali will communicate with each other 
	Click next 








After setting up the network we have to assign the IPs to both VMs statically 
first, we will set for windows VM 
	Click to “change adaptor options”











	Right click to ethernet option and select Properties










	Select the internet protocol version 4 -> properties










	here you assign the IPs manually 














	IP Is 192.168.20.10 subnet mask set as default 255.255.255.0 
	Note: - You can assign IP as per your choice here your network fundamentals come into play 










	Just go to command prompt and write a command “ipconfig” then you can able to see your assign IP 










	
	now in kali Linux you have to assign the IP so Go to edit Connections









	Select the Wired Connections 1 -> setting icon











	



	select the manual option  and assign the IP 192.168.20.11 subnet mask be as 24 












	just check your IP which you enter is been seen by writing the command on terminal 
	Command is “ifconfig”









	We have to assign the Ips to both the VMs so to ping to both we will open are Windows VMs to ping with kali Linux VM
	Command: - ping 192.168.20.11 
	Note: - you can ping with your IP I have ping my windows machine to kali machine so it is pinging to the kali machine 










Setup Splunk Server in Ubuntu
	Visit the Official site: - https://ubuntu.com/
	Select Server From given other options
	Click t0 Get Ubuntu Server






	Click to Download 24.04.2 LTS
	Note: - Update version may vary when it is been download 







	Similar to other machines we have to set the name In my “Ubuntu_splunk”
	Add ISO Image which we have downloaded 
	Check the skip unattended installation  
	Click “Next”











	Setting up the hardware as 4GB Base memory one can set their memory as per the Ram which they have in host machine
	CPU as 2
	Click “Next”










	Set Virtual Hard Disk as 100 GB
	Click “Next”











	we have started the Ubuntu VM for further process
	Step 1: - press Enter










	Step 2: - select Done and press Enter 














	Step 3: - click “Done”













	Step 4: - click “Done”












	Step 5: - click “Done”












	Step 6: - click to “Continue”











	Step 7: - click “Done”












	Step 8: - Click to “Continue”










	

	Setting up name , server name, username, password.
	Name: - cyberdefence
	server name: - splunk
	Username: - ubuntusplunk
	Password: - Splunk@123
	Note: -Set as per your Preferences










	Click to “Continue”









	










	From here your installation of ubuntu server will start…….
	Click to Done











	



	Here your ubuntu server in successfully installed…...











	you will get the failed message you have just ignore for now we will not fix then also it will work properly…so just ignore that message and press Enter








	

	Here we go we successfully installed our ubuntu server 
	Now we enter our username and password to start our server 
	Now we will run one command to update and upgrade our server
	sudo apt-get upgrade && sudo apt-get update 












After downloading all the VMs, Now, we have to install and configure Sysmon and Splunk to our windows target machine and windows server so that they can collect telemetry and send the logs over to our Splunk
	to do so we have to set our VMs into NAT Network so that they can Communicate with internet access with each other.






	Set up the name of the network as ADProject
	Network: - 192.168.10.0/24










	Select for ubuntu Splunk










	Same for windows server select network name 








	Set for windows 10 













	Same for Kali Linux Select the ADProject as a NET Network 




	Now, Open the Splunk server to check for the IP Which is been Assign to it as it been setup by default in DHCP so it will be assign a dynamic IP
	As we have to setup the static IP of 192.168.10.10
	To do so Run a Command – ip a
	As we are able to see that the IP which is been assign is different from which we have to assign so we will assign our IP








	









	Run the command sudo nano /etc/netplan/ and press tab you will get your file in my it is a 50-cloud-init.yaml it differ in different VMs
	Now we have to assign the IP make sure proper spaces is maintained
	Press Ctrl + x to save 
	Then press Enter and clear the screen 















	Run the command $ sudo netplan apply to apply the changes 
	then again run the command $ ip a to check whether our IP which we have assign is correctly done or not 
	Here we able to see it displaying the IP which we have assign 
	192.168.10.10/24













	Run the Command $ ping google.com to check its responding to it or not.
	to exit the pinging just press Ctrl+c









	Now we have to Setup the Splunk so we have to Download Splunk from Host Machine 
	Visit the Splunk Site: - https://www.splunk.com/
	Click to Splunk Enterprise -> Get My Free Trial










	Select Linux and Download the .deb file and save it in one folder 
with proper name of your choice 









	Open the Ubuntu Splunk 
	Run the Command $ sudo apt-get install virtualbox-guest-additions-iso












	run the command $ sudo reboot










	Now we have to add our users to vboxsf group
	Run a Command $ sudo adduser ubuntusplunk vboxsf
	Note: - you get the fatal error message that vboxsf doesn’t exist
So we have to download it 
        







	Run the Command $ sudo apt-get install virtualbox













	Run the Command $ sudo apt-get install virtualbox-guest-utils

	Run the command to reboot the VMs $ sudo reboot



	Now we will able to add our users to vboxsf group
	Again, we will run the command
	 $ sudo adduser ubuntusplunk vboxsf










	Now we have to create one Directory called share in which we have to add our Splunk ISO file
	Command $ mkdir share
	$ ls










	As we have created one directory so now, we have to mount our shared folder on the share directory.
	Run command $sudo mount -t vboxsf -o uid=1000,gid=1000 Splunk_ISO share/
	Note: - Splunk_ISO is a shared folder name which we added earlier and share/ is folder where we have to add the shared folder.
	Run the Command $ ls -la


	Run Command to change directory: - $ cd share 
	As we able to see our Splunk_ISO folder with splunk iso file, so now we have to install splunk
	Run command $ sudo dpkg -i splunk  and hit tab to have full file name
	Press Enter to install 




	run Command $ cd /opt/splunk
	$ ls -la
	$ sudo -u splunk bash
	$ cd bin
	To start installing we run the command: - $./splunk start
	Click to yes
	Admin name: - ubuntusplunk
	Password: - Splunk@123













	Now we have installed the Splunk so we have to ensure Splunk server should start when we login to our ubuntu server.
	$ exit 
	$ cd bin 
	$ sudo ./splunk enable boot-start-user ubuntusplunk
	Note: - make sure you have access to Splunk otherwise you have to add user then only it will be enabling the booting option.


Now we have to move to our Target machine (Windows 10)
	Changing the Device name to “target-PC” to easily identify my device name.
	Go to search bar
	Type pc -> go to properties
	Click to Rename the PC
	Rename your PC and Restart your PC









Check the IP Address of the machine
	Open the Command Prompt
	Run the Command ipconfig 
	A dynamic is displaying we have to assign a static IP of 192.168.10.100











	Go to network right click
	Click to open Network & adaptor options
	Click to change adapter options
	Click to ethernet
	Click to properties
	Select to Internet Protocol Version
	Click to Properties
	Assign the IP Address











	Check the IP address again
	Run the Command ipconfig
	Now it will display an ip of 192.168.10.100










To check whether your Splunk Server is working or not, so just to browser and enter the Ip address of server 192.168.10.10:8000 
	Note: - Splunk listen to port 8000 make sure you don’t forget it and make sure your Splunk server is open then only it will respond to it.

Now we have to download the Splunk Universal forwarder in our Target machine (Windows 10)
	Visit the Official website: - https://www.splunk.com/
	Click to Product-> Universal forwarder-> Get my Free download
	Download the windows 10 based as per your OS.

After download of Splunk universal forwarder , redirect yourself to the download directory 
	Click to install
	Check the licenses and agreement and other should be set to default.
	Click next










	Set as username admin
	Check the generate a random password
	Click next










	Deployment server we don’t have so click to next
	In receiving Indexer, we will give the Ubuntu Splunk Ip so that it responds to it.
	Hostname: - 192.168.10.10 
	Port set to default: - 9997











Now we have to download the Sysmon
	Visit the Official site for Sysmon: - https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon







	For Configuration we will search for Sysmon aloc config GitHub









	Select sysmonconfig.xml











	Click to Raw 
	right click to save as to download directory 











	Go to download Folder and unzip the Sysmon -> Extract all













	

	Go to Sysmon Folder and copy the path 
	C:\users\Cyber_Defence\Downloads\Sysmon 












	Open PowerShell as Run as Administrator
	Just run the command to change directory
	cd C:\users\Cyber_Defence\Downloads\Sysmon 












	Run the Command: - .\Sysmon.exe -I ..\sysmonconfig.xml












	Agree the licenses












Now we have to add our inputs.conf file 
	We are able to see our inputs.conf file but we don’t have to change that file 
	We are going to add over inputs.conf file into local directory
	It will in system directory 















	Open notepad as admin and copy pastes the data which I will give you in my GitHub repo by the file name called inputs.conf file 



Now as we save the inputs.conf then we have to restart our Splunk universal forwarder services, as we have updated our inputs.conf file so we have to restart its services again otherwise our changes would not be applied.
	Type in search bar -> services -> Run as admin -> Splunkforwarder-> click to NTservices-> click to log on-> check the log on as -> check the local system account -> Apply -> Click OK
	Now you look to log on as it will display local system 
	Start the service of Splunk forwarder
	And also check the Sysmon is also running.












Now we have to open our Splunk
	On windows 10 VMs
	Browse the address 192.168.10.10:8000
	Login -> ubuntusplunk
	Password-> Splunk@123
	Go to setting->indexes
	Note: - This is my credentials but you check with your credential you have created at the time Splunk setup.









Now you can recall that we have set our inputs.conf with indexes only of endpoint
	So we are able to see are available indexes but we are not able to see endpoint so will create it.










	Create with name endpoint and save it 











	Next, we have to enable Splunk to forward or receive	
	Go to Setting
	Click to forward and receiving.













	Under Receive data 
	Click to Configure Receiving
	Click to new Receiving Port
	We have set a port as 9997 So will enter that
Note: - If we setup the things correctly we should able to see data received or sending from our target machine.















	Click to Apps
	Select search & Reporting
	Click Skip
	Write on Search area index =” endpoint” time last 24 hours as we know we few minutes before we created it so we will set time to that only.









	Now we are able to see our target-pc name in host area











	We are able to see source values, Sysmon, Security, System, Application












	Note: - Same setup we have to do for Windows Server which I am skipping and processed further.

Now we have to install and configure Active Directory (Windows server)
On to our server and then we have to promote it to a domain controller. 
And finally configure the target machine (windows 10) to join our newly created domain.
	Setting up the device name of my Active Directory for ease identification.
	Go to PC -> Click to Properties -> Rename the PC -> Enter PC name as ADDC01 -> Click Next -> Restart your PC









	Setting up a static Ip address for Active Directory which we have to assign as per our Logical diagram.
	Go to network -> Open Network & internet setting -> change adapter option -> click to ethernet -> click to properties -> check for Ip version 4-> properties -> check the use the following Ip address 
	Add your Ip address of 192.168.10.7
	Default gateway as 192.168.10.1
	check the use following DNS server addresses and write 8.8.8.8 google DNS .











	Open CMD to Check with your Ip addresses
	Run the Command -> ipconfig /all 
	Ping google.com










We also check for Splunk server where it is responding or not make sure server is open then only it will respond to it.
	ping 192.168.10.10
	From this we can say that this is a connection between the computers.










Now, ahead over to server manager search for it….
	Go to manage 
	Add role and features 










	Installation type -> check Role Based or featured based installation
	Server Selection -> able to see the ADDC01 server name Ip addresses
	Server Roles -> Select Active Directory Domain Services -> Add features.
	Click next until you get install option.











What does Active Directory Domain Service will do? Why we have choosen this?
	ADDS Stores information about users, computers and other devices on the network. ADDS helps administrators securely manage this information and facilities resource sharing and collaboration between users.
After the installation of ADDS into the ADDC server….
	Flag icon beside the manage click to that
	Click to promote this server to domain controller
	Select Add a new forest as we are going to create a new Domain name as cyberdefence.local 
	Note: -you can create a domain name of your choice as well 
	Click next












	

	Set all things to default and create a password of your choice.











	we are able to see our paths for database, log files, SYSVOL.
	Click next 
	Again, install and system will restart automatically after installation.










	Now we are able to see our domain name with back slash which indicates that our domain server is configured to domain controller.
	Note: - the password is not been change it is same only the domain name is added.












Now we are going to Add some users….
	Go to tools in server manager
	Select Active Directory users and computer
Now you can explore the domain server, you been able to see the Built-in group in the right-hand side.
	Note: - You cannot add custom group to pre build groups like built-in is pre build groups so you can’t add custom group but you can you can create your own custom group and you can add pre build group to that custom groups.












	We have to create an organizational unit as IT & HR 
	We will create a user of the IT as of your choice you can create your own group.










	Inside IT just create a user by clicking to user










	As we have created these two groups, So we are going to head over to target machine and join it to a newly created domain called cyberdefence.local and authenticate using Sudarshan Sinha





	






Now we move ahead towards our target machine and set our DNS server.
DNS server is: - 192.168.10.7










	Now we check for are a PC and click to properties
	Click to advanced system settings
	Click to computer name click to change 
	Select domain and write domain name cyberdefence.local










	Now we are going to login with administrator  account as it will have proper functions
	Restart your PC











	we will login with a new user account which is our domain controller name Sudarshan Sinha password will your that password which you set a the time of creation of user for IT










Now we are going to setup the things in kali machine and will attempt a brute force attack and setup and install Atomic Red Team and Run Atomic tests.
We have setup our kali machine to statice Ip addresses of 192.168.10.250
	Go to ethernet icon and right click 
	Edit Connection
	Select Wired Connections
	Select the setting Icon
	Select IPv4 settings and set to manual set the address as 192.168.10.250/24
	DNS: - 8.8.8.8
	Click to save 











	
Open terminal check for Ip address whether it changed as not.
	Run the command Ip a
	We see that our Ip address doesn’t change, so go to ethernet Icon left click and disconnect it and then click again and select wired connection 1.











	now Ping the Google.com and our Splunk Server 
ping google.com
ping 192.168.10.10









	Now we will update and upgrade our repositories
	sudo apt-get update && sudo apt-get upgrade -y 

Now we are going to create a directory called AD-project to make it familiar, In this directory we are going save all the things which are going to do .
	mkdir AD-project











For our attack we are going to use our tool called crowbar….

	Run the Command sudo apt-get install -y crowbar

	Note: - Do not target any assets which will have different consequences just do for an educational purposes, labs and machine which only own to you.











	We are going to use the popular wordlist ‘Rockyou’ under directory 
cd /usr/share/wordlist/
ls
	We are able to see the Rockyou.txt.gz
	We have to unzip the file using gunzip
	Sudo gunzip rockyou.txt.gz
	ls









	cp Rockyou.txt ~/Desktop/AD-project
	Check inside the AD-project file is copied












	Run the command head -n 20 rockyou.txt, first 20 line is visible to you










	Run the command nano password.txt
	Add our actual password.










	Before we head over to attack the system we have to enable the remote desktop
	Go to target PC and enable the remote desktop their 
	PC -> properties-> advanced system settings-> login with admin account-> Remote->check the allow remote connections to the computer -> select users-> Add
	Add your users here 
	Sudarshan Sinha
	Krishna Shankar
	Check name 
	Click ok -> Apply






Back to kali machine 
	Run the command crowbar -h it will show all the command to know which command is required as we want rdp for Remote desktop protocol so we go with rdp 
	Command crowbar -b rdp -u sinhasudarshan -C passwords.txt 
-s 192.168.10.100/32
Note: - rdp is a protocol 
               -u username on which the attack to be done in my it is sinhasudarshan you can add your username which you have set in OU in AD DS.
192.168.10.100/32 it is the source Ip in which the attack to be done.














Now we are head over to Splunk server in target machine 192.168.10.10:8000
	Click search and reporting 
	Search for index=”endpoint” sinhasudarshan last 15 min










	Click to Eventcode and check for total events
	Event ID 4625 ,4624 etc to know how much event attempts is done 

	








	message indicates that sinhasudarshan’ s account is been successfully logged on
	In computer name we can see that the name is given with domain name @cyberdefence.local










Now we have to install Atomic red team to see our local account generates the telemetry to see in the Splunk server so just do that 
	Open PowerShell as Admin privileges login with admin account 
	Run Command: - Set-ExcutionPolicy Bypass CurrentUser
     










	We have to add Exclusion go to 
	Windows security->virus and threat protection->manage settings->under Exclusion->Add->add Exclusion -> folder
	This PC
	Select C drive 
	Select folder


















	Run the command IEX(IWR-UseBasicParsing);
	Run the command install-AtomicRedTeam -getatomics













	Go to C drive and search for a Atomic Red Team ->Atomics
	You will able to see the bunch of techniques Id
	Visit the MITRE ATT&CK Framework https://attack.mitre.org/ any of your choice and test it.
	Invoke -AtomicTest T1134.001












	This will automatically generate the telemetry with a local account
	Now we move over to Splunk and check for NewLocalUser
	We will not able to see that form this we can say that attacker may compromised with the local account as it will hidden not been seen.
	Note :- You can check for another test you may get local user their check for the same and explore other things as well…….





Important Links: -
	  https://www.virtualbox.org/
	     https://www.microsoft.com/en-us/software-download/windows10/
	    https://www.kali.org/
	 7-Zip download: - https://www.7-zip.org/
	https://ubuntu.com/
	MITRE ATT&CK Framework https://attack.mitre.org/
	https://www.splunk.com/
	https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon



