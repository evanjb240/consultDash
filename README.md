# Installing console dash on raspberry pi

### Video guide

Instructions are below, but here is a [video guide](https://www.youtube.com/watch?v=5C9ypE6JUuY)
to help guide you through it.

##### If RPI is a fresh install you might need to expand your file system

`sudo raspi-config`

`choose option 1 (expand file system)`

`reboot`


##### Install node

`sudo apt-get update`

`sudo apt-get upgrade`

####Node Options
Option: 1 node/npm out of the box

*NOTE: You must install node version v5.12 for the dash to work. Instructions on how to install a specific version of node incoming...*

`sudo apt-get install nodejs npm`

Option: 2 node/npm via nvm
Use this link to install nvm https://www.freecodecamp.org/news/node-version-manager-nvm-install-guide

Once nvm is installed:
`nvm install v16.11.0`
`nvm alias default v16.11.0`
`nvm use v16.11.0`

##### Install Chromium

`sudo apt-get update`

`sudo apt-get install chromium-browser -y`

##### Install Dash

`git clone https://github.com/evanjb240/consultDash.git`
`cd consultDash`
`npm install`


##### Install script for mausberry circuit

`http://mausberrycircuits.com/pages/car-setup`

Find the rc.local file and open it to point to the script needed to start the app
`sudo nano /etc/rc.local`

If you used Option 1 in the Node options section add:
`sudo sh /home/pi/consultDash/startScript.sh` 
If you used Option 2 in the Node options section add:
`sudo sh /home/pi/consultDash/startScriptNVM.sh`
*Note: run `which node` to find out/double-check the exact path of your node version and adjust startScriptNVM.sh as needed*
*Note: remove NODE_ENV=development when ready to run in the car*

Edit the autostart file to start the chromium-browser on reboot
`sudo nano /etc/xdg/lxsession/LXDE-pi/autostart`

Add this entry to Autostart
`@chromium-browser —kiosk --incognito file:///home/pi/consultDash/re-direct-page.html`

Once those are done, you can run `sudo reboot` to test it out. Assuming all is good, Alt+F4 to quit kiosk mode 

### Related guides

- [How to install a consult port](https://youtu.be/6Vd9oKWORPs?t=164)
- [How to install the OS on your Raspberry Pi](https://www.raspberrypi.org/learning/software-guide/quickstart/)
- [How to guide on installing that dash and power supply software (original)](https://github.com/gregsqueeb/consultDash)
- [How to guide on installing that dash and power supply software (forked)](https://github.com/evanjb240/consultDash)

### Suggested hardware

- [Raspberry Pi 3](https://www.adafruit.com/products/3055)
- [Touch screen](https://www.adafruit.com/products/2718)
- [Mausberry Circuit Power Supply](https://www.mausberrycircuits.com/collections/frontpage/products/4amp-car-supply-switch)

or

- [Consult cable](http://www.ebay.com/itm/Consult-Auto-Car-Diagnostic-Interface-Tool-14-Pin-Scanner-Scan-Cable-for-Nissan-/261194185645?hash=item3cd062fbad:g:EdIAAOxyB0VRrvEt&item=261194185645&vxp=mtr)
- [Serial to USB cable](http://www.ebay.com/itm/RS232-RS-232-Serial-to-USB-2-0-PL2303-Cable-Adapter-Converter-for-Win-7-8-10-/301675657589?hash=item463d453975:g:wRQAAOSwHnFVkj3Z)

# How to run for development

This will loop through MPH RPM and Temp so you can style things without being connected to a car :)

`npm run dev`
