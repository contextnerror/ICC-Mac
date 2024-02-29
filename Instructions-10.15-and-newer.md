# For 10.15 and newer #

You will need to use Wineskin.

## Setting up Wineskin Winery ##

Install Wineskin from here: https://github.com/Gcenx/WineskinServer

You should now have an app called Wineskin Winery. Open it.

Click the + button next to New Engine(s) available! and pick the newest standard engine from the dropdown. This is the one with the highest number, but without "D3DMetal" or "wip" in the name. Click download and ok.

If there is a notice saying Wrapper Version has an update, update it

## Setting up the wrapper ##

Click Create New Blank Wrapper. Pick the name that you want the app to show as. Avoid special characters or spaces. Wait for the wrapper to generate, this will take a while.  

Once it has been generated, click the option to view it in Finder. In Finder, right-click the wrapper and Show Package Contents. Open the Wineskin app inside. You can now close the Winery app.

In Wineskin, click Advanced and go to the Advanced tab. Make sure that "Disable Mono Installation" is NOT checked. If it is, uncheck it, then go to the Tools tab and hit "Refresh Wrapper" and "Rebuild Wrapper", in that order.  

Regardless of what you did in the last step, go to the Tools tab and click Config Utility (winecfg). In the new window, go to the Applications tab. Click Default Settings in the list, then under Windows Version select "Windows 10" from the dropdown. Click Apply then OK.   

Wait for the "a tool is running" indicator to go away.  

## Installing ICC ##

Keep Wineskin open and go to Ice Cream Calc's official download site in your browser. Download the latest version and unzip it.

Back to Wineskin, click Install Software. Click Choose Setup Executable and pick the IceCreamCalculatorSetup.exe file from your downloads. In the installer that opens, DO NOT change the default install location. Un-check the option to create a desktop shortcut. Un-check the option to open the application and click finish.

Wineskin will ask you to choose an executable. Pick IceCreamCalculator.exe from the dropdown.

## Cosmetic changes ##

Under the Configuration tab, change the Version field to whatever version of ICC you're using. If you want to change the icon, click browse and select an image file. You can download the .icns file from this repository and use it as the icon if you would like the default ice cream cone icon.

## Configuring ICC ##
These steps are now obsolete with ICC version 4. They are kept for historical reference but do not need to be done.
~~Open the ICC application and go to settings. Check "Place data folder with executable". Save and exit settings, then exit ICC.~~

~~Go back to Finder and Show Package Contents. Navigate to `drive_c > ProgramData > Ice Cream Calculator`. There should be Sorbet, Gelato and Ice Cream .chart files. Take these files and move them to `drive_c > ProgramFiles (x86) > Ice cream calculator > Data`.~~

~~You should now be ready to go.~~
