# Start or stop the GNOME Display Manager

If you need for some reason to start your Ubuntu system directly in the text environment without starting GNOME Display Manager these commands are useful. 

## Prevent GUI on boot permanently

`sudo systemctl set-default multi-user.target`

Use code with caution. You will need to run sudo reboot to test this change.

Stop the current GUI immediately:

`sudo systemctl stop gdm3`

Bring the desktop back manually:

`sudo systemctl start gdm3`

## Undo this change permanently

`sudo systemctl set-default graphical.target`
