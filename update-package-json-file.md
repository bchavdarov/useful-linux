# Update the package.json file with the newest versions of the packages

The objective of the `npm update` command is to update your `package-lock.json` according to what you have specified in the `package.json` file. This is the normal behavior.

If you want to update your package.json file, you can use **npm-check-updates**: `npm install -g npm-check-updates`.

You can then use these commands:

    `ncu` -  Checks for updates from the package.json file
    `ncu -u` -  Update the package.json file
    `npm update --save` Update your package-lock.json file from the package.json file
