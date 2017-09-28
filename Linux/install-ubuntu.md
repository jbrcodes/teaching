Installing Ubuntu 14.10
=======================

Summary
-------

In this exercise we'll install the latest release of Ubuntu: 14.10. We will also install the VirtualBox Guest Additions (more on that below), and for those of us who aren't satisfied with Unity (the default desktop), we'll install a Windows-like alternative called GNOME (yes, the "G" is pronounced).


1. Create a New Virtual Machine (VM) in VirtualBox
--------------------------------------------------

Thanks to the nifty virtualization software called VirtualBox, we'll be able to install Ubuntu as a *guest OS* on a computer running Windows as the *host OS*.

1. Start VirtualBox. The first window that you see is called the *VirtualBox Manager*, and it shows all the Virtual Machines (VMs) that have been created.
2. Click on the *New* button.
3. You will now have a number of configuration values to set, and for some reason the screens don't look the same on all computers. Just make sure you do the following:
    1. Give your VM a meaningful name. For example, I might use *Jim Ubuntu 14.10*. (Using apostrophes in VM names -- like *Jim's Ubuntu 14.10* -- has sometimes caused strange behavior in the past. I recommend avoiding apostrophes in your VM name.)
    2. Set the type to Linux and the version to Ubuntu (64 bit).
    3. Specify 1024 MB of RAM.
    4. Accept all the defaults for creating your virtual hard disk.

Congratulations. You have just created the environment in which you will install Ubuntu.


2. Start Installation Using an ISO Image
----------------------------------------

Instead of installing from a CD-ROM, we're going to install Ubuntu from an ISO image that was previously downloaded and has been delicately copied to every computer in Room 9.

1. Select your new VM in the VirtualBox Manager and click on the *Start* button. You will be asked to select a start-up disk. Click on the folder icon with the green caret (^), just above the *Cancel* button.
2. Select file `ubuntu-14.10-desktop-amd64.iso` from the D drive. (The `.iso` extension may not be displayed.) Click on the *Open* button.
3. Click on the *Start* button.
4. Ignore a possible warning that some audio devices could not be opened.

You have now started the installation process, which will progress the same as if you had Ubuntu on a DVD.


### 2.1 Window with a "Test Pattern"

If your window resizes itself and shows what looks like a multi-colored test pattern, do this:

1. Press right &lt;Ctrl>-&lt;F1>. (Hold down the right-hand &lt;Ctrl> key and then press the &lt;F1> key.)
2. Press right &lt;Ctrl>-&lt;F7>.

You should now see the Welcome screen.


3. Install Ubuntu
-----------------

You'll be presented with a number of windows during the installation process. In most cases you can accept the defaults. The following table shows the window titles you will see and what action you should take:

  Window Title                 | Action
  -------------------------------------
  Welcome                      | Click on *Install Ubuntu*.
  Preparing to install Ubuntu  |   Accept the defaults. Click on *Continue*.
  Installation type            | Accept the defaults. Click on *Install Now*, then *Continue* for the popup window.
  Where are you?               | Chicago is fine; the installer is just trying to determine the correct time zone. Click on *Continue*.
  Keyboard layout              |  Accept the default. Click on *Continue*.
  Who are you?                 | Enter values for your (full) name, your computer, your user name and password. (Remember your password, or next time you'll be reinstalling! You may want to choose `foobar` or something similar that the whole cohort will remember.) Accept the other defaults. Click on *Continue*.

Now you're on your way! (Time passes... Installation shouldn't take more than 15 minutes unless a lot of people are installing at the same time.)

You will be asked to restart your VM. Click the *Restart Now* button. Most likely you'll see a terminal with some shutdown messages, and at the end it will say "Press &lt;Enter>." If pressing &lt;Enter> works, great! If it doesn't, you can click on the close window button (the red "X"), then select *Power off the machine* in the little window that appears, and click on the *OK* button.

Congratulations, you've successfully installed Ubuntu.



4. Install Guest Additions
--------------------------

Go ahead and log in to your shiny new Ubuntu VM. The first thing that you'll probably notice is that the window's awfully small. Thankfully we can fix that.

VirtualBox has some additional goodies called *Guest Additions* that improve interaction between the host and guest operating systems. Examples of this improved interaction include: copy/paste between the host and guest OS, improved hardware support by the host OS, and a shared folder between host and guest. These drivers and other utility programs will actually be installed *inside* your guest OS.

To install Guest Additions, select the *Insert Guest Additions CD image...* menu item from the *Devices* menu in the window where Ubuntu is running.

If this is not your first attempt to install Guest Additions, you will probably get an error message like "Unable to insert the virtual optical disk." If so, do the following:

1. Click the *Cancel* button.
2. Look in the Launcher (the icons along the left edge of the screen) for an image of a CD; it may be near the bottom.
3. Right-click on it and select *Eject* from the pop-up menu. Now you can try to install Guest Additions again.

Click on *Run* when asked if you would like to run it.

You'll be asked to type in your password again. (In Ubuntu-speak, you must *authenticate* again.) A terminal will appear and some status messages will be displayed. Installation can take a minute or so. Once you see "Press Return to close this window...," you can indeed press &lt;Enter> to close the window. For the Guest Additions to take effect, you need to restart Ubuntu, via the little gear icon in the upper-right corner. Select *Shutdown* and then *Restart*.

Log back in. One of the nice features of Guest Additions is it detects the screen's dimensions and lets you use the entire screen. If you press Right-&lt;Ctrl>-F (hold down the right &lt;Ctrl> key and press the F key), you can toggle back and forth between full-screen mode and window mode. Nice...


5. Update Software
------------------

Ubuntu 14.10 was released in October, and a few things have happened since then (software-wise). A program called Software Updater checks regularly to see if updated software is available. (Keeping your software up-to-date is one step towards keeping your system secure.) If it finds updated software, Software Updater will show itself in the dock along the left edge of the screen.

Click on the Software Updater icon to open it, then press the *Install Now* button. You'll be asked to type in your password. It's likely you'll be required to restart your virtual machine once updates have been installed. You can do so and then log in again.

If full-screen mode is not working anymore, then the software you just updated must have overwritten part of the Guest Additions. But never fear, you can install Guest Additions again to get your full-screen capability back.


6. Install the GNOME Desktop
----------------------------

By default, Ubuntu comes supplied with the relatively new Unity desktop. Unity has attempted to "simplify" or "unclutter" the desktop, but it has had the unintended side-effect of upsetting many long-time Ubuntu users. There are a number of reasons why you might not want to use Unity:

1. It tries to do some very fancy graphics that unfortunately slow down the computer a lot.
2. If you're coming from a Windows environment then the Unity desktop will seem very foreign to you.

Therefore, we're going to install the GNOME desktop, which is more like Windows. Don't worry, you'll be able to switch between desktops whenever you log in, so you can experiment with both.

One way to install software is by using the GUI approach. However, in the Linux world, the GUI way is for wimps. ;-) That's because there are only a limited number of things you can do using GUI-based tools, and many administrator tasks can only be accomplished via the terminal (also called the *shell* or *command line*). So here's a little taste of what's to come during the next 12 weeks.

Using the Unity desktop, open a new terminal window by pressing (left) &lt;Ctrl>-&lt;Alt>-T. (Hold down the left-hand &lt;Ctrl> and &lt;Alt> keys, then press the T key.) A terminal will appear. Type the following into the terminal:

    sudo apt-get install gnome-session-fallback

A very brief explanation: You use `sudo` whenever you want to execute a command as an administrator; `apt-get` is a program for managing software; we're asking `apt-get` to install something; and the something we're asking it to install is the software package called `gnome-session-fallback`.

Once you press &lt;Enter>, you will be asked to enter your password; it won't be displayed as you type it in. Then you'll see some messages about what other packages will be installed. Press Y and &lt;Enter> to confirm that you want to install GNOME. It will download the necessary pieces from the Internet and install them in the appropriate places. When it is done it won't give you a clear "successfully completed" message; what we'll see is that Linux is typically silent when things go well... and sometimes when things go wrong. :-}

To try out your new, more Windows-like desktop, log out (via the little gear icon in the upper-right corner). When you see the login screen again, there will be a little round Ubuntu icon above the right end of the password field. Click on it to see what desktops you have to choose from. The desktop called "GNOME Flashback (Metacity)" has fewer special graphics effects and seems to run the fastest, so choose that one. (See how the icon above the password field changes to a little foot? That's the GNOME icon.) Now log in as usual and notice the two menus at the upper-left of the screen. *Applications* contains some programs we'll be using, and the *Places* menu contains various folders that you can open using a file browser. Exploring is allowed, even encouraged!