# Change the first day of week for Linux

To display locale enter command:

`$ locale`

Edit the file:

`$ sudo nano /usr/share/i18n/locales/en_US`

Change first_weekday from 1 (Sunday) to 2 (Monday).

Now generate locale files:

`$ sudo locale-gen`

Reboot. All done. 