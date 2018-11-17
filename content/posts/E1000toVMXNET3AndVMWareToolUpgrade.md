+++
title = "Upgrading VMWare Tools and Network adapter from E1000 to VMXNET3"
date = 2018-10-31T00:52:17+05:30
tags = [""]
categories = [""]
draft = false
+++

### VMware tools installation:

1. You can install VMWare tools manually or automatically. Sometimes you don't have any choice except to install manually.

2. Automatic Installation: 
    * Right click on the VM -> Guest -> Install/Upgrade VMWare tools
    *  Choose Automatic Tools Upgrade and click on OK.
    * Installation will take some time, you can see it's status in Tasks shown at the bottom of the window.

3. Manual Installation:
     * Right click on the VM -> Guest -> Install/Upgrade VMWare tools
     * Choose Interactive Tools Upgrade and click on OK.
     * Now log into VM and run the following commands.
        * mount /dev/cdrom /mnt/cdrom  ; ls /mnt/cdrom 
        * cp /mnt/cdrom/VMwareTools-****.tar.gz /tmp/
        * cd /tmp ; tar -zxvf VMwareTools-****.tar.gz
        * cd vmware-tools-distrib
   		* ./vmware-install.pl
    	* Complete the screen prompts to install the VMware Tools. Options in square brackets are default choices and can be selected by pressing Enter.
   		* umount /mnt/cdrom
    * Sometimes OS is unable to unmount the /dev/cdrom. In this case, you may need to manually end the VMware Tools installation. 
    * To end the VMware Tools install, click VM in the virtual machine menu, then click Guest > End VMware Tools Install.

#### Known Issues:

1. eth2 and eth3 adapters are added in 70-persistent-net.rules file.
Ans. This problem occurs when either "MAC is bounded to ifcfg-eth0 and ifcfg-eth1 files" or "there exists an old 70-persistent-net.rules file". 
     To resolve this issue, either "comment the line which has HWADDRADDR in ifcfg-eth0 and ifcfg-eth1 files" or 
     "Take a backup and remove the old 70-persistent-net.rules file and reboot the VM" depending on your case. 

2. VMs are not pingable or reachable.
Ans. First reboot the VM. If this does not solve the problem then try the resetting the VM.
If still, you have issues check /etc/udev/rules.d/70-persistent-net.rules, ifcfg-eth0 and ifcfg-eth1 files

3. VMWare tools status is showing as "Not running" while VMware tools version is shown as "current".
Ans. Type "vmware" on command prompt and press tab. You will be see multiple options.
     Run the option "vmware-config-tools.pl". It will try to reconfigure the VMWare tools. Press Enter to choose default options. After installation try reboot and resetting the VM.

### Steps for upgrading E1000 to VMXNET3:

1. First update the VMWare tools to latest version either manually or automatically.

2. Log in to OS here CentOS 6.6

3. Now go to VM Settings -> edit settings

4. From here, remove both E1000 adapters and add two VMXNET3 adapters for Northbound and Southbound.

5. After doing this, VM will automatically reconfigure itself and /etc/udev/rules.d/70-persistent-net.rules 
   will be modified with two new adapters.

6. Take a backup and remove this modified /etc/udev/rules.d/70-persistent-net.rules file

7. reboot the OS.

8. Voila! you did it. Now everything should work fine.

9. If VM is not pingable after this, try resetting the VM.
