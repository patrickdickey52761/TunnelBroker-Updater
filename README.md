# TunnelBroker-Updater
THe purpose of this program is to automatically update your TunnelBroker IPv6 tunnel
whenever your IPv4 address changes. When you call the program, you will supply the 
following arguments (paramters):
    tunnelID (String)
    tunnelPassword (String)
    updateInterval(integer) <-- This value cannot be less than 30. 

The update interval needs to be set in minutes. If you update too frequently, then Hurricane
Electric can block your IP Address. If you set it too long, then you might lose connectivity
when your IPv4 address changes. What happens here is every time the Update Interval runs out,
the program will contact a webserver to obtain your current IPv4 address. If it is different
from the stored copy, it will trigger an update to TunnelBroker and then write the new IPv4 
address into a file. 

Originally, I wrote this in Java with the intention of making it a GUI application. The issue I 
ran into was that I couldn't change the timer interval. So, I created a Python script that did
what I wanted, although the issue with changing the update time persisted. I'm recreating this in
Rust because 1) it's memory safer and 2) my limited understanding is that I can kill off the previous
thread and restart it with a new owner, passing in the new update interval time. THe first versions 
of this application will not have that capability yet. When I fully understand how to do it, and what 
dangers (if any) that it may create, I'll implement it. Eventually my goal is to create either a GUI 
application that calls this program, or pull this code into the GUI Application itself. So, in future 
versions, the argument list may evolve as I change what needs to be passed in.

INSTALLATION AND USE:

To install, simply compile this with cargo. Before you run this the first time, you must create a text 
file called IPAddress.txt in the same directory as your executable. The format of the file is 
tunnelID,password,IPv4Address (comma separated values). In order to force an update the first time 
through, I would put 0.0.0.0 as your IPv4 address.

LICENSING:

This program will be licensed under both the GNU GPL v 2.0 or later and the MIT License. Some crates 
and other dependencies may be licensed in other methods. If you wish to use this project under another 
license, please contact me to work something out. I may ask that you contribute major changes back. 
Where conflicts between the licensing options that I have chosen arise, the GNU GPL v 2.0 will be the 
prevailing license.
