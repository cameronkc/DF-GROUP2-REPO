-f cridex.vmem imageinfo

<img width="379" alt="imageinfo" src="https://user-images.githubusercontent.com/15861347/144344199-a4f0912f-fdb2-4100-88ca-f1a8019dbc95.PNG">

Processes running

-f cridex.vmem –profile=WinXPSP2x86 pslist (process list)

![InternetShortcut](pslist.PNG)

-f cridex.vmem –profile=WinXPSP2x86 pstree

 ![InternetShortcut](pstree.PNG)
 
-f cridex.vmem –profile=WinXPSP2x86 psxview (Hidden)

![InternetShortcut](psxview.PNG)

Sockets and Connections

-f cridex.vmem –profile=WinXPSP2x86 connscan (Connections at time of download)

![InternetShortcut](connscan.PNG)

-f cridex.vmem –profile=WinXPSP2x86 sockets

![InternetShortcut](sockets.PNG)

-f cridex.vmem –profile=WinXPSP2x86 cmdline

![InternetShortcut](CMDline.PNG)

-f cridex.vmem –profile=WinXPSP2x86 prodump -p 160  --dump-dir .

![InternetShortcut](dump%20direcrory.PNG)

strings 1640.dmp | grep -F1 "41.168.5.140" -C 5

![InternetShortcut](file%20dump.PNG)

Strings 1640.dmp | less

This command allows you to go page by page for the information above then his Q to exit the page.
Next, we want to see if the executable we are using is Malicious or not so run it in a malware detector. I used Virustotal.com because it shows the number malware detectors that believe a file is malicious or not.

![InternetShortcut](malwear%20detector.PNG)

So we see here that 30/67 detectors believe this executable is malware.
Next we want to see how the exe is launched.

vol.py -f cridex.vmem --profile=WinXPSP2x86 printkey -K "Software\Microsoft\Windows\CurrentVersion\Run" can be used to see what programs run at startup.

 ![InternetShortcut](startuphive.PNG)
 
Here we see the start up hive. If you look closely you can see there is an executable being launched for the Robert profile named as KB00207877.exe.
Now we have to find a connection between this file and the main file.
We can use strings 1640.dmp | grep -Fi "KB00207877.exe" to find the connection.

![InternetShortcut](connection.PNG)
This shows a direct connection of the two files.
