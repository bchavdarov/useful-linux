# Change the first day of week for Linux

Tested with **Debian 11/MATE**. To display locale enter command:

`$ locale`

Edit the file:

`$ sudo nano /usr/share/i18n/locales/en_US`

In the section `LC_TIME` change line `first_weekday 1` (which means Sunday) to `first_weekday 2` (which is Monday). If such a line is missing, add it afrer the line that says: `week 7;19971130;1`

Now generate locale files:

`$ sudo locale-gen`

Reboot. All done. 