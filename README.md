# SPRecon
SharePoint Patch Reconciler

Sometimes when installing SharePoint updates things do not go as planned. Perhaps while trying to install the update you get the message "An error occurred while running detection". Or maybe it says the patch is not applicable.
Another scenario is when the updates appear to have installed correctly but running PSConfig shows "some farm products and patches were not detected on this or other servers".
Adding a new server to the farm can be a challenge trying to know which updates are needed and then you have to go download them all.

This is what SharePoint Patch Reconciler is designed to help with.
The SharePoint Patch Reconciler - or SPRecon - is a PowerShell script to 'fix up' a broken Windows Installer cache and report what patches are installed in the farm but detected as missing from a server. 

What it will do:
It will automatically use other servers in the farm as a source to restore missing .MSI and .MSP files as well as using them as a source location for patches missing from the server.
The script will prompt for an alternate source path in case your existing farm is missing them.
If updates are detected as missing on the local server, it will offer to attempt to install them from an identified source. 
If you choose not to let it do the installation, it will display the command line it would have used.
It will report products and updates missing on other servers in the farm that will need to be addressed before PSConfig can complete successfully.
The report will also show disk space available (if the server is low on disk space sometimes only a subset of the .MSP patches are installed successfully resulting in unexpected 'missing' patches)
If the server is not currently part of a farm, it will prompt for the SQL server and Configuration database of the target farm in order to identify what products and updates are needed in order to join.

Usage:
  Rename to .ps1
  Launch from right-click or in ISE (if within ISE, I recommend widening the app to at least 100 chars to prevent text wrapping).
  It will automatically use all other servers in the farm as an msi/msp source 
  It will also use its current location (and all subfolders ) as a source location (so don't run it from C:\ or it may take a while 😊 )
  When it prompts for a path, you can specify another server as \\server\c$\windows\installer even if it is not the same farm
  If patches are missing with sources available, it should prompt before applying patches.


The tool creates log/work files in %temp% with _SP_Recon_* as part of the name.
If applying a patch fails, there should be "*_MSPApply" Installer logs to assist in identifying the cause or the failure
