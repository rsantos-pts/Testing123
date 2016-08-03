To set up a new printer or update IP address printer on the Nowdocs server. (RDP server)

If replacing an existing printer be sure to right click on old printer, select printer properties, click on Sharing tab change existing Share name
Or you can delete the Old printer (just make a note of Printer make & model if replacing IP)

Go go Start > Devices and Printers
Click on Add a Printer
Choose an option, select Add a local or network printer as an Administrator
For what type of printer do you want to install, select Add a network, wireless or Bluetooth printer
It is will start a search for all printer devices, just click on Stop and select The printer that I want ins’t listed.
Select Add a printer using a TCP/IP address or hostname, click Next
Device Type: select  “TCP/IP Device”
Hostname or IP address: type IP address
Port name: leave alone
Check the box: Query the printer and automatically select the driver to use
Click Next

If it located the printer it will select the correct drivers and installed.
If not, select the correct manufacturer for the printer, if unknown select Generic Network Card.
It will search for the drivers, if still unknown manufacturer selec Generic > Generic/Text Only
Select Use the driver that is currently installed click Next
Type in Printer name
Select Share this printer so that others on your network can find and use it
Share name: enter name(ex:**_New W2Printer_**)
Location: leave blank
Comment: leave blank

Now go to Start > All Programs >Nowdocs >NowForms >Configuration Panel
Click on Data Directory
Click on Printers
Next select the Name of the printer that you would like to change, and only change the \name of printer
Example:
Old Value: \\qa-cli-nowdocs\ **_W2Printer_**
New Value: \\qa-cli-nowdocs\ **_New W2Printer_**
Click ok

I would run a Print test page to ensure that it is online and printing properly.
