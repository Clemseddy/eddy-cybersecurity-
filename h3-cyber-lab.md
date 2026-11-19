# H3 - Cyber lab

This is assignment 3 for the course which is a lab exercise. Actual test is to install Linux Debian 13 Trixie into virtual machine and test some commands and tools, especially Hashcat for cracking passwords.

## Part 1 - Read and summarize

below are summarized articles about topics.

### Heinonen 2026: How to Install Linux to Virtualbox?

* Hardware & VirtualBox Setup: Before setting up VirtualBox on a Windows machine, I need to make sure VT-x (virtualization technology) is enabled in my computer's BIOS/UEFI settings so the virtual machine runs smoothly

* Getting the Operating System: The guide uses the Debian 13 (Trixie) Live Xfce ISO image, which is a single file containing a complete copy of the operating system that I can download and boot

* Configuring the Virtual Machine: When creating the VM in VirtualBox, I set the type to Linux/Debian 64-bit, assign 4 GB of RAM, select 2 CPU cores, give it 20–40 GB of disk space, enable EFI, and make sure to skip unattended installation

* Testing Live & Real Installation: I can test Debian in a Live session first to check my internet and keyboard, then run the Calamares installer to erase the virtual disk, set up my user account, and run sudo apt-get update && sudo apt-get upgrade after restarting

* My Idea / Question: Why is running a Live session recommended before doing a full installation, and how can taking virtual machine snapshots help save my work if a system update goes wrong later?

### Karvinen 2020: Command Line Basics Revisited

* File System Layout: Linux stores everything under a single root directory (/) instead of using drive letters, where my personal user files live in /home/username/ and main system settings are saved as plain text files in /etc/

* Basic Navigation & File Control: I can move around and manage files using simple commands like pwd to see my current folder, ls to view files, cd to change folders, mkdir to create folders, cp to copy, mv to move/rename, and rm to permanently delete files without a trash bin

* Time-Saving Shortcuts: To work faster and avoid typos, I can press the Tab key to auto-complete filenames, use less or pipe output (|) to read long text page-by-page, and press the Up arrow or Ctrl+R to search my command history

* Admin Privileges & Software Packages: Following the least privilege rule, I only use sudo for administrative commands like refreshing package lists (sudo apt-get update) and installing or removing software packages with apt-get

* My Idea / Question: Since the rm command deletes files immediately without sending them to a trash bin, would setting up a safer alias command be a good safety net for beginners?

### Karvinen 2022: Cracking Passwords with Hashcat

* How Password Hashes Work: Systems don't store passwords as readable text; they convert them into one-way scrambled codes called hashes (like MD5), which cannot be directly reversed back into the original word

* Identifying Hashes & Wordlists: To crack a hash, I use hashid to figure out the hash format (like Mode 0 for MD5) and download a large dictionary of real-world leaked passwords like rockyou.txt

* Running Hashcat: I run Hashcat from the command line by giving it the hash type, the target hash, and the dictionary file (e.g., hashcat -m 0 'hash' rockyou.txt -o solved), which tests millions of dictionary words per second until it finds a match

* Boosting Speed with GPUs: Password cracking runs significantly faster when executed directly on the host computer's graphics hardware (GPU) using graphics drivers rather than running inside a virtual machine

* My Idea / Question: Given how fast hashcat can test millions of dictionary words per second, how much safer could it be for a long 16-character passphrase compared to a simple 8-character password against dictionary attacks?

## Part 2 - Linux. Install Linux on a virtual machine. Use Debian 13-Trixie

being guided by the instruction on Heinonen 2026: How to Install Linux to VirtualBox?, i performed this test as summarized below

1.  Overview and System Environment

For this coursework assignment, I installed Debian 13 (Trixie) Linux as a virtual machine to set up my environment for upcoming cybersecurity tasks. I performed the entire setup locally on my personal Acer Aspire laptop running the Windows operating system.

My objective was to establish a fully functional, isolated Linux environment using Oracle VirtualBox while keeping my host operating system completely separate. Below is the step-by-step account of how I configured VirtualBox, downloaded the installation media, provisioned the virtual machine, and completed the Debian installation.

2. VirtualBox Installation and Directory Configuration

I started by setting up the Oracle VirtualBox hypervisor on my host laptop to manage my virtual machines.

1. I downloaded the Oracle VirtualBox installer for Windows hosts and ran the setup executable as an administrator, accepting the User Account Control (UAC) prompt.
2. I completed the standard VirtualBox setup wizard.
3. To keep my virtual machine files organized, I configured a dedicated workspace folder in VirtualBox Manager:
  * I manually created a new folder named VirtualBox VM on my local drive.
  * I opened the VirtualBox Manager settings and selected VirtualBox VM as my default machine folder.
  * I confirmed the remaining settings and saved the preferences.

3. Downloading the Debian 13 (Trixie) Installation Image

Next, I obtained the official Debian installation file to use as the boot media for my virtual machine.

1. I opened my web browser and navigated to the official Debian site at debian.org.
2. I located the installation image by following this path: Other Downloads > Complete Installation Image > 64-bit PC DVD ISO (AMD64).
3. I downloaded the Debian 13 (Trixie) AMD64 ISO image to my laptop's local storage.

4. Virtual Machine Creation and Configuration

With the installer file ready, I opened VirtualBox Manager to create and configure virtual hardware for my Linux environment.

1. I clicked New in VirtualBox Manager to start the virtual machine setup wizard.
2. I assigned the name Test Debian to my new virtual machine.
3. I configured the virtual machine settings:
  * ISO Selection: Attached the downloaded Debian 13 (Trixie) ISO image.
  * Operating System Type: Set the OS type to Linux with the Debian (64-bit) subtype.
  * User Credentials: Entered my user account name and selected a 6-digit PIN for my password, which makes executing sudo administrative commands quicker during CLI tasks.
  * Network Domain Name: Specified .home as my local domain name.
  * Keyboard Layout: Selected the Finnish layout to match the physical keyboard on my Acer Aspire laptop.
  * System Firmware: Enabled EFI (Unified Extensible Firmware Interface) for modern boot support.
  * Network Access: Left internet access enabled so the system could download packages and updates.
4. I reviewed the settings and completed the creation wizard to assemble the Test Debian VM.

5. Graphical Operating System Installation and First Boot

After provisioning the virtual hardware, I launched the virtual machine to run the Debian installer.

<img width="1524" height="1388" alt="WhatsApp Image 2026-11-19 at 04 02 35" src="https://github.com/user-attachments/assets/74e85f95-bb35-4bcf-a30b-b41f7bae0277" />

1. I started the Test Debian virtual machine from VirtualBox Manager.
2. The VM booted from the attached ISO, and I selected the graphical installation option.
3. I stepped through the installer prompts:
  * Interface Language: Selected English as the system language.
  * Location: Set my location to Europe > Finland.
  * Keyboard Layout: Selected the Finnish keyboard layout to ensure correct character mapping.
  * Storage Allocation: Chose to erase the virtual disk, allowing the installer to format the blank virtual drive automatically.
4. I confirmed my configuration choices and started the installation.
5. Once the installation completed, I rebooted the virtual machine when prompted.
6. The VM booted into the Debian desktop environment, and I logged into my account using my username and 6-digit PIN.

<img width="1594" height="1448" alt="WhatsApp Image 2026-11-19 at 04 04 10" src="https://github.com/user-attachments/assets/80193158-ff04-45db-bb7d-55f049b05f81" />

6. Post-Installation Verification and Terminal Setup

After logging in, I verified that the system was working properly and noted key operational details for lab work.

1. I opened the application menu ("Show Apps") and launched the Terminal.
2. I confirmed that the terminal opened to a black screen with a blinking cursor, ready for entering Linux commands.

<img width="1600" height="1147" alt="WhatsApp Image 2026-11-19 at 04 04 22" src="https://github.com/user-attachments/assets/2700a79a-4f12-47a3-a015-12c4ed30bca6" />

4. I noted the following key operational conditions of my setup:
  * Host-Guest Isolation: The Debian virtual environment and its filesystem remain completely separate from my Windows host OS.
  * Clipboard Isolation: Shared copy-paste between my Windows host and the VM is disabled by default for security.
  * Resource Usage: While VirtualBox Manager allows running multiple virtual machines simultaneously, I need to manage active VMs to preserve system resources on my laptop.

some of the challenges faced and errors and how i resolved them are:

- **Finding the Debian download:** The first links were confusing and did not appear to start a download. Then i returned to debian.org and selected **Other Downloads → Complete Installation Image → 64-bit PC DVD ISO**; the download then started.
- **Choosing the keyboard layout:** Finnish was not immediately clear in the installer. Then i checked the laptop’s physical keyboard, then selected the Finnish keyboard layout on the next phase
- **Understanding the virtualization tip:** The H3 VTX/BIOS tip caused confusion. then i later realized it was an optional speed improvement, not completely necessary for the installation if it worked well.
- **Getting started with hash cracking:** The task felt unclear because Linux was new. then i was practicing with *Command Line Basics Revisited* first, then following the H3 step-by-step hash-cracking guide in the Debian terminal. The hash-cracking task was not completed during the first trial session.

## Part 3 - Crack. Crack the hash 6b1628b016dff46e6fa35684be6acc96

I continued further by following the instructions and guide in the *Karvinen 2022: Cracking Passwords with Hashcat*. 

A. **Overview and Environment Setup**

I performed a practical password cracking test inside my Debian 13 (Trixie) virtual machine running on VirtualBox. The objective of this lab exercise was to identify the hash algorithm and recover the plaintext password for the target hash 6b1628b016dff46e6fa35684be6acc96 following the procedure described in Tero Karvinen's 2022 guide.

System and Virtual Hardware Configuration

* Host Hardware: Acer Aspire laptop equipped with an Intel Core i7-10510U CPU (@ 1.80GHz).
* Virtual Machine Setup: Debian 13 (Trixie) 64-bit guest operating system in Oracle VirtualBox, verified with active VirtualBox Guest Additions modules (vboxguest, vboxsf, vboxvideo).
* Target Hash: 6b1628b016dff46e6fa35684be6acc96
* Software Tools Used: hashid (v3.1.4), hashcat (v6.2.6 utilizing CPU OpenCL via PoCL), wget, tar, and the RockYou dictionary.

B. **Step-by-Step Test Execution and Troubleshooting**

The following numbered log details every step I took during the test, including the specific terminal errors I encountered, why they occurred, and how I resolved them.

Step 1: Updating Package Lists and Installing Tools

1. I opened the Linux terminal in my VM and updated the local package index:
  * Command executed: sudo apt-get update
  * Error Encountered: E: The repository 'cdrom:// Debian GNU/Linux 13.7.0 _Trixie_ Release' does not have a Release file.
  * Root Cause & Resolution: The APT package manager attempted to read the installation ISO image mounted in the virtual CD-ROM drive. Since the online Debian repositories (deb.debian.org and security.debian.org) were reachable and updated successfully, I safely ignored the CD-ROM repository warning.
2. I installed the required utilities (hashid, hashcat, and wget):
  * Error Encountered: When pasting the command into the terminal, terminal bracketed paste mode introduced escape characters (^[[200~sudo apt-get -y install hashid hashcat wget), resulting in bash: $'\E[200~sudo': command not found.
  * Resolution: I manually re-typed the command sudo apt-get -y install hashid hashcat wget cleanly without copy-paste artifacts. The system confirmed all three tools were installed and up to date.

<img width="1600" height="1094" alt="WhatsApp Image 2026-11-19 at 04 40 57" src="https://github.com/user-attachments/assets/22c8692a-eed8-46e5-9160-f8a4ea0f6221" />

Step 2: Workspace Setup and Wordlist Preparation

1. I created and entered a clean working folder:
  * Commands executed: mkdir hashed followed by cd hashed.
2. I downloaded the compressed RockYou password list using wget:
  * Command executed: wget with the target download URL for rockyou.txt.tar.gz from the SecLists repository.
  * The 50.82 MB file downloaded successfully in 2.1 seconds at a rate of 24.1 MB/s.
3. I extracted the wordlist archive and removed the temporary tarball:
  * Commands executed: tar xf rockyou.txt.tar.gz and rm rockyou.txt.tar.gz.
4. I inspected the wordlist to confirm its contents and line count:
  * Commands executed: head rockyou.txt and wc -l rockyou.txt.
  * The file was verified to contain 14,344,391 dictionary password entries.

Step 3: Identifying the Target Hash Type

1. Before running the password cracker, I used hashid to identify the hash type:
  * Command executed: hashid -m 6b1628b016dff46e6fa35684be6acc96
2. Analysis output returned multiple candidate types:
  * [+] MD5 [Hashcat Mode: 0]
  * [+] MD4 [Hashcat Mode: 900]
  * [+] NTLM [Hashcat Mode: 1000]
3. Selected Mode: Based on standard cryptographic usage and hashid recommendations, I selected MD5 (Hashcat Mode 0) for the attack.

Step 4: Running Hashcat and Troubleshooting Stdin Timeouts

1. I attempted my first cracking run against the target hash:
  * Command executed: hashcat -m 0 '6b1628b016dff46e6fa35684be6acc96'
  * Error Encountered: Hashcat initialized in standard input mode (Starting attack in stdin mode). It sat at 0 H/s speed for over two minutes, repeatedly logging: ATTENTION! Read timeout in stdin mode. Password candidates input is too slow. It eventually aborted with No password candidates received in stdin mode, aborting.
  * Root Cause: I forgot to supply the path to the dictionary file (rockyou.txt) and output options. When Hashcat receives a hash without a wordlist file parameter, it expects candidates to be piped into standard input (stdin).
  
  <img width="1406" height="927" alt="WhatsApp Image 2026-11-19 at 04 41 48" src="https://github.com/user-attachments/assets/f5ac74a7-8361-417f-a807-6b2c435bd00e" />

  * Resolution: I corrected the command structure by explicitly specifying the dictionary file (rockyou.txt) and an output file (-o solved):
    * Corrected command: hashcat -m 0 '6b1628b016dff46e6fa35684be6acc96' rockyou.txt -o solved

Step 5: Successful Password Recovery and Verification

1. I executed the corrected command. Hashcat built the dictionary cache (14,344,384 keyspace entries) in 1 second and cracked the hash almost instantly:
  * Status: Cracked
  * Speed: 4,143 H/s on CPU
  * Progress: 512 / 14,344,384 candidate entries tested before finding a match.
2. I inspected the output file to view the recovered password:
  * Command executed: cat solved
  * Result: 6b1628b016dff46e6fa35684be6acc96:summer
3. I verified Hashcat's potfile caching mechanism by running the command without the output flag:
  * Command executed: hashcat -m 0 6b1628b016dff46e6fa35684be6acc96 rockyou.txt
  * Output notice: INFO: All hashes found in potfile! Use --show to display them.
4. I retrieved the cracked password directly from the potfile:
  * Command executed: hashcat -m 0 6b1628b016dff46e6fa35684be6acc96 rockyou.txt --show
  * Output confirmed: 6b1628b016dff46e6fa35684be6acc96:summer

<img width="1368" height="1024" alt="WhatsApp Image 2026-11-19 at 04 43 57" src="https://github.com/user-attachments/assets/f42a2453-62d6-46a7-835f-cff8a22ebed9" />

 C. **Summary of Results and Key Lessons**

* Target Hash: 6b1628b016dff46e6fa35684be6acc96
* Algorithm Identified: MD5 (Mode 0)
* Recovered Plaintext Password: summer
* Dictionary Used: rockyou.txt (14,344,391 words)
* Key Lessons Learned:
  * Command Syntax: Omitting the dictionary file argument in Hashcat forces it into stdin mode, causing the process to hang and time out. Always pass hashcat -m <mode> '<hash>' <wordlist> -o <output_file>.
  * Terminal Paste Artifacts: Copy-pasting shell commands into a VirtualBox terminal can introduce hidden control strings (such as ^[[200~). Re-typing the command manually ensures clean execution.
  * Potfile Caching: Once Hashcat successfully cracks a hash, it stores the hash and plaintext pair in a local potfile (~/.local/share/hashcat/hashcat.potfile). Subsequent runs will complete immediately, and the result can be displayed anytime using --show.

_Error message i was getting :  Not enough allocatable device memory for this attack._  
Solution: I had to ask co-pilot how to fix this and got the recommendation below which now solved the issue.
1.Shut down the Debian VM completely.
2.Open Oracle VM VirtualBox Manager.
3.Select the Debian VM.
4.Click Settings → System → Motherboard.
5.Increase Base Memory:
 •Minimum: 4096 MB (4 GB)
 •i increased to: 6194 MB 
6.Go to Display.
7.Increase Video Memory to the maximum available (i increased it to 128 MB).
8.Enable 3D Acceleration.
9.Click OK and start the VM.

Overall this is an interesting task.

## References:

Heinonen, J. (2026). How to Install Linux to Virtualbox? GitHub Repository: johanna-test-repo/module_1.md. https://github.com/johannaheinonen/johanna-test-repo/blob/main/module_1.md

Karvinen, T. (2020). Command Line Basics Revisited. TeroKarvinen.com. https://terokarvinen.com/2020/command-line-basics-revisited/

Karvinen, T. (2022). Cracking Passwords with Hashcat. TeroKarvinen.com. https://terokarvinen.com/2022/cracking-passwords-with-hashcat/
