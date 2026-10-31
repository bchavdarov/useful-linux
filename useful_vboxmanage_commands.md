Category,Command,Description,Example Usage
VM Management,list vms,Lists all registered virtual machines,VBoxManage list vms
VM Management,list runningvms,Lists currently running virtual machines,VBoxManage list runningvms
VM Management,showvminfo,Displays detailed information about a specific VM,VBoxManage showvminfo "Ubuntu_Server"
VM Management,createvm,Creates a new virtual machine XML definition file,VBoxManage createvm --name "TestVM" --ostype "Ubuntu_64" --register
VM Management,registervm,Registers an existing VM definition file (.vbox),VBoxManage registervm "/path/to/vm.vbox"
VM Management,unregistervm,Unregisters a VM (optionally deletes its files),VBoxManage unregistervm "TestVM" --delete
VM Power State,startvm,Starts a virtual machine (gui|headless|mfe),VBoxManage startvm "Ubuntu_Server" --type headless
VM Power State,controlvm pause,Pauses execution of a running VM,VBoxManage controlvm "Ubuntu_Server" pause
VM Power State,controlvm resume,Resumes a paused VM,VBoxManage controlvm "Ubuntu_Server" resume
VM Power State,controlvm savestate,Saves current VM state and closes it,VBoxManage controlvm "Ubuntu_Server" savestate
VM Power State,controlvm acpipowerbutton,Sends ACPI shutdown signal to guest OS,VBoxManage controlvm "Ubuntu_Server" acpipowerbutton
VM Power State,controlvm poweroff,Forcibly powers off a VM (like pulling the plug),VBoxManage controlvm "Ubuntu_Server" poweroff
VM Configuration,modifyvm --memory,Configures RAM allocation (in MB),VBoxManage modifyvm "TestVM" --memory 4096
VM Configuration,modifyvm --cpus,Sets the number of virtual CPUs,VBoxManage modifyvm "TestVM" --cpus 2
VM Configuration,modifyvm --boot1,Sets primary boot device (floppy|dvd|disk|net),VBoxManage modifyvm "TestVM" --boot1 dvd
VM Configuration,modifyvm --vram,Configures video RAM allocation (in MB),VBoxManage modifyvm "TestVM" --vram 128
Disk Management,createmedium,Creates a new virtual hard disk image,VBoxManage createmedium disk --filename "/path/disk.vdi" --size 20480
Disk Management,modimedium --resize,Resizes an existing virtual disk (in MB),VBoxManage modifymedium disk "/path/disk.vdi" --resize 40960
Disk Management,showmediuminfo,Displays details about a disk image,VBoxManage showmediuminfo "/path/disk.vdi"
Disk Management,clonemedium,Clones virtual disk to another format (VDI/VMDK/VHD),VBoxManage clonemedium disk input.vdi output.vmdk --format VMDK
Storage Controllers,storageattach,Attaches a disk image or ISO to a VM controller,VBoxManage storageattach "TestVM" --storagectl "SATA" --port 0 --device 0 --type hdd --medium "/path/disk.vdi"
Storage Controllers,storageattach (ISO),Mounts an ISO image into virtual DVD drive,VBoxManage storageattach "TestVM" --storagectl "IDE" --port 0 --device 0 --type dvddrive --medium "/path/ubuntu.iso"
Networking,modifyvm --nic,Sets network mode (none|null|nat|bridged|intnet|hostonly),VBoxManage modifyvm "TestVM" --nic1 bridged --bridgeadapter1 "eth0"
Networking,modifyvm --natpf,Adds a Port Forwarding rule for NAT networking,VBoxManage modifyvm "TestVM" --natpf1 "guestssh,tcp,,2222,,22"
Networking,list hostonlyifs,Lists host-only network interfaces on the host system,VBoxManage list hostonlyifs
Snapshots,snapshot take,Creates a snapshot of current VM state,VBoxManage snapshot "TestVM" take "CleanInstall_Snap"
Snapshots,snapshot restore,Restores VM to a specific snapshot,VBoxManage snapshot "TestVM" restore "CleanInstall_Snap"
Snapshots,snapshot list,Lists all snapshots associated with a VM,VBoxManage snapshot "TestVM" list
Snapshots,snapshot delete,Deletes a specific snapshot,VBoxManage snapshot "TestVM" delete "CleanInstall_Snap"
Host & Environment,list hostinfo,Displays detailed system information of host machine,VBoxManage list hostinfo
Host & Environment,list dhcpservers,Lists all active VirtualBox internal DHCP servers,VBoxManage list dhcpservers
Guest Control,guestcontrol run,Executes a command inside the running guest OS,VBoxManage guestcontrol "TestVM" run --username user --password pass -- /usr/bin/ls
Guest Control,guestcontrol copyto,Copies a file from host to guest OS,VBoxManage guestcontrol "TestVM" copyto "/host/file.txt" "/guest/file.txt" --username user --password pass