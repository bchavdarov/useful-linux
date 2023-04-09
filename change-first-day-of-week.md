# Change the first day of week for Linux

Tested with **Debian 11/MATE**. To display locale enter command:

`$ locale`

Edit the file:

`$ sudo nano /usr/share/i18n/locales/en_US`

Change first_weekday from 1 (Sunday) to 2 (Monday). If such a line is missing, add it afrer the line: `week 7;19971130;1
`

Now generate locale files:

`$ sudo locale-gen`

Reboot. All done. 