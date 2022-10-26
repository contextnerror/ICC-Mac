# How to Install #

Download the version of the app you want from the [releases page.](https://github.com/contextnerror/ICC-Mac/releases)

Before you open the archive, you will need to strip the quarantine flag from it. Otherwise, macOS will incorrectly claim the app is broken. There are two ways to do this step.

#### Using an app ####
You will need xattred. [Download xattred here.](https://eclecticlight.co/xattred-sandstrip-xattr-tools/)
Open "ICC-(version number).tgz" in xattred. In the list of flags, you should see "com.apple.quarantine". Click it, then click "Strip flag". You can now uncompress the file. 

#### Using Terminal ####
This isn't recommended unless you're familiar with the command line.
Enter this command in Terminal: `xattr -d com.apple.quarantine /path/to/.tgz`
You can now uncompress the file. 

### Configuring Wine ###
Right-click on "Ice Cream Calculator.app" and select "Show Package Contents".
Open "Wineskin.app", then click "Advanced". From there, click "Tools" and select "Refresh Wrapper".
Once this is done, close Wineskin. You should be able to run Ice Cream Calculator now.

#### If you are unable to open Wineskin (exec[number].bat error) ####
Check to see if the Wineskin app has a quarantine flag on it, and remove it.

