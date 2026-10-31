# VBoxManage Cheat Sheet

A quick reference of useful `VBoxManage` commands for managing VirtualBox from the command line.

> **Tips**
> - On Windows, `VBoxManage.exe` lives in `C:\Program Files\Oracle\VirtualBox\` (add it to `PATH`).
> - VMs can be referenced by **name** (in quotes if it has spaces) or by **UUID**.
> - Most `modifyvm` changes require the VM to be **powered off**; use `controlvm` for a running VM.
> - Run `VBoxManage <command> --help` (or `VBoxManage help <command>`) for full options.

## Commands

| Category | Command | Description | Example Usage |
|---|---|---|---|
| General | `--version` | Show the installed VirtualBox version | `VBoxManage --version` |
| General | `help` | Show help for all or a specific command | `VBoxManage help modifyvm` |
| Information | `list vms` | List all registered VMs | `VBoxManage list vms` |
| Information | `list runningvms` | List only running VMs | `VBoxManage list runningvms` |
| Information | `list ostypes` | List supported guest OS type IDs (for `--ostype`) | `VBoxManage list ostypes` |
| Information | `list hdds` | List registered virtual hard disks | `VBoxManage list hdds` |
| Information | `list hostonlyifs` | List host-only network interfaces | `VBoxManage list hostonlyifs` |
| Information | `list natnets` | List NAT networks | `VBoxManage list natnets` |
| Information | `list bridgedifs` | List host interfaces available for bridged networking | `VBoxManage list bridgedifs` |
| Information | `list extpacks` | List installed extension packs | `VBoxManage list extpacks` |
| Information | `list systemproperties` | Show global settings (default machine folder, limits, etc.) | `VBoxManage list systemproperties` |
| Information | `showvminfo` | Show detailed configuration of a VM | `VBoxManage showvminfo "Debian12"` |
| Information | `showvminfo --machinereadable` | VM info in key=value form, handy for scripts | `VBoxManage showvminfo "Debian12" --machinereadable` |
| VM Lifecycle | `createvm` | Create and register a new VM | `VBoxManage createvm --name "Debian12" --ostype Debian_64 --register` |
| VM Lifecycle | `registervm` | Register an existing `.vbox` file | `VBoxManage registervm "/home/user/VirtualBox VMs/Debian12/Debian12.vbox"` |
| VM Lifecycle | `unregistervm` | Unregister a VM (keeps files) | `VBoxManage unregistervm "Debian12"` |
| VM Lifecycle | `unregistervm --delete` | Unregister and delete the VM and its disks | `VBoxManage unregistervm "Debian12" --delete` |
| VM Lifecycle | `clonevm` | Clone a VM | `VBoxManage clonevm "Debian12" --name "Debian12-clone" --register` |
| VM Lifecycle | `clonevm --options link` | Create a linked clone from a snapshot (saves disk space) | `VBoxManage clonevm "Debian12" --snapshot "base" --options link --name "Debian12-linked" --register` |
| Configuration | `modifyvm --memory` | Set RAM in MB | `VBoxManage modifyvm "Debian12" --memory 4096` |
| Configuration | `modifyvm --cpus` | Set number of virtual CPUs | `VBoxManage modifyvm "Debian12" --cpus 4` |
| Configuration | `modifyvm --vram` | Set video memory in MB | `VBoxManage modifyvm "Debian12" --vram 128` |
| Configuration | `modifyvm --graphicscontroller` | Set graphics controller (vmsvga, vboxsvga, vboxvga) | `VBoxManage modifyvm "Debian12" --graphicscontroller vmsvga` |
| Configuration | `modifyvm --boot1` | Set first boot device (disk, dvd, net, none) | `VBoxManage modifyvm "Debian12" --boot1 dvd --boot2 disk` |
| Configuration | `modifyvm --firmware` | Choose BIOS or EFI firmware | `VBoxManage modifyvm "Debian12" --firmware efi` |
| Configuration | `modifyvm --ioapic` | Enable I/O APIC (needed for multiple CPUs) | `VBoxManage modifyvm "Debian12" --ioapic on` |
| Configuration | `modifyvm --nested-hw-virt` | Enable nested virtualization | `VBoxManage modifyvm "Debian12" --nested-hw-virt on` |
| Configuration | `modifyvm --clipboard-mode` | Shared clipboard (disabled, hosttoguest, guesttohost, bidirectional) | `VBoxManage modifyvm "Debian12" --clipboard-mode bidirectional` |
| Configuration | `modifyvm --draganddrop` | Drag and drop mode | `VBoxManage modifyvm "Debian12" --draganddrop bidirectional` |
| Configuration | `modifyvm --name` | Rename a VM | `VBoxManage modifyvm "Debian12" --name "Debian12-dev"` |
| Configuration | `modifyvm --description` | Set a VM description | `VBoxManage modifyvm "Debian12" --description "Dev web server"` |
| Configuration | `setproperty machinefolder` | Change the default folder for new VMs | `VBoxManage setproperty machinefolder /data/vms` |
| Storage | `createmedium disk` | Create a virtual hard disk (size in MB) | `VBoxManage createmedium disk --filename "/data/vms/Debian12.vdi" --size 40960 --format VDI` |
| Storage | `storagectl --add` | Add a storage controller to a VM | `VBoxManage storagectl "Debian12" --name "SATA" --add sata --controller IntelAhci` |
| Storage | `storageattach` (disk) | Attach a hard disk to a controller | `VBoxManage storageattach "Debian12" --storagectl "SATA" --port 0 --device 0 --type hdd --medium "/data/vms/Debian12.vdi"` |
| Storage | `storageattach` (ISO) | Attach an ISO as a DVD drive | `VBoxManage storageattach "Debian12" --storagectl "SATA" --port 1 --device 0 --type dvddrive --medium debian-12.iso` |
| Storage | `storageattach` (eject) | Eject the ISO from the DVD drive | `VBoxManage storageattach "Debian12" --storagectl "SATA" --port 1 --device 0 --medium emptydrive` |
| Storage | `modifymedium --resize` | Enlarge a disk (size in MB; extend the partition inside the guest afterwards) | `VBoxManage modifymedium disk "/data/vms/Debian12.vdi" --resize 81920` |
| Storage | `modifymedium --compact` | Shrink a dynamic VDI (zero free space in the guest first) | `VBoxManage modifymedium disk "/data/vms/Debian12.vdi" --compact` |
| Storage | `clonemedium` | Copy or convert a disk image (VDI, VMDK, VHD) | `VBoxManage clonemedium disk Debian12.vdi Debian12.vmdk --format VMDK` |
| Storage | `showmediuminfo` | Show details about a disk image | `VBoxManage showmediuminfo disk "/data/vms/Debian12.vdi"` |
| Storage | `closemedium` | Unregister a disk (add `--delete` to remove the file) | `VBoxManage closemedium disk "/data/vms/old.vdi" --delete` |
| Start / Stop | `startvm` | Start a VM with a GUI window | `VBoxManage startvm "Debian12"` |
| Start / Stop | `startvm --type headless` | Start a VM without a window (servers, SSH access) | `VBoxManage startvm "Debian12" --type headless` |
| Start / Stop | `controlvm acpipowerbutton` | Clean shutdown (like pressing the power button) | `VBoxManage controlvm "Debian12" acpipowerbutton` |
| Start / Stop | `controlvm poweroff` | Hard power off (like pulling the plug) | `VBoxManage controlvm "Debian12" poweroff` |
| Start / Stop | `controlvm savestate` | Save the VM state to disk and stop it | `VBoxManage controlvm "Debian12" savestate` |
| Start / Stop | `controlvm pause` | Pause a running VM | `VBoxManage controlvm "Debian12" pause` |
| Start / Stop | `controlvm resume` | Resume a paused VM | `VBoxManage controlvm "Debian12" resume` |
| Start / Stop | `controlvm reset` | Hard reset (reboot without shutdown) | `VBoxManage controlvm "Debian12" reset` |
| Start / Stop | `discardstate` | Discard a saved state | `VBoxManage discardstate "Debian12"` |
| Networking | `modifyvm --nic1 nat` | Set adapter 1 to NAT | `VBoxManage modifyvm "Debian12" --nic1 nat` |
| Networking | `modifyvm --nic1 bridged` | Set adapter 1 to bridged on a host interface | `VBoxManage modifyvm "Debian12" --nic1 bridged --bridgeadapter1 enp3s0` |
| Networking | `modifyvm --nic2 hostonly` | Set adapter 2 to host-only | `VBoxManage modifyvm "Debian12" --nic2 hostonly --hostonlyadapter2 vboxnet0` |
| Networking | `modifyvm --natpf1` | Add a NAT port-forwarding rule (name,proto,hostip,hostport,guestip,guestport) | `VBoxManage modifyvm "Debian12" --natpf1 "ssh,tcp,,2222,,22"` |
| Networking | `modifyvm --natpf1 delete` | Remove a NAT port-forwarding rule | `VBoxManage modifyvm "Debian12" --natpf1 delete "ssh"` |
| Networking | `controlvm natpf1` | Add a port-forwarding rule on a running VM | `VBoxManage controlvm "Debian12" natpf1 "http,tcp,,8080,,80"` |
| Networking | `controlvm setlinkstate1` | Connect or disconnect the virtual cable | `VBoxManage controlvm "Debian12" setlinkstate1 off` |
| Networking | `hostonlyif create` | Create a host-only interface | `VBoxManage hostonlyif create` |
| Networking | `hostonlyif ipconfig` | Set the IP of a host-only interface | `VBoxManage hostonlyif ipconfig vboxnet0 --ip 192.168.56.1 --netmask 255.255.255.0` |
| Networking | `natnetwork add` | Create a NAT network shared by several VMs | `VBoxManage natnetwork add --netname natnet1 --network "10.0.2.0/24" --enable --dhcp on` |
| Networking | `dhcpserver add` | Add a DHCP server to a network | `VBoxManage dhcpserver add --network=natnet1 --server-ip=10.0.2.3 --netmask=255.255.255.0 --lower-ip=10.0.2.10 --upper-ip=10.0.2.100 --enable` |
| Snapshots | `snapshot take` | Take a snapshot | `VBoxManage snapshot "Debian12" take "before-upgrade" --description "Clean install"` |
| Snapshots | `snapshot take --live` | Take a snapshot without pausing a running VM | `VBoxManage snapshot "Debian12" take "live-snap" --live` |
| Snapshots | `snapshot list` | List snapshots of a VM | `VBoxManage snapshot "Debian12" list` |
| Snapshots | `snapshot restore` | Restore a snapshot (VM must be off) | `VBoxManage snapshot "Debian12" restore "before-upgrade"` |
| Snapshots | `snapshot restorecurrent` | Restore the current snapshot | `VBoxManage snapshot "Debian12" restorecurrent` |
| Snapshots | `snapshot delete` | Delete a snapshot (merges its changes) | `VBoxManage snapshot "Debian12" delete "before-upgrade"` |
| Shared Folders | `sharedfolder add` | Add a host folder share (needs Guest Additions) | `VBoxManage sharedfolder add "Debian12" --name projects --hostpath /home/user/projects --automount` |
| Shared Folders | `sharedfolder remove` | Remove a shared folder | `VBoxManage sharedfolder remove "Debian12" --name projects` |
| Import / Export | `export` | Export a VM as an OVA/OVF appliance | `VBoxManage export "Debian12" -o Debian12.ova` |
| Import / Export | `import` | Import an OVA/OVF appliance | `VBoxManage import Debian12.ova` |
| Import / Export | `import --dry-run` | Preview import settings without importing | `VBoxManage import Debian12.ova --dry-run` |
| Guest Control | `guestproperty enumerate` | List guest properties (IP, OS, etc.; needs Guest Additions) | `VBoxManage guestproperty enumerate "Debian12"` |
| Guest Control | `guestproperty get` | Get the guest's IP address on adapter 1 | `VBoxManage guestproperty get "Debian12" "/VirtualBox/GuestInfo/Net/0/V4/IP"` |
| Guest Control | `guestcontrol run` | Run a command inside the guest | `VBoxManage guestcontrol "Debian12" run --exe /bin/ls --username user --password pass -- ls -la /tmp` |
| Guest Control | `guestcontrol copyto` | Copy a file from host to guest | `VBoxManage guestcontrol "Debian12" copyto --username user --password pass /home/user/file.txt --target-directory /tmp/` |
| Guest Control | `guestcontrol copyfrom` | Copy a file from guest to host | `VBoxManage guestcontrol "Debian12" copyfrom --username user --password pass /tmp/log.txt --target-directory /home/user/` |
| Guest Control | `controlvm screenshotpng` | Save a screenshot of the VM display | `VBoxManage controlvm "Debian12" screenshotpng shot.png` |
| Remote Display | `modifyvm --vrde` | Enable the VRDE (RDP) server (needs extension pack) | `VBoxManage modifyvm "Debian12" --vrde on --vrdeport 3389` |
| USB | `list usbhost` | List host USB devices | `VBoxManage list usbhost` |
| USB | `usbfilter add` | Add a USB filter so a device auto-attaches | `VBoxManage usbfilter add 0 --target "Debian12" --name "MyStick" --vendorid 0781 --productid 5567` |
| USB | `controlvm usbattach` | Attach a host USB device to a running VM | `VBoxManage controlvm "Debian12" usbattach <uuid-or-address>` |
| Extension Packs | `extpack install` | Install an extension pack | `VBoxManage extpack install Oracle_VirtualBox_Extension_Pack.vbox-extpack` |
| Extension Packs | `extpack uninstall` | Uninstall an extension pack | `VBoxManage extpack uninstall "Oracle VirtualBox Extension Pack"` |
| Extension Packs | `extpack cleanup` | Remove leftovers from failed installs | `VBoxManage extpack cleanup` |
| Monitoring | `metrics setup` | Enable performance metrics collection | `VBoxManage metrics setup --period 1 --samples 5 "Debian12"` |
| Monitoring | `metrics query` | Query collected metrics (CPU, RAM, etc.) | `VBoxManage metrics query "Debian12"` |

## Quick Recipe: Create a Headless Debian VM

```bash
VM="Debian12"
VBoxManage createvm --name "$VM" --ostype Debian_64 --register
VBoxManage modifyvm "$VM" --memory 4096 --cpus 2 --nic1 nat --natpf1 "ssh,tcp,,2222,,22"
VBoxManage createmedium disk --filename "$HOME/VirtualBox VMs/$VM/$VM.vdi" --size 40960
VBoxManage storagectl "$VM" --name "SATA" --add sata --controller IntelAhci
VBoxManage storageattach "$VM" --storagectl "SATA" --port 0 --device 0 --type hdd --medium "$HOME/VirtualBox VMs/$VM/$VM.vdi"
VBoxManage storageattach "$VM" --storagectl "SATA" --port 1 --device 0 --type dvddrive --medium debian-12.iso
VBoxManage startvm "$VM" --type headless
# then: ssh -p 2222 user@localhost (after install)
```
