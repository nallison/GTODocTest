# GTO Automatic Duty login
Selected computers can be configured to allow GTO to not require account details for Duty login.  This feature is designed to provide automatic login for shared computers, physically located at the airfield, use for Ops control.  You will not need to enter your personal account details to login for pilot Duty.
# MS-Windows GTO Identity Service
The identity server is a MS-Windows service application.  It installs in the background, running a small http service running on port 2204.  This service allows GTO to verify the identity of the Duty computer.
# Installing the Identity Service
Unzip **GTOIdentityService1_01_1.7z** into a directory.

https://drive.google.com/drive/u/1/folders/1Hp9CWpMDPORxTCtbBFeVhr-Apwyv4wzY

In an administrator command prompt, enter the following two commands

**c:>GTOIdentityService1_01.exe install**

**c:>GTOIdentityService1_01.exe start**

Note : **install** and **stop** are two extra command line parameters you may want some day.

# Registration
Once the service is installed and started, open a web browser and goto **http://localhost:2204**

If everything is working you will see a reply something like this

<pre style="margin-left:20px;font-weight:bold">
{
  "name": "GTOIdentityService",
  "version": "1.0.1",
  "fingerprint": "CanterburyGlidingClub_78aca17abc4f320c636f41a0e37866cc"
}
</pre>

This fingerprint is needed in the next step.

P.S.  It's a good idea to reboot the computer before getting the fingerprint to check that the service correctly restarted on a reboot.
# GTO Server WhiteList
This last step is for somebody with GTO server access.  If that's not you please email the fingerprint details to somebody who does have access.

This computer's fingerprint needs to be registered in the GTO server database.
  
This fingerprint needs to be added to the **whitelist** database table.  Create a new table row with **type** = **auto_duty_login** and **value** = the fingerprint.

Please also add a meaningful description so we can better manage whitelisted computers in the future.
