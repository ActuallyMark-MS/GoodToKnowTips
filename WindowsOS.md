# WindowsOS Tips

# Remove the stale entry via “Programs and Features” (Legacy View)
Sometimes the modern Settings → Apps view misses things, but the classic control panel still allows cleanup.

Press Win + R
Type:

~~~
appwiz.cpl
~~~

Look for the old application.

If it appears, try Right-click → Uninstall.
It may prompt that files are missing—allow cleanup if offered.

# VM's that run on HyperV - Change NTP to not use HyperV as NTP source

In RegEdit navigate to this path:

~~~
Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\VMICTimeProvider
~~~

Change the record called **Enabled** to **0**

For domain joined servers, you can use this command to use Domain Controller as Time server afterwards:

~~~
w32tm /config /syncfromflags:domhier /update 
net stop w32time 
net start w32time
~~~

Check NTP status by using this command:

~~~
w32tm /query /status
~~~

# Uninstall Internet Explorer
- To uninstall Internet Explorer run the following command
- *Be aware that finishing the uninstallation requires a system reboot*

~~~
dism /online /Disable-Feature /FeatureName:Internet-Explorer-Optional-amd64
~~~
