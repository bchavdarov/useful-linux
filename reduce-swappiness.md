# How to change swappiness

Check your current swappiness value. Type in the terminal:

`cat /proc/sys/vm/swappiness`

The result will probably be 60.

To change the swappiness into a more sensible setting, type in the terminal:

`xed admin:///etc/sysctl.conf`

Scroll to the bottom of the text file that opens and add your swappiness parameter to override the default.

`# Decrease swap usage to a more reasonable level`
`vm.swappiness=10`

Save, close and reboot. After reboot check your swappines value:

`cat /proc/sys/vm/swappiness`

Should be 10