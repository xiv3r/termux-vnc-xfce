## Termux VNC Xfce GUI

### Graphical Environment
This article is only applicable only to Termux installations running on Android 7.0 or higher.

* Termux provides support for programs that use X Window System. However, there no hardware acceleration for rendering and user will have to install a third party application to view graphical output.

### Enabling the X11 Repository
X11 packages are available in a separate APT repository. You can enable it by running the following command:

    pkg install x11-repo

It will automatically add appropriate sources.list file and PGP key.

To disable this repository, you need to uninstall package x11-repo.

### Setting up VNC
Server
If you decided to use VNC for graphical output, follow these instructions for properly setting up VNC server.

1. Install package `tigervnc`:

       pkg install tigervnc

2. After installation, execute this:

       vncserver -localhost

At first time, you will be prompted for setting up passwords:

You will require a password to access your desktops.

Password:
Verify:
Would you like to enter a view-only password (y/n)? n

Note that passwords are not visible when you are typing them and maximal password length is 8 characters.

3. If everything is okay, you will see this message:

     New 'localhost:1 ()' desktop is localhost:1

     Creating default startup script /data/data/com.termux/files/home/.vnc/xstartup
     Creating default config /data/data/com.termux/files/home/.vnc/config
     Starting applications specified in /data/data/com.termux/files/home/.vnc/xstartup
     Log file is /data/data/com.termux/files/home/.vnc/localhost:1.log
 
It means that X (vnc) server is available on display 'localhost:1'.

4. Finally, to make programs do graphical output to the display 'localhost:1', set environment variable like shown here (yes, without specifying 'localhost'):

       export DISPLAY=":1"

You may even put this variable to your bashrc or profile so you don't have to always set it manually unless display address will be changed.

Client
Here will be assumed that you use this Android VNC client: VNC Viewer (developed by RealVNC Limited).



### VNC Viewer: new connection
1. Determine port number on which VNC server listens. It can be calculated like this: 5900 + {display number}. So for display 'localhost:1' the port will be 5901.

2. Now open the VNC Viewer application and create a new connection with the following information (assuming that VNC port is 5901):

Address:
127.0.0.1:5901

Name:Termux

If you are using VNC client on a computer using the same network as the phone does, make sure you correctly start a VNC session and know the IP address of the device.

