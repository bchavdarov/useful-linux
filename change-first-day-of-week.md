# Change the first day of week for Linux

Tested with **Debian 11/MATE**. To display locale enter command:

`$ locale`

Edit the file:

`$ sudo nano /usr/share/i18n/locales/en_US`

In the section `LC_TIME` change line `first_weekday 1` (which means Sunday) to `first_weekday 2` (which is Monday). If such a line is missing, add it afrer the line that says: `week 7;19971130;1`

Now generate locale files:

`$ sudo locale-gen`

Reboot. All done. 

Workaround with **Fedora 40**. 

`$ locale -k LC_TIME`

will display more information about the environmental variable **LC_TIME**, which stores the time and date format.

Until now I haven't found a way to change `first_weekday=1` to `first_weekday=2` (in Fedora). I simply changed the locale variable LC_TIME by:

`$ sudo localectl set-locale LC_TIME=en_GB.utf8`

Again reboot. The calendar has **'Monday'** as the first day of the week
