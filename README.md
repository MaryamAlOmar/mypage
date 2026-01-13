# mypage
"Lab" user NTLM hash decrypted
googleplus
root.txt
THM{aea1e3ce6fe7f89e10cea833ae009bee}
Everyone prefers a graphical user interface (GUI) until they master a command-line interface (CLI). There are many reasons for that. One reason is that GUIs are usually intuitive. If someone offers you a GUI interface you are unfamiliar with, you can quickly poke around and discover a non-trivial part. Compare this with dealing with a CLI, i.e., a prompt.

CLI interfaces usually have a learning curve; however, as you master the command line, you will find it faster and more efficient. Consider this trivial example: How many clicks do you need to find your IP address using the graphical desktop? Using the command-line interface, you don’t even need to raise your hands off the keyboard. Let’s say you want to recheck your IP address. You need to issue the same command instead of moving the mouse pointer to every corner of your screen.

There are many other advantages to using a CLI besides speed and efficiency. We will mention a few:

Lower resource usage: CLIs require fewer system resources than graphics-intensive GUIs. In other words, you can run your CLI system on older hardware or systems with limited memory. If you are using cloud computing, your system will require lower resources, which in turn will lower your bill.
Automation: While you can automate GUI tasks, creating a batch file or script with the commands you need to repeat is much easier.
Remote management: CLI makes it very convenient to use SSH to manage a remote system such as a server, router, or an IoT device. This approach works well on slow network speeds and systems with limited resources.
Learning Objectives
The purpose of this room is to teach you how to use MS Windows Command Prompt cmd.exe, the default command-line interpreter in the Windows environment. We will learn how to use the command line to:

Display basic system information
Check and troubleshoot network configuration
Manage files and folders
Check running processes
Room Prerequisites
Before starting this room, you should have finished the Windows and AD Fundamentals module.

Press the Start Machine button below.


Start Machine
Start the AttackBox by pressing the Start AttackBox button at the top of this page. The AttackBox machine will start in Split-Screen view. If it is not visible, use the blue Show Split View button at the top of the page.
You can use the SSH client on the AttackBox to connect to MACHINE_IP with the following credentials:

Username: user
Password: Tryhackme123!
Establishing an SSH Connection from the AttackBox
If this is the first time you initiate an SSH connection from the AttackBox to a target system, the steps are shown in the screenshot below, and they are the following:

Start the AttackBox’s terminal by clicking the terminal icon marked with 1.
To connect to the target VM, issue the command ssh user@MACHINE_IP as user is the username in this case.
Because this is your first time connecting to this target VM, you will be asked to trust this connection. Answer with yes as marked with 3.
Enter your password Tryhackme123!. Please note that the password will not appear as you type it.
Starting the terminal on the AttackBox and connecting the target VM using SSH.

Answer the questions below
What is the default command line interpreter in the Windows environment?
cmd.exe

Correct Answer
Task 2
Basic System Information
Task 3
Network Troubleshooting
Most of us are used to looking up MS Windows network configuration from the GUI interface. The command-line interface provides many networking-related commands to look up your current configuration, check ongoing connections, and troubleshoot networking issues.

Network Configuration
You can check your network information using ipconfig. The terminal output below shows our IP address, subnet mask, and default gateway.

Terminal
C:\>ipconfig

Windows IP Configuration

Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : eu-west-1.compute.internal
   Link-local IPv6 Address . . . . . : fe80::90df:4861:ba40:f2a8%4
   IPv4 Address. . . . . . . . . . . : 10.10.230.237
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . . : 10.10.0.1
You can also use ipconfig /all for more information about your network configuration. As shown in the terminal below, we can view our DNS servers and confirm that DHCP is enabled.

Terminal
C:\>ipconfig /all

Ethernet adapter Ethernet 3:

   Connection-specific DNS Suffix  . : eu-west-1.compute.internal
   Description . . . . . . . . . . . : Amazon Elastic Network Adapter
   Physical Address. . . . . . . . . : 02-B7-DF-1D-0D-99
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::90df:4861:ba40:f2a8%4(Preferred) 
   IPv4 Address. . . . . . . . . . . : 10.10.230.237(Preferred) 
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Lease Obtained. . . . . . . . . . : Wednesday, May 1, 2024 2:38:05 PM
   Lease Expires . . . . . . . . . . : Wednesday, May 1, 2024 4:08:07 PM
   Default Gateway . . . . . . . . . : 10.10.0.1
   DHCP Server . . . . . . . . . . . : 10.10.0.1
   DHCPv6 IAID . . . . . . . . . . . : 134353458
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-27-E3-D1-2B-0E-F8-30-D0-72-3F
   DNS Servers . . . . . . . . . . . : 10.0.0.2
   NetBIOS over Tcpip. . . . . . . . : Enabled
Network Troubleshooting
One common troubleshooting task is checking if the server can access a particular server on the Internet. The command syntax is ping target_name. Inspired by ping-pong, we send a specific ICMP packet and listen for a response. If a response is received, we know that we can reach the target and that the target can reach us.

Let’s find out if we reach example.com. In the terminal output below, we can see that we have successfully received four replies. Furthermore, we got some statistics; for instance, the average round trip time is 78 milliseconds.

Terminal
C:\>ping example.com

Pinging example.com [93.184.215.14] with 32 bytes of data:
Reply from 93.184.215.14: bytes=32 time=78ms TTL=52
Reply from 93.184.215.14: bytes=32 time=78ms TTL=52
Reply from 93.184.215.14: bytes=32 time=78ms TTL=52
Reply from 93.184.215.14: bytes=32 time=78ms TTL=52

Ping statistics for 93.184.215.14:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 78ms, Maximum = 78ms, Average = 78ms
Another valuable tool for troubleshooting is tracert, which stands for trace route. The command tracert target_name traces the network route traversed to reach the target. Without getting into more details, it expects the routers on the path to notify us if they drop a packet because its time-to-live (TTL) has reached zero. The terminal output below shows that we passed through 15 routers before reaching our target.

Terminal
C:\>tracert example.com

Tracing route to example.com [93.184.215.14]
over a maximum of 30 hops:

  1    59 ms    32 ms    42 ms  ec2-3-248-240-3.eu-west-1.compute.amazonaws.com [3.248.240.3]
  2     *        *        *     Request timed out.
  3     *        *        *     Request timed out.
  4     *        *        *     Request timed out.
  5     *        *        *     Request timed out.
  6     *        *        *     Request timed out.
  7     *        *        *     Request timed out.
  8     *        *        *     Request timed out.
  9    <1 ms    13 ms    <1 ms  100.100.2.56
 10    15 ms    11 ms    11 ms  ae-42.a03.londen12.uk.bb.gin.ntt.net [131.103.117.104]
 11    17 ms    11 ms    12 ms  ae-14.r20.londen12.uk.bb.gin.ntt.net [129.250.3.248]
 12    81 ms    80 ms    80 ms  ae-7.r20.nwrknj03.us.bb.gin.ntt.net [129.250.6.147]
 13    83 ms    83 ms    86 ms  ae-0.a02.nycmny17.us.bb.gin.ntt.net [129.250.3.9]
 14    79 ms    79 ms    96 ms  ce-0-3-0.a02.nycmny17.us.ce.gin.ntt.net [128.241.1.14]
 15    81 ms    86 ms    79 ms  ae-67.core1.nyd.edgecastcdn.net [152.195.68.135]
 16    78 ms    78 ms    78 ms  93.184.215.14

Trace complete.
More Networking Commands
One networking command worth knowing is nslookup. It looks up a host or domain and returns its IP address. The syntax nslookup example.com will look up example.com using the default name server; however, nslookup example.com 1.1.1.1 will use the name server one.one.one.one. The terminal below shows the output of both commands. The results are identical; however, you can see that the answers were retrieved from different name servers.

Terminal
C:\>nslookup example.com
Server:  ip-10-0-0-2.eu-west-1.compute.internal
Address:  10.0.0.2

Non-authoritative answer:
Name:    example.com
Addresses:  2606:2800:21f:cb07:6820:80da:af6b:8b2c
          93.184.215.14

C:>nslookup example.com 1.1.1.1
Server:  one.one.one.one
Address:  1.1.1.1

Non-authoritative answer:
Name:    example.com
Addresses:  2606:2800:21f:cb07:6820:80da:af6b:8b2c
          93.184.215.14
The final networking command we will cover in this room is netstat. This command displays current network connections and listening ports. A basic netstat command with no arguments will show you established connections, as shown below. In this case, we only have one SSH connection; we figured out it is SSH because it is bound to port 22.

Terminal
C:\>netstat

Active Connections

  Proto  Local Address          Foreign Address        State
  TCP    10.10.230.237:22       ip-10-11-81-126:53486  ESTABLISHED
If you are curious about the other options, you can run netstat -h, where -h displays the help page. We opted for the following options:

-a displays all established connections and listening ports
-b shows the program associated with each listening port and established connection
-o reveals the process ID (PID) associated with the connection
-n uses a numerical form for addresses and port numbers
We combine these four options and execute the netstat -abon command. The result is quite long, but we display the first few lines in the terminal below. It is clear now that the executable sshd.exe is responsible for listening for incoming connections on port 22, as shown in the first line. We can also see the process ID (PID) associated with each connection.

Terminal
C:\>netstat -abon

Active Connections

  Proto  Local Address          Foreign Address        State           PID 
  TCP    0.0.0.0:22             0.0.0.0:0              LISTENING       2116
 [sshd.exe]
  TCP    0.0.0.0:135            0.0.0.0:0              LISTENING       820
  RpcSs 
 [svchost.exe]
[...]
  TCP    0.0.0.0:49669          0.0.0.0:0              LISTENING       2036
 [spoolsv.exe]
  TCP    0.0.0.0:49670          0.0.0.0:0              LISTENING       584 
 Can not obtain ownership information
  TCP    0.0.0.0:49686          0.0.0.0:0              LISTENING       592
 [lsass.exe]
  TCP    10.10.230.237:22       10.11.81.126:53486     ESTABLISHED     2116 
 [sshd.exe]
 [...]
Answer the questions below
Which command can we use to look up the server’s physical address (MAC address)?
ipconfig /all

Correct Answer

What is the name of the service listening on port 135?

RpcSs

Correct Answer
What is the name of the service listening on port 3389?

TermService

Correct Answer
Task 4
File and Disk Management
Task 5
Task and Process Management
You must be familiar with MS Windows Task Manager and might be familiar with killing non-responsive processes. Let’s discover how to achieve a similar functionality using the command line.

We can list the running processes using tasklist.

Terminal
C:\>tasklist

Image Name                     PID Session Name        Session#    Mem Usage 
========================= ======== ================ =========== ============
System Idle Process              0 Services                   0          8 K
System                           4 Services                   0         88 K
Registry                        84 Services                   0     50,700 K
smss.exe                       276 Services                   0      1,132 K
csrss.exe                      372 Services                   0      5,264 K
wininit.exe                    448 Services                   0      6,892 K
csrss.exe                      456 Console                    1      5,028 K
winlogon.exe                   516 Console                    1     11,144 K
services.exe                   584 Services                   0      7,492 K
lsass.exe                      592 Services                   0     16,108 K
svchost.exe                    704 Services                   0     23,432 K
fontdrvhost.exe                736 Console                    1      4,256 K
[...]
Some filtering is helpful because the output is expected to be very long. You can check all available filters by displaying the help page using tasklist /?. Let’s say that we want to search for tasks related to sshd.exe, we can do that with the command tasklist /FI "imagename eq sshd.exe". Note that /FI is used to set the filter image name equals sshd.exe.

Terminal
C:\>tasklist /FI "imagename eq sshd.exe"

Image Name                     PID Session Name        Session#    Mem Usage
========================= ======== ================ =========== ============
sshd.exe                      2116 Services                   0      6,992 K
sshd.exe                      2712 Services                   0      7,668 K
sshd.exe                      4752 Services                   0      7,372 K
With the process ID (PID) known, we can terminate any task using taskkill /PID target_pid. For example, if we want to kill the process with PID 4567, we would issue the command taskkill /PID 4567.

Answer the questions below
What command would you use to find the running processes related to notepad.exe?
tasklist /FI "imagename eq notepad.exe"

Correct Answer
What command can you use to kill the process with PID 1516?
taskkill /PID 1516

Correct Answer
Task 6
Conclusion
Task 6
Conclusion
In this room, we focused on the most practical commands for accessing a networked system over the command line.

We intentionally omitted a few common commands as we didn’t see a real value for including them in a beginner room. We mention them below so that you know that the command line can be used for other tasks.

chkdsk: checks the file system and disk volumes for errors and bad sectors.
driverquery: displays a list of installed device drivers.
sfc /scannow: scans system files for corruption and repairs them if possible.
It is important to remember all the commands covered in the previous tasks; moreover, it is equally important to know that /? can be used with most commands to display a help page.

In this room, we used the command more in two ways:

Display text files: more file.txt
Pipe long output to view it page by page: some_command | more
Equipped with this knowledge, we now know how to display the help page of a new command and how to display long output one page at a time.

Now that you know the Windows command line, it is time to move to the Windows PowerShell room.

Answer the questions below
The command shutdown /s can shut down a system. What is the command you can use to restart a system?
shutdown /r

Correct Answer

What command can you use to abort a scheduled system shutdown?
shutdown /a

Correct Answer
How likely are you to recommend this room to others?

Task 1
Windows Editions
The Windows operating system has a long history dating back to 1985, and currently,  it is the dominant operating system in both home use and corporate networks. Because of this, Windows has always been targeted by hackers & malware writers.

Windows XP was a popular version of Windows and had a long-running. Microsoft announced Windows Vista , which was a complete overhaul of the Windows operating system. There were many issues with Windows Vista. It wasn't received well by Windows users, and it was quickly phased out.

When Microsoft announced the end-of-life date for Windows XP, many customers panicked. Corporations, hospitals, etc., scrambled and tested the next viable Windows  version , which was Windows 7, against many other hardware and devices. Vendors had to work against the clock to ensure their products worked with Windows 7 for their customers. If they couldn't, their customers had to break their agreement and find another vendor that upgraded their products to work with Windows 7. It was a nightmare for many, and Microsoft took note of it.

Windows 7, as quickly as it was released soon after, was marked with an end of support date.  Windows 8.x came and left and it was short-lived, like Vista.

Then arrived Windows 10 followed by Windows 11, which is the current Windows operating system version for desktop computers.

Windows 11 comes in 2 flavors, Home and Pro. You can read the difference between the Home and Pro here.

Even though we didn’t talk about servers, the current version of the Windows operating system for servers is Windows Server 2025.

Many critics like to bash on Microsoft, but they have made long strides to improve the usability and security with each new version of Windows .

Note : The Windows edition for the attached VM is Windows Server 2019 Standard, as seen in   System Information .

Update : As of June 2021, Microsoft announced the retirement dates for Windows 10 here . 

" Microsoft will continue to support at least one Windows 10 Semi-Annual Channel until October 14, 2025 ".

As of October 5th, 2021 - Windows 11 now is the current Windows operating system for end-users. Read more about Windows 11 here .  

Answer the questions below
What encryption can you enable on Pro that you can't enable in Home?
BitLocker

Correct Answer
Task 2
The Desktop (GUI)
Task 3
Introduction to Windows

Start Machine
 

The Windows operating system (OS) is a complex product with many system files, utilities, settings, features, etc. 

This module will attempt to provide a general overview of just a handful of what makes up the Windows OS, navigate the user interface, make changes to the system, etc.  The content is aimed at those who wish to understand and use the Windows OS on a more comfortable level. 

Press the Start Machine button below to launch the attached virtual machine.

The virtual machine should open within your web browser. 

If you want to access the virtual machine via Remote Desktop , use the credentials below. 

Machine IP :  MACHINE_IP

User :  administrator

Password :  letmein123!



Accept the Certificate when prompted, and you should be logged into the remote system now.

Note : The virtual machine may take up to 3 minutes to load.

Answer the questions below
Read above and start the virtual machine.
No answer needed

Correct Answer
Task 4
The File System
The file system used in modern versions of  Windows  is the New Technology File System or simply  NTFS .

Before NTFS, there was  FAT16/FAT32 (File Allocation Table) and HPFS (High Performance File System). 

You still see FAT partitions in use today. For example, you typically see FAT partitions in USB devices, MicroSD cards, etc.  but traditionally not on personal Windows computers/laptops or Windows servers.

NTFS is known as a journaling file system. In case of a failure, the file system can automatically repair the folders/files on disk using information stored in a log file. This function is not possible with FAT.   

NTFS addresses many of the limitations of the previous file systems; such as: 

Supports files larger than 4GB
Set specific permissions on folders and files
Folder and file compression
Encryption ( Encryption File System or EFS )
If you're running Windows, what is the file system your Windows installation is using? You can check the Properties (right-click) of the drive your operating system is installed on, typically the C drive (C:\).

  

You can read Microsoft's official documentation on FAT, HPFS, and NTFS here . 

Let's speak briefly on some features that are specific to NTFS. 

On NTFS volumes, you can set permissions that grant or deny access to files and folders.

The permissions are:

Full control
Modify
Read & Execute
List folder contents
Read
Write
The below image lists the meaning of each permission on how it applies to a file and a folder. (credit  Microsoft )



How can you view the permissions for a file or folder?

Right-click the file or folder you want to check for permissions.
From the context menu, select Properties .
Within Properties, click on the Security tab.
In the Group or user names list, select the user, computer, or group whose permissions you want to view.
In the below image, you can see the permissions for the Users group for the Windows folder. 



Refer to the Microsoft documentation to get a better understanding of the NTFS permissions for  Special Permissions .

Another feature of NTFS is Alternate Data Streams ( ADS ).

Alternate Data Streams  (ADS) is a file attribute specific to Windows  NTFS  (New Technology File System).

Every file has at least one data stream ( $DATA ), and ADS allows files to contain more than one stream of data. Natively Window Explorer doesn't display ADS to the user. There are 3rd party executables that can be used to view this data, PowerShell also gives you the ability to view ADS for files. We will cover how you can use PowerShell to view any ADS for any files in the Windows PowerShell room.

From a security perspective, malware writers have used ADS to hide data.

Not all its uses are malicious. For example, when you download a file from the Internet, there are identifiers written to ADS to identify that the file was downloaded from the Internet.

To learn more about ADS, refer to the following link from MalwareBytes here . 

Bonus : If you wish to interact hands-on with ADS, I suggest exploring Day 21 of  Advent of Cyber 2 .

Answer the questions below
What is the meaning of NTFS?
New Technology File System

Correct Answer
Task 5
The Windows\System32 Folders
Task 5
The Windows\System32 Folders
The Windows folder ( C:\Windows ) is traditionally known as the folder which contains the Windows operating system. 

The folder doesn't have to reside in the C drive necessarily. It can reside in any other drive and technically can reside in a different folder.

This is where environment variables, more specifically system environment variables, come into play.  Even though not discussed yet, the system  environment variable for the Windows directory is %windir% .

Per Microsoft , " Environment variables store information about the operating system environment. This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders ".

There are many folders within the 'Windows' folder. See below.



One of the many folders is System32 . 



The System32 folder holds the important files that are critical for the operating system.

You should proceed with extreme caution when interacting with this folder. Accidentally deleting any files or folders within System32 can render the Windows OS inoperational. Read more about this action here . 

Note : Many of the tools that will be covered in the Windows Fundamentals series reside within the System32 folder. 

Answer the questions below
What is the system variable for the Windows folder?
%windir%

Correct Answer
Task 6
User Accounts, Profiles, and Permissions
Task 6
User Accounts, Profiles, and Permissions
User accounts can be one of two types on a typical local Windows system: Administrator & Standard User. 

The user account type will determine what actions the user can perform on that specific Windows system. 

An Administrator can make changes to the system: add users, delete users, modify groups, modify settings on the system, etc. 
A Standard User can only make changes to folders/files attributed to the user & can't perform system-level changes, such as install programs.
You are currently logged in as an Administrator. There are several ways to determine which user accounts exist on the system. 

One way is to click the Start Menu and type Other User. A shortcut to System Settings > Other users should appear. 



If you click on it, a Settings window should now appear. See below.



Since you're the Administrator, you see an option to Add someone else to this PC.

Note: A Standard User will not see this option.  

Click on the local user account. More options should appear: Change account type and Remove. 



Click on Change account type. The value in the drop-down box (or the highlighted value if you click the drop-down) is the current account type. 



When a user account is created, a profile is created for the user. The location for each user profile folder will fall under is C:\Users.

For example, the user profile folder for the user account Max will be C:\Users\Max.

The creation of the user's profile is done upon initial login. When a new user account logs in to a local system for the first time, they'll see several messages on the login screen. One of the messages, User Profile Service, sits on the login screen for a while, which is at work creating the user profile. See below.

 

Once logged in, the user will see a dialog box similar to the one below (again), indicating that the profile is in creation.



Each user profile will have the same folders; a few of them are:

Desktop
Documents
Downloads
Music
Pictures
Another way to access this information, and then some, is using Local User and Group Management. 

Right-click on the Start Menu and click Run. Type lusrmgr.msc. See below



Note: The Run Dialog Box allows us to open items quickly. 

Back to lusrmgr, you should see two folders: Users and Groups. 

If you click on Groups, you see all the names of the local groups along with a brief description for each group. 

Each group has permissions set to it, and users are assigned/added to groups by the Administrator. When a user is assigned to a group, the user inherits the permissions of that group. A user can be assigned to multiple groups.

Note: If you click on Add someone else to this PC from Other users, it will open Local Users and Management. 

Answer the questions below
What is the name of the other user account?

tryhackmebilly

Correct Answer
What groups is this user a member of?

Remote Desktop Users,Users

Correct Answer
What built-in account is for guest access to the computer?
Guest

Correct Answer
What is the account description?

window$Fun1!

Correct Answer
Task 7
User Account Control
Task 7
User Account Control
The large majority of home users are logged into their Windows systems as local administrators. Remember from the previous task that any user with administrator as the account type can make changes to the system.

A user doesn't need to run with high (elevated) privileges on the system to run tasks that don't require such privileges, such as surfing the Internet, working on a Word document, etc. This elevated privilege increases the risk of system compromise because it makes it easier for malware to infect the system. Consequently, since the user account can make changes to the system, the malware would run in the context of the logged-in user.

To protect the local user with such privileges, Microsoft introduced User Account Control (UAC). This concept was first introduced with the short-lived Windows Vista  and continued with versions of Windows that followed.

Note : UAC (by default) doesn't apply for the built-in local administrator account. 

How does UAC work? When a user with an account type of administrator logs into a system, the current session doesn't run with elevated permissions. When an operation requiring higher-level privileges needs to execute, the user will be prompted to confirm if they permit the operation to run. 

Let's look at the program on the account you're currently logged into, the built-in administrator account—Right-click to view its Properties.

In the Security tab, we can see the users/groups and their permissions to this file. Notice that the standard user is not listed. 



Log in as the standard user and try to install this program. To do this, you can remote desktop into the machine as the standard user account. 

Note : You have the username and password for the standard user. It's visible in lusrmgr.msc .

Before installing the program, notice the icon. Do you see the difference?  When you're logged in as the standard user, the shield icon is on the program's default icon. See below.



This shield icon is an indicator that UAC will prompt to allow higher-level privileges to install the program.



Double-click the program, and you'll see the UAC prompt. Notice that the built-in administrator account is already set as the user name and prompts the account's password. See below.



After some time, if a password is not entered, the UAC prompt disappears, and the program does not install. 

This feature reduces the likelihood of malware successfully compromising your system. You can read more about UAC here.

Answer the questions below
What does UAC mean?
User Account Control

Correct Answer
Task 8
Settings and the Control Panel
Task 8
Settings and the Control Panel
On a Windows system, the primary locations to make changes are the Settings menu and the Control Panel.

For a long time, the Control Panel has been the go-to location to make system changes, such as adding a printer, uninstall a program, etc. 

The Settings menu was introduced in Windows 8, the first Windows operating system catered to touch screen tablets, and is still available in Windows 10. As a matter of fact, the Settings menu is now the primary location a user goes to if they are looking to change the system. 

There are similarities and differences between the two menus. Below are screenshots of each.

Settings :



Control Panel : 



Now, if you want to see which applications are installed on the system, click Programs button shown here in the control panel. Then select Programs and Features. This will list all installed applications along with their names, publishers, and versions. In this way, you can verify any software that has been added to the system. The screenshot below shows the installed applications of another machine through this feature:



Note : The icons for Settings might be different in the version of Windows on your personal device. 

Both can be accessed from the Start Menu. See below.



Control Panel is the menu where you will access more complex settings and perform more complex actions. In some cases, you can start in Settings and end up in the Control Panel.

For example, in Settings, click on Network & Internet . From here, click on Change adapter options . 



Notice that the next window that pops up is from the Control Panel. 



If you're unclear which to open if you wish to change a setting, use the Start menu and search for it. 

In the example below, the search was 'wallpaper.' Notice that few results were returned. 



If we click on the Best match, a window to the Settings menu appears to make changes to the wallpaper. 



Answer the questions below
In the Control Panel, change the view to Small icons. What is the last setting in the Control Panel view?
Windows Defender Firewall

Correct Answer
Task 9
Task Manager
Task 9
Task Manager
The last subject that will be touched on in this module is the Task Manager.

The Task Manager provides information about the applications and processes currently running on the system. Other information is also available, such as how much CPU and RAM are being utilized, which falls under Performance. 

You can access the Task Manager by right-clicking the taskbar. 



Task Manager will open in Simple View and won't show much information. 



Click on More details, and the view changes.



You can refer to this blog post for more detailed information about the Task Manager.

If you wish to learn more about the core Windows processes and what each process is responsible for, visit the Core Windows Processes room. 

Answer the questions below
What is the keyboard shortcut to open Task Manager?
Ctrl+Shift+Esc

Correct Answer
Task 10
Conclusion

Task 1
Introduction

We will continue our journey exploring the Windows operating system. 

In Windows Fundamentals 1, we covered the desktop, the file system, user account control, the control panel, settings, and the task manager. 

This module will attempt to provide an overview of some other utilities available within the Windows operating system and different methods to access these utilities.

Press the Start Machine button below to launch the attached virtual machine.


Start Machine
If you wish to access the virtual machine via Remote Desktop, use the credentials below. 

Machine IP: MACHINE_IP

User: administrator

Password: letmein123!



Accept the Certificate when prompted, and you should be logged into the remote system now.

Note: The virtual machine may take up to 3 minutes to load.

Answer the questions below
Read above and start the virtual machine.
No answer needed

Correct Answer
Task 2
System Configuration and Advanced System Settings
Task 2
System Configuration and Advanced System Settings
System Configuration
The System Configuration utility (MSConfig) is for advanced troubleshooting, and its main purpose is to help diagnose startup issues. 

Reference the following document here for more information on the System Configuration utility. 

There are several methods to launch System Configuration. One method is from the Start Menu.



Note: You need local administrator rights to open this utility. 

The utility has five tabs across the top. Below are the names for each tab. We will briefly cover each tab in this task. 

General
Boot
Services
Startup
Tools


In the General tab, we can select what devices and services for Windows to load upon boot. The options are: Normal, Diagnostic, or Selective. 

In the Boot tab, we can define various boot options for the Operating System. 



The Services tab lists all services configured for the system regardless of their state (running or stopped). A service is a special type of application that runs in the background.  



In the Startup tab, you won't see anything interesting in the attached VM.  Below is a screenshot of the Startup tab for MSConfig from my local machine. 



As you can see, Microsoft advises using Task Manager (taskmgr) to manage (enable/disable) startup items. The System Configuration utility is NOT a startup management program. 

If you open the Task Manager for the attached VM, you will notice that it doesn't display a Startup tab. You will also not see anything in the Startup tab inside the msconfig utility, as shown above. This is because the attached machine is a Windows server, and Windows servers handle startup applications differently than Windows client systems. Unlike Windows 10 or 11, you will not see startup programs in Task Manager or in the Startup tab of msconfig. On these Windows server machines, the only reliable way to view user-level startup items is through the Startup folder itself. You can access it by pressing Win + R, which opens the Run Dialog, typing shell:startup, and then pressing Enter. This will display all startup programs as shortcuts or executables that are configured to run automatically the next time a user logs in. This is where you can verify applications that are configured to launch at startup. Below is a screenshot of the startup folder from another Windows server (not from the attached VM):



Now coming back to the msconfig. There is a list of various utilities (tools) in the Tools tab here that we can run to configure the operating system further. There is a brief description of each tool to provide some insight into what the tool is for. 



Notice the Selected command section. The information in this textbox will change per tool.

To run a tool, we can use the command to launch the tool via the run prompt, command prompt, or by clicking the Launch button. 

Advanced System Settings
Windows gives you some additional configuration settings as well, which you can use to control the performance behavior and system recovery. To access this option, you can search for View advanced system settings in your search bar and open it. This will open a System Properties panel as shown below:



Windows uses a page file as an extra virtual memory space when the physical RAM becomes full. This helps to prevent slowdowns or application crashes when the system runs out of memory. You can view or modify the page file by navigating to the Advanced option at the top and clicking Settings under the Performance tab.



So after clicking the Settings, you will get the Performance Options window, as can be seen below:



 In this Performance tab, the Advanced option can also tell you about the page file size configured for the drives. In this case, it's 1048 MB. The other settings here can give you the following information:

The drive where the page file is stored
The initial size (MB)
The maximum size
Whether Windows manages the size automatically
There is another cool configuration that you can find in the Advanced System Settings. It is known as Startup and Recovery. Windows can create a crash dump file whenever it encounters a critical error, such as a Blue Screen of Death. This crash dump helps the administrators or analysts understand what went wrong during the crash. You can view or modify the crash dump settings by navigating to the Advanced option at the top and then clicking Settings under the Startup and Recovery section.



So after clicking the settings, you will see the Startup and Recovery window, as shown below:



Here, you will find different settings for the startup and recovery. The Write debugging information dropdown tells you the type of crash dump configured for the system. Windows supports different dump types, such as:

Automatic memory dump
Kernel memory dump
Small memory dump (256 KB)
Complete memory dump
None
This setting shows how much information Windows will save in the crash dump when a system crash occurs.

Answer the questions below
What is the name of the service that lists Systems Internals as the manufacturer?
PsShutdown

Correct Answer
Whom is the Windows license registered to?

Windows User

Correct Answer
What is the command for Windows Troubleshooting?
C:\Windows\System32\control.exe /name Microsoft.Troubleshooting

Correct Answer
What command will open the Control Panel? (The answer is  the name of .exe, not the full path)

control.exe

Correct Answer
Task 3
Change UAC Settings
We're continuing with Tools that are available through the System Configuration panel.

User Account Control (UAC) was covered in great detail in Windows Fundamentals 1. 

The UAC settings can be changed or even turned off entirely (not recommended). You can move the slider to see how the setting will change the UAC settings and Microsoft's stance on the setting.

This slider has four security levels, each of which controls how Windows alerts you when apps or users try to make changes at the system level. They fall into four standard categories as explained below:

Always notify: This is the highest security. Windows notifies you whenever any apps or you yourself try to make changes, and the desktop dims (Secure Desktop).

Notify for apps: Windows notifies only when apps try to make changes, but not when you change Windows settings. This option is enabled by default.

Notify without dimming: Same as above (Notify for apps), but this time the screen does not dim. 

Never notify: Notifications are turned off. Windows won’t warn you about any changes made by you or any apps. 

You can find the current level by looking at the position of the slider in the User Account Control settings window, as shown below:



Answer the questions below
What is the command to open User Account Control Settings? (The answer is the name of the .exe file, not the full path)
UserAccountControlSettings.exe

Correct Answer
Task 4
Computer Management
We're continuing with tools that are available through the System Configuration panel.

The Computer Management (compmgmt) utility has three primary sections: System Tools, Storage, and Services and Applications.



System Tools

Let's start with Task Scheduler. Per Microsoft, with Task Scheduler, we can create and manage common tasks that our computer will carry out automatically at the times we specify.

A task can run an application, a script, etc., and tasks can be configured to run at any point. A task can run at log in or at log off. Tasks can also be configured to run on a specific schedule, for example, every five mins.

To view the scheduled tasks that are present on the system, click Task Scheduler Library. This will display all the scheduled tasks of the system. You can click on any of them to view their details. The screenshot below shows a scheduled task named SystemInfoDailyLog configured to run every day at 10:00 AM. Here, you will see the program or command that will run when the task is triggered.



It is also important to note that some scheduled tasks are not recurring and are made to run just once at a specific time. In this case, we would see something like At 2:50 PM on 6/15/2025 as the trigger.

To create a basic task, click on Create Basic Task under Actions (right pane).



Next is Event Viewer.

Event Viewer allows us to view events that have occurred on the computer. These records of events can be seen as an audit trail that can be used to understand the activity of the computer system. This information is often used to diagnose problems and investigate actions executed on the system. 



Event Viewer has three panes.
The pane on the left provides a hierarchical tree listing of the event log providers. (as shown in the image above)
The pane in the middle will display a general overview and summary of the events specific to a selected provider.
The pane on the right is the actions pane.
There are five types of events that can be logged. Below is a table from docs.microsoft.com providing a brief description for each.
 

 
The standard logs are visible under Windows Logs. Below is a table from docs.microsoft.com providing a brief description for each.
 

 
For more information about Event Viewer and Event Logs, please refer to the Windows Event Log room. 

Shared Folders is where you will see a complete list of shares and folders shared that others can connect to. 



In the above image, under Shares, are the default share of Windows, C$, and default remote administration shares created by Windows, such as ADMIN$. 

As with any object in Windows, you can right-click on a folder to view its properties, such as Permissions (who can access the shared resource). 

Under Sessions, you will see a list of users who are currently connected to the shares. In this VM, you won't see anybody connected to the shares.

All the folders and/or files that the connected users access will list under Open Files.

The Local Users and Groups section you should be familiar with from Windows Fundamentals 1 because it's lusrmgr.msc.

In Performance, you'll see a utility called Performance Monitor (perfmon).

Perfmon is used to view performance data either in real-time or from a log file. This utility is useful for troubleshooting performance issues on a computer system, whether local or remote. 



Device Manager allows us to view and configure the hardware, such as disabling any hardware attached to the computer.



Storage  

Under Storage is Windows Server Backup and Disk Management. We'll only look at Disk Management in this room.

Note: Since the virtual machine is a Windows Server operating system, there are utilities available that you will typically not see in Windows 10.  



Disk Management is a system utility in Windows that enables you to perform advanced storage tasks.  Some tasks are:

Set up a new drive
Extend a partition
Shrink a partition
Assign or change a drive letter (ex. E:) 
Services and Applications

Recall from the previous task, a service is a special type of application that runs in the background. You can see all the services and their statuses by clicking the Services button given under the Services and Applications section, as shown below:



The services shown above have their display names, status, and other values. If you want to get more information about any service, right-click on the service and click properties. Here, you will see additional details, such as the service name (which differs from the display name), the path to its executable, its startup type, and other relevant information.



There is a field known as Startup type in a service’s Properties window, as shown above. It determines how and when the service is configured to start. We can set a service to Automatic, which means it starts every time the system boots, or Manual, which means it only starts when another process or user triggers this service, or Disabled, which means it should not run at all. The service shown in the screenshot above is set to Automatic.

WMI Control configures and controls the Windows Management Instrumentation (WMI) service.

Per Wikipedia, "WMI allows scripting languages (such as VBScript or Windows PowerShell) to manage Microsoft Windows personal computers and servers, both locally and remotely. Microsoft also provides a command-line interface to WMI called Windows Management Instrumentation Command-line (WMIC)."

Note: The WMIC tool is deprecated in Windows 10, version 21H1. Windows PowerShell supersedes this tool for WMI. 

Answer the questions below
What is the command to open Computer Management?
(The answer is the name of the .msc file, not the full path)

compmgmt.msc

Correct Answer
When is the npcapwatchdog scheduled task set to run at?

At system startup

Correct Answer

What is the name of the hidden folder that is shared?

sh4r3dF0Ld3r

Correct Answer
Task 5
System Information
We're continuing with Tools that are available through the System Configuration panel.

What is the System Information (msinfo32) tool?

Per Microsoft, "Windows includes a tool called Microsoft System Information (Msinfo32.exe).  This tool gathers information about your computer and displays a comprehensive view of your hardware, system components, and software environment, which you can use to diagnose computer issues."

The  information in System Summary is divided into three sections:

Hardware Resources
Components
Software Environment
System Summary will display general technical specifications for the computer, such as processor brand and model.



The information displayed in Hardware Resources is not for the average computer user. If you want to learn more about this section, refer to the official Microsoft page.



Under Components, you can see specific information about the hardware devices installed on the computer. Some sections don't show any information, but some sections do, such as Display and Input.



In the Software Environment section, you can see information about software baked into the operating system and software you have installed. Other details are visible in this section as well, such as the Environment Variables and Network Connections. 



Recall from the Windows Fundamentals 1 room (The Windows\System32 Folder task) where Environment Variables was briefly touched on. 

Per Microsoft, "Environment variables store information about the operating system environment. This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders.

The environment variables store data that is used by the operating system and other programs. For example, the WINDIR environment variable contains the location of the Windows installation directory. Programs can query the value of this variable to determine where Windows operating system files are located".

Click on Environment Variables to see the assigned values for the virtual machine.



Another method to view environment variables is Control Panel > System and Security > System > Advanced system settings > Environment Variables OR Settings > System > About > system info > Advanced system settings > Environment Variables.



The detour is over. Let's redirect our attention back to msinfo32 and pick up where we left off.

Towards the very bottom of this utility, there is a search bar. Please give it a go. Select Components and search for IP address.



Answer the questions below
What is the command to open System Information? (The answer is the name of the .exe file, not the full path)
msinfo32.exe

Correct Answer
What is listed under System Name?

THM-WINFUN2

Correct Answer
Under Environment Variables, what is the value for ComSpec?
%SystemRoot%\system32\cmd.exe

Correct Answer
Task 6
Resource Monitor
Task 6
Resource Monitor
We're continuing with Tools that are available through the System Configuration panel.

What is Resource Monitor (resmon)?

Per Microsoft, "Resource Monitor displays per-process and aggregate CPU, memory, disk, and network usage information, in addition to providing details about which processes are using individual file handles and modules. Advanced filtering allows users to isolate the data related to one or more processes (either applications or services), start, stop, pause, and resume services, and close unresponsive applications from the user interface. It also includes a process analysis feature that can help identify deadlocked processes and file locking conflicts so that the user can attempt to resolve the conflict instead of closing an application and potentially losing data."

As some of the other tools mentioned in this room, this utility is geared primarily to advanced users who need to perform advanced troubleshooting on the computer system.

In the Overview tab, Resmon has four sections:

CPU
Disk
Network
Memory


The same four sections have corresponding tabs across the top. See below.



Note that each tab has additional information for each. An image is shown below for each tab. 

CPU



Memory



Disk



Network



Although not captured in any of the images above, Resource Monitor has a pane at the far right. This pane shows a graphical view in real-time for each section. 

Note: The information displayed in Resource Monitor will be different for you compared to the images above.

Answer the questions below
What is the command to open Resource Monitor? (The answer is the name of the .exe file, not the full path)
resmon.exe

Correct Answer
Task 7
Command Prompt
We're continuing with Tools that are available through the System Configuration panel.

The command prompt (cmd) can seem daunting at first, but it's really not that bad once you understand how to interact with it. 

In early operating systems, the command line was the sole way to interact with the operating system.

When the GUI (graphical user interface) was introduced, it allowed users to perform complex tasks with a few clicks of a button instead of entering commands in the command prompt. 

Even though the GUI is the primary way to interact with the operating system, a computer user can still interact via the command prompt. 

In this task, we'll only cover a few commands that a computer user can run in the command prompt to obtain information about the computer system.

Let's start with a few simple commands, such as hostname and whoami.

The command hostname will output the computer name.



The command whoami will output the name of the logged-in user.



Next, let's look at some commands that are useful when troubleshooting.

A command used often is ipconfig. This command will show the network address settings for the computer.



Each command will have a help manual to explain the expected syntax to execute the command properly, along with any additional parameters that can be added to the command to expand its execution.

A  command to retrieve the help manual for a command is /?.

For example, to see the help manual for ipconfig, you can use the following command: ipconfig /?



Note: To clear the command prompt screen, the command is cls. 

The next command is netstat. Per the help manual, this command will display protocol statistics and current TCP/IP network connections. 



In the above image, the line within the red box shows us an example syntax for the command. 

The structure tells us the netstat command can be run alone or with parameters, such as -a,  -b,  -e, etc. 

When any of the parameters are appended to the root command, netstat in this case, the output changes. Play with a few to see for yourself. 

The net command is primarily used to manage network resources. This command supports sub-commands.

If you type net without a sub-command, the output will show the syntax for the root command showing a few of the sub-commands you can use.



For the net command, to display the help manual /? will not work. In this case, you need to use different syntax, which is net help.



So, if you wish to see the help information for net user , the command is net help user. 



You can use the same command to view the help information for other useful net sub-commands, such as localgroup, use, share, and session. 

Refer to the following link to see a comprehensive list of commands you can execute in the command prompt here. 

Answer the questions below
In System Configuration, what is the full command for Internet Protocol Configuration?
C:\Windows\System32\cmd.exe /k %windir%\system32\ipconfig.exe

Correct Answer
For the ipconfig command, how do you show detailed information?

ipconfig /all

Correct Answer
Task 8
Registry Editor
We're continuing with Tools that are available through the System Configuration panel.

The Windows Registry (per Microsoft) is a central hierarchical database used to store information necessary to configure the system for one or more users, applications, and hardware devices.

The registry contains information that Windows continually references during operation, such as:

Profiles for each user
Applications installed on the computer and the types of documents that each can create
Property sheet settings for folders and application icons
What hardware exists on the system
The ports that are being used.
Warning: The registry is for advanced computer users. Making changes to the registry can affect normal computer operations. 

There are various ways to view/edit the registry. One way is to use the Registry Editor (regedit).



Refer to the following Microsoft documentation here to learn more about the Windows Registry. 

Answer the questions below
What is the command to open the Registry Editor? (The answer is the name of  the .exe file, not the full path)
regedt32.exe

Correct Answer

Task 9
Conclusion
Recall that the tasks covered in this room were some of the tools that can launch from MSConfig. 

Throughout the room, commands and shortcuts were shared for the utilities. This means you don't have to launch MSConfig to run these utilities. 

You can also run some of these utilities directly from the Start Menu. See below where some of these utilities can be found.



Some of the tools listed in MSConfig that weren't mentioned in this room were either covered in Windows Fundamentals 1 or were left for you to explore on your own. 
Task 1
Recon
Press the Start Machine button below.


Start Machine
Start the AttackBox by pressing the Start AttackBox button at the top of this page. The AttackBox machine will start in Split-Screen view. If it is not visible, use the blue Show Split View button at the top of the page.

Scan and learn what exploit this machine is vulnerable to. Please note that this machine does not respond to ping (ICMP) and may take a few minutes to boot up. This room is not meant to be a boot2root CTF, rather, this is an educational series for complete beginners. Professionals will likely get very little out of this room beyond basic practice as the process here is meant to be beginner-focused. 





Art by one of our members, Varg - THM Profile - Instagram - Blue Merch - Twitter



Link to Ice, the sequel to Blue: Link

You can check out the third box in this series, Blaster, here: Link

-----------------------------------------



The virtual machine used in this room (Blue) can be downloaded for offline usage from https://darkstar7471.com/resources.html



Enjoy the room! For future rooms and write-ups, follow @darkstar7471 on Twitter.

Answer the questions below
Scan the machine. (If you are unsure how to tackle this, I recommend checking out the Nmap room)

No answer needed

Correct Answer

How many ports are open with a port number under 1000?

3

Correct Answer

What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)

ms17-010

Correct Answer

Task 2
Gain Access
Exploit the machine and gain a foothold.

Answer the questions below
Start Metasploit

No answer needed

Correct Answer

Find the exploitation code we will run against the machine. What is the full path of the code? (Ex: exploit/........)

exploit/windows/smb/ms17_010_eternalblue

Correct Answer

Show options and set the one required value. What is the name of this value? (All caps for submission)

RHOSTS

Correct Answer

Usually it would be fine to run this exploit as is; however, for the sake of learning, you should do one more thing before exploiting the target. Enter the following command and press enter:

set payload windows/x64/shell/reverse_tcp

With that done, run the exploit!

No answer needed

Correct Answer

Confirm that the exploit has run correctly. You may have to press enter for the DOS shell to appear. Background this shell (CTRL + Z). If this failed, you may have to reboot the target VM. Try running it again before a reboot of the target. 

No answer needed

Correct Answer
Task 3
Escalate
Escalate privileges, learn how to upgrade shells in metasploit.

Answer the questions below
If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected) 

post/multi/manage/shell_to_meterpreter

Correct Answer

Select this (use MODULE_PATH). Show options, what option are we required to change?

SESSION

Correct Answer
Set the required option, you may need to list all of the sessions to find your target here. 

No answer needed

Correct Answer

Run! If this doesn't work, try completing the exploit from the previous task once more.

No answer needed

Correct Answer

Once the meterpreter shell conversion completes, select that session for use.

No answer needed

Correct Answer

Verify that we have escalated to NT AUTHORITY\SYSTEM. Run getsystem to confirm this. Feel free to open a dos shell via the command 'shell' and run 'whoami'. This should return that we are indeed system. Background this shell afterwards and select our meterpreter session for usage again. 

No answer needed

Correct Answer
List all of the processes running via the 'ps' command. Just because we are system doesn't mean our process is. Find a process towards the bottom of this list that is running at NT AUTHORITY\SYSTEM and write down the process id (far left column).

No answer needed

Correct Answer
Migrate to this process using the 'migrate PROCESS_ID' command where the process id is the one you just wrote down in the previous step. This may take several attempts, migrating processes is not very stable. If this fails, you may need to re-run the conversion process or reboot the machine and start once again. If this happens, try a different process next time. 

No answer needed

Correct Answer
Task 4
Cracking
Task 4
Cracking
Dump the non-default user's password and crack it!

Answer the questions below
Within our elevated meterpreter shell, run the command 'hashdump'. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user? 

Jon

Correct Answer
Copy this password hash to a file and research how to crack it. What is the cracked password?

alqfna22

Correct Answer

Task 5
Find flags!
Task 5
Find flags!
Find the three flags planted on this machine. These are not traditional flags, rather, they're meant to represent key locations within the Windows system. Use the hints provided below to complete this room!



-----------------------------------------------------------------



Completed Blue? Check out Ice: Link

You can check out the third box in this series, Blaster, here: Link

Answer the questions below
Flag1? This flag can be found at the system root. 
flag{access_the_machine}

Correct Answer

Flag2? This flag can be found at the location where passwords are stored within Windows.



*Errata: Windows really doesn't like the location of this flag and can occasionally delete it. It may be necessary in some cases to terminate/restart the machine and rerun the exploit to find this flag. This relatively rare, however, it can happen. 

flag{sam_database_elevated_access}

Correct Answer

flag3? This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved. 

flag{admin_documents_can_be_valuable}

Correct Answer


