# RaspberryPiServer

![Image of Pi](https://www.raspberrypi.org/app/uploads/2011/10/Raspi-PGB001-300x267.png)

Getting a webserver up and running for under $100 can be done. You can even expand the webserver to handle SQL, PHP and be used for FTP.

Here's how I got mine set up.

Parts Needed:
* [Canakit Raspberry Pi](https://www.amazon.com/CanaKit-Raspberry-4GB-Basic-Starter/dp/B07VYC6S56/ref=sr_1_5?crid=3QX1KT3VHBFWH&keywords=canakit+raspberry+pi+4+starter+kit+-+4gb+ram&qid=1585493679&sprefix=Canakit+%2Caps%2C170&sr=8-5)
* A Router you have admin access to - to make life easier I recommend an ethernet cable to plug directly in

Steps:
* Set up Raspbian 

The easiest way to do this is with NOOBS. Thankfully the Canakit comes with an SD card that has NOOBS loaded on it.

* Set up Apache and add PHP

The best tutorial to do this is right on [Raspberry Pi's own website](https://www.raspberrypi.org/documentation/remote-access/web-server/apache.md). One misstep I took was missing the right file location for index.php and where to remove index.html from. The right location is cd /home/pi/var/www/html/

* Get your website off just your local network and onto the internet

This part is a bit difficult but the basic premise is this. You need to:

1. Set your Raspberry Pi to a Static IP

The easiest way I found was via this tutorial [here](https://www.ionos.com/digitalguide/server/configuration/provide-raspberry-pi-with-a-static-ip-address/). Through the command line, it's simply using nano to edit a dhcpcd config file. The steps are:

Check for dhcpcd on your Pi
'sudo service dhcpcd status'

If it's active you can skip this step, if it's not active then
'sudo service dhcpcd start'
'sudo systemctl enable dhcpcd'

Then edit the config file in nano
'sudo nano /etc/dhcpcd.conf'

once nano is open you can scroll down to the commented part for a static IPv4 address and set it to what you want. Make sure the interface is also right, eth0 if ethernet and you can also set your static router ip. Then you just have to reboot your pi.

2. Set your router to allow an open port 80 for the static IP

This part depends a lot on your router. If your ISP provides your router you could run into access problems. This is why it's important to have your admin router password. The best tutorial I found for this was [here](https://portforward.com/router.htm)

and that's it! If it's going to start attached to your local network. For this project I wanted to be able to store the pi at a different physical location. In order to do that we need to allow SSH or Remote Desktop. For most users I think having access to the GUI of Raspbian is adventageous. 

* Optional: Set up Remote Desktop Login Access (WARNING!: This could hinder your router and network security if not done properly)

The easiest way to do this without opening up another port on your router is to whitelist your desktop/main laptop to the network that runs the raspberry pi webserver.

I installed Xrdp using this [guide](https://linuxize.com/post/how-to-install-xrdp-on-raspberry-pi/) and then followed the port set up instructions [here](https://www.windowscentral.com/how-use-remove-desktop-app-connect-pc-windows-10-0) and was able to connect via remote desktop using windows 10 to the raspberrry pi server~!

