# Ubuntu-BlackScreen-Fix

This is a guide to fixing Ubuntu black screen crashes not specifically upon startup. More specifically, this is a response to black screen crashes upon clicking the "Show Applications" and "Activiites buttons, as well as occasionally at random. This issue appears to be common with the r9 390, and is a power-saving issue within Ubuntu. By running this script, you force the OS to run at high and perfomance modes, preventing it from terminating the graphical adapter. I run this in 18.04 LTS upon every boot, although, i see no reason why this would not work on any other ubuntu-based distro or version.

If you have a similar issue, with a Radeon GPU and a similar linux distro, feel free to try out this solution. It is quite simple, really.

## How to: 

### Install dpm-query: 

You must first install dpm-query tool, courtesy of illwieckz on github: 

https://github.com/illwieckz/dpm-query

I have included a script which can do this for you, or you can follow the wonderful directions provided on his repository.

Allow permission to run the script: 
```
cd /path/to/Ubuntu-BlackScreen-Fix

chmod +x dpm-query_install
```

Run the script:
```
cd /path/to/Ubuntu-BlackScreen-Fix

./dpm-query_install
```

As mentioned in the terminal, this will by default install  into your Documents folder. Feel free to move it wherever you wish.

### Initialize command to run on boot: 

The command to set your performance priorities must be run upon each boot of the system. So instead of typing that in every time, lets have the OS do the work for us. Note, because this is a sudo command this will require a few extra steps! The rc.local file in your /etc folder does exactly this. So to do that, we will take our necessary command and place it into that file, or make our own!

First, we need to determine if your /etc/ folder has an rc.local file. Go ahead and look for yourself.

#### If /etc does NOT have an rc.local file: 

Copy the rc.local file i have provided into your /etc folder:
```
sudo cp -r '/path/to/Ubuntu-BlackScreen-Fix/rc.local' /etc/
```

If this was you, congrats! You're system should be functioning!

If it wasn't, however...

#### If /etc DOES have an rc.local file: 

Edit your rc.local file:
```
sudo nano /etc/rc.local
```

Add this command somewhere between '#!/bin/sh -e' and 'exit 0'. THIS IS IMPORTANT.
```
sudo dpm-query set all high performance
```

And that's it! Your system will execute this file at the start of every boot, and will hopefully solve your issues in the same way it solved mine :)



