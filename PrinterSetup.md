To set up a new IP address for a printer on the Nowdocs server. (RDP to server)

If replacing an existing printer be sure to right click on old printer, select printer properties, click on Sharing tab change existing Share name
Or you can delete the Old printer (just make a note of Printer make & model if replacing IP)

Go go _Start > Devices and Printers_

Click on _Add a Printer_

Choose an option, select _Add a local or network printer as an Administrator_

For what type of printer do you want to install, select _Add a network, wireless or Bluetooth printer_

It is will start a search for all printer devices, just click on _Stop_ and select _The printer that I want ins’t listed._

Select _Add a printer using a TCP/IP address or hostname_, click _Next_

_Device Type: select  _“TCP/IP Device”_

Hostname or IP address: type IP address

Port name: leave alone

Check the box: Query the printer and automatically select the driver to use_

Click _Next_

If printer was located it will select and install the drivers.

If not, select the correct manufacturer for the printer, if unknown select _Generic Network Card._

It will search for the drivers, if still unknown manufacturer select _Generic > Generic/Text Only_

Select _Use the driver that is currently installed_ click _Next_

Type in Printer name

Select _Share this printer so that others on your network can find and use it_

_Share name: enter name(ex:**_New W2Printer_**)

Location: leave blank

Comment: leave blank_

Now go to _Start > All Programs >Nowdocs >NowForms >Configuration Panel_

Click on _Data Directory_

Click on _Printers_

Next select the Name of the printer that you would like to change, and only change the \name of printer

Example:

_Old Value: \\qa-cli-nowdocs\ **_W2Printer_**_
_New Value: \\qa-cli-nowdocs\ **_New W2Printer_**_

Click _Ok_

I would run a Print test page to ensure that it is online and printing properly.
