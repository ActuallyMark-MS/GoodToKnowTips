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
- **Be aware that finishing the uninstallation requires a system reboot**

~~~
dism /online /Disable-Feature /FeatureName:Internet-Explorer-Optional-amd64
~~~

# Reboot commands
- To reboot OS, run this command

~~~
shutdown /r
~~~

- For a timed reboot, run it as its stated below
- To do a timed reboot, a value need to be typed after **/t**
- The timed value is typed in seconds
- In the example, OS will reboot in 1 hour

~~~
shutdown /r /t 3600
~~~

- To cancel a timed reboot run this command

~~~
shutdown /a
~~~

# Re-establish domain trust (without leaving domain)
- If a computer lost trust on domain, either logon with local account or remove network access and logon onto it with cached credentials
- Run the following command in Powershell and reboot computer

~~~
Test-ComputerSecureChannel -Repair -Credential domain\AdminUser
~~~
