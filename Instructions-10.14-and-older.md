# For 10.14 and older #

You will need to use Wine via MacPorts.  
This section uses ` symbols to indicate code blocks, these should not be included in the actual commands.

## Installing the Command Line Tools ##

If you don't have them already, you will need a copy of the Xcode Command Line Tools. Install these by entering `xcode-select --install` in the terminal app.

## Installing Macports ##

You won't be able to use the default installation method or some ports will fail to build. You'll need to do two installations from source.  
The following instructions are adapted from this MacPorts mailing list post: https://lists.macports.org/pipermail/macports-dev/2019-August/041001.html

### Download the source code ###

Go to https://www.macports.org/install.php#installing and click the link for either tar.bz2 or tar.gz. It doesn't matter which one. Then go to Finder and double-click the file to uncompress it. This should give you a folder. Right-click this folder and select "New Terminal at Folder".

### Set up your shell ###

In the terminal app, enter this command: `export PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:`. To confirm it worked, enter `echo $PATH` and it should say `/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:`. If there's anything else in there, something is currently modifying your path and you will need to temporarily disable it.

The next steps all need to be done in the same terminal window/session, or else the path will revert to whatever it was previously.

### Make the first "bootstrap" MacPorts install ###

Note: some of the next commands will involve using `sudo`. If you don't know how to do this, read the [related Apple support article.](https://support.apple.com/guide/terminal/enter-administrator-commands-apd5b0b6259-a7d4-4435-947d-0dff528912ba/mac)

Enter `./configure --prefix=/opt/bootstrap --with-applications-dir=/opt/bootstrap/Applications --without-startupitems`. Wait for it to finish then enter `make && sudo make install`. Wait for this to finish.

Sync the ports tree by entering `sudo /opt/bootstrap/bin/port -v sync`. Then download curl using `sudo /opt/bootstrap/bin/port -v -N install curl`.

You are now done with the current MacPorts folder, and can delete it from your Finder. You can also close the terminal window.

### Make the second MacPorts install ###

Repeat the instructions from "Download the source code". You don't need to re-download the source, just uncompress the original one again. Then repeat the steps in "Set up your shell". After that enter `./configure --with-curlprefix=/opt/bootstrap` in terminal, then `make && sudo make install`.

You should now have MacPorts installed. You can delete the MacPorts folder and tar file from your downloads. Close the terminal window.

#### Set up MacPorts in your path ####

Open up /.bash_profile in your home directory, and add `export PATH=/opt/local/bin:/opt/local/sbin:$PATH` to it. If you don't have a .bash_profile file you might need to create one, but first make sure it's not just invisible. Press shift+command+period to enable viewing hidden files.

Save .bash_profile when you're done.

These instructions are a simplification, if you already have shell customizations you might need to do something different. Read https://guide.macports.org/#installing.shell for full details. (If you're not sure if you do or not—you probably don't.)

## Set up macports-wine ##

Install a modern version of git: `sudo port install git`

Once you have git, enter `cd /opt`  
Clone [Gcenx's Wine repository](https://github.com/Gcenx/macports-wine) into /opt with this command: `sudo git clone https://github.com/Gcenx/macports-wine.git`

You will now need to add this as a local repository so MacPorts can find it. To do this, open terminal and enter the command `sudo vi /opt/local/etc/macports/sources.conf`. This will open the vi text editor to edit the sources file. This is needed because regular text editors don't normally have permissions to edit system files. If you already have a text editor that is capable of editing these files (most coding text editors, for example) you can use that instead.

### Adding macports-wine to sources.conf ###

In sources.conf, there should be a line that starts with "rsync:". You will want to paste `file:///opt/macports-wine` above this line. To do this in vi, perform this sequence (capitalization matters!):  

G (moves to the bottom of the file)  
up arrow key (move cursor up one line)  
i (enter "insert mode")  
enter (make a new line)  
command v (paste)  
esc key (exit insert mode)  
:wq (save and quit)

If you make a mistake, you can enter :q! to exit without saving. (Make sure to exit insert mode first by pressing esc, or else you'll just type :q! instead.)

### Configure macports.conf ###

These instructions will be very similar to the previous section. You will want to paste this at the bottom of macports.conf:

```
macosx_deployment_target     10.13
macosx_sdk_version           10.13
```

To do this in vi:

`sudo vi /opt/local/etc/macports/macports.conf`  

G (moves to the bottom of the file)  
i (enter "insert mode")  
enter (make a new line)  
command v (paste)  
esc key (exit insert mode)  
:wq (save and quit)

## Installing Wine ##

First index your new ports by entering `cd /opt/macports-wine` then `sudo portindex`. Then enter `cd ~` and run `sudo port -v sync`. After registering the new ports you want to install the 10.13 sdk by running `port install MacOSX10.13.sdk`. Finally you can install Wine by entering `sudo port install wine-devel`. You can also install wine-stable or wine-staging, but wine-devel is the best compromise between updates and stability.

Since Wine is being built from source, MacPorts is going to ask you to install a lot of other programs that are needed to build Wine. This is normal. This also means it will take a very long time, so you might want to find something else to do for a while.

Assuming this all worked, congrats! You now have Wine.

## Setting up Wine ##

In terminal, enter `winecfg`. Wine should notice that you don't have a wineprefix yet, and make one for you. Then it will create a window called "Wine configuration". In the applications tab of this window, make sure Windows Version is set to Windows 10, then apply any changes and press OK.

Now that you have a wineprefix, you can download ICC. Go to the official website and download the latest version, then unzip it to get an .exe file. In terminal, type in `wine `, DO NOT HIT ENTER, and drag the .exe file into the terminal window to enter its file path. ([What is a file path?](https://support.apple.com/guide/terminal/specify-files-and-folders-apd3cf6fe02-3ec8-48f1-951f-866e52955fc8/mac)) Then you can press enter. An installer will open. In the installer that opens, DO NOT change the default install location. Un-check the option to create a desktop shortcut. Un-check the option to open the application and click finish.

## Configuring ICC ##

Run ICC by entering this in terminal: `wine ~/.wine/drive_c/Program\ Files\ \(x86\)/Ice\ cream\ calculator\ 4/IceCreamCalculator.exe 
`. There will be some fixme: messages, this is fine.

~~Under settings, check "Place data folder with executable". Save and exit settings, then exit ICC.~~ This step is outdated for ICC 4.0

~~In terminal, enter `cd ~/.wine/drive_c/ProgramData/Ice\ Cream\ Calculator`. Then enter `mv *.chart ~/.wine/drive_c/Program\ Files\ \(x86\)/Ice\ cream\ calculator/Data`. This moves the default chart files into the new data folder.~~ This step is outdated for ICC 4.0

You should now be ready to go. To run ICC in the future open terminal and enter `wine ~/.wine/drive_c/Program\ Files\ \(x86\)/Ice\ cream\ calculator\ 4/IceCreamCalculator.exe`.

### Bonus: setting up a shortcut for ICC ###

If you don't want to enter the entire command to ICC every time, you can make something called an alias. To do this, you add a line to your .bash_profile file.  
For example, if I wanted the command "ICC" to run the program, I would add this line:`alias ICC='/opt/local/bin/wine /Users/(your username here).wine/drive_c/Program\ Files\ \(x86\)/Ice\ cream\ calculator\ 4/IceCreamCalculator.exe'`

You can also use something like [Automator](https://support.apple.com/guide/automator/welcome/mac/10.14) to run the program for you.

