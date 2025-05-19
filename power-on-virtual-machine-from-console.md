# Power on Virtualbox virtual machine from console

To power on a virtual machine from the conosole can be very useful when you want to start it remotely through a ssh connection. Here is a simple procedure which works very good for my network setup. 

1. Connect to the host using ssh. You will be asked to type the user password.  

`ssh user@host`

2. Check the names of the virtual machines:

`VBoxManage list vms`

The output will be something like: 

`"Debian" {ab81efb0-00df-4624-88bb-1a01f57f9e84}`

`"Windows7" {7be55420-7b10-4578-a2fa-b4ea301e2572}`

3. Run the virtual machine:

`VBoxManage startvm "Debian" --type headless` - if you want to run headless (without graphic interface)

or 

`VBoxManage startvm "Debian" --type gui` - if you want to run the virtual machine with graphic interface

For those using Remmina I strongly recommend the headless method, as they will be able to connect through RDP. 

4. Use the combined command once you open the terminal:

`ssh user@host "VBoxManage startvm 'Debian' --type headless"`

Enjoy your work!