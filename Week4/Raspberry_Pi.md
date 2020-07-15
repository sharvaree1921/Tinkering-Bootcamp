## Raspberry Pi
- The Raspberry Pi is a low cost, credit-card sized computer that plugs into a computer monitor or TV, and uses a standard keyboard and mouse.
- It’s capable of doing everything you’d expect a desktop computer to do.

![rpi](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/rpi.jpg)

### What R-pi can do?
- A General purpose Computer
- Media Centre
- Learn programming
- Learn and make electronic projects
- Take photos using camera module(in projects)
- Use in Robotics
- Network Storage
- Weather Station
- Retro Pi PlayStation
- Anything you can think of!

![rpi1](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/rpi1.JPG)

### Specifications-
- Broadcom BCM2837B0,Cortex-A-53(ARMv8) 64bit SoC @1.4 Ghz
- 1GB LPDDR2 SDRAM
- 2.4 Ghz and 5GHz IEEE 802.11.b/g/n/ac wireless LAN,Bluetooth 4.2,BLE
- Extended 40pin GPIO header
- Full size HDMI
- 4 USB 2.0 ports
- CSI camera port for connecting a raspberry pi camera
- DSI display port for connecting a Raspberry pi touchscreen display
- 4-pole stereo output and composite video port
- Micro SD port for loading your operating system and storing data
- 5V/2.5A DC power input
- Power-over-Ethernet(PoE) support(requires seperate PoE HAT)

![rpi2](https://github.com/sharvaree1921/Tinkering-Bootcamp/blob/master/rpi2.JPG)

### What will you need to start?
- Raspberry Pi
- Keyboard and Mouse
- HDMI cable
- Power Cable
- Display screen(monitor or TV)

### Tour of Raspbian-
- Raspbian is one of the operating systems of Rpi.There are several many.It is one of the most widely used one.
- It has similar features like any other OS.
- Text editor,browsing web,games,programming languages,add/remove software,terminal,etc. are some of its features.
- Recall the presentation demonstrated on TV.

**GUI(Graphical User Interface)**
- Through GUI , we are ble to hover around,click tabs,etc,(i.e. the commands executed by us and what we see on the front end).But,before GUI there was 
**CLI(Command Line Interface)**. 
- CLI mainly include shell(in mac)/cmd(in windows)/terminal(in ubuntu) .That is we type some command and that particular function was executed.
- Terminal is there in Raspbian OS.

### Linux Terminal Commands
- _ls_ : listing of the content of current directory(ls Downloads)
- _cd_ : changes the current directory to current specified(ls Desktop)
- _pwd_:displays the nae of current working directory(pwd)
- _mkdir_: to make directory of specified name in the current location(mkdir sharveree)
- _rmdir_: to remove the directory of dpecified name in the current location(rmdir sharvaree)
- _cp_ : makes the copy of the file(cp sharvaree)
- _mv_: moves a file and places it to the specific location(mv ~/fileA /home/otherUser/ would move the file fileA from your home directory to that of the user   otherUser)
- _chmod_  : You would normally use chmod to change the permissions for a file. The chmod command can use symbols u (user that owns the file), g (the files group) , and o (other users) and the permissions r (read), w (write), and x (execute). Using chmod u+x *filename* will add execute permission for the owner of the file.
- _ssh_ : 'ssh' gives access to use CLI of Rpi through other device /monitor wirelessly.ssh denotes the secure shell. Connect to another computer using an encrypted network connection.
- _sudo_ : The sudo command enables you to run a command as a superuser, or another user. Use sudo -s for a superuser shell.
- _unzip_ : The unzip command extracts the files from a compressed zip file.
- _tar_ : Use tar to store or extract files from a tape archive file. It can also reduce the space required by compressing the file similar to a zip file.
To create a compressed file, use tar -cvzf *filename.tar.gz* *directory/* To extract the contents of a file, use tar -xvzf *filename.tar.gz*
- _pipes_ : A pipe allows the output from one command to be used as the input for another command. The pipe symbol is a vertical line |. For example, to only show the first ten entries of the ls command it can be piped through the head command ls | head.
- _tree_ : Use the tree command to show a directory and all subdirectories and files indented as a tree structure.
- _curl_ : Use curl to download or upload a file to/from a server. By default, it will output the file contents of the file to the screen.
- _Hostname_ : The hostname command displays the current hostname of the system. A privileged (super) user can set the hostname to a new one by supplying it as an argument (e.g. hostname new-host).
- _Hostname -I_ : This displays the IP address of the device.

**1.SSH** : ssh gives access to use **CLI** of Rpi through other desktop/monitor wirelessly .
Ex:Suppose we want to control the functions of rpi through windows,type 'ssh pi@192.168.0.162' in your cmd.192.168.0.162 is the IP address of our device.Execution of this command enables the access of CLI of Rpi.That means whatever commands we write in our windows terminal is as good as writting commands in rpi CLI.Thus,we have connected it wirelessly.

**2.VNC Connect** : VNC gives access to use **GUI** of Rpi wirelessly through another desktop/monitor in live time.

### PyAutoGui
- PyAutoGui is an external library of python used to control the keyboard and mouse events.
- The x, y coordinates used by PyAutoGUI has the 0, 0 origin coordinates in the top left corner of the screen. The x coordinates increase going to the right (just as in mathematics) but the y coordinates increase going down (the opposite of mathematics)
- All keyboard presses done by PyAutoGUI are sent to the window that currently has focus, as if you had pressed the physical keyboard key.
- There are various PyAutoGui commands.One can look them [here](https://pypi.org/project/PyAutoGUI/)







