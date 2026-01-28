# KDE Specific Proxy Scripts

These scripts are different from the ones present in the "Arch" directory.

> ⚠️ Use these scripts ONLY if you are using a KDE Plasma desktop.

These scripts will
- manually change the proxy configuration in "System Settings → Networking → Wi-Fi & Internet → Proxy" from "Use manually specified proxy configuration" to "No proxy".
- manually change the proxy configuration in Firefox Browser from "Manual proxy configuration" to "No proxy".
- make it so that pacman doesnt use the "XferCommand" line in /etc/pacman.conf which can lead to issues, and rather make it directly read the proxy environment variable set by the script.

These scripts were made after realising that for my KDE Plasma setup,
- the originial Arch scripts werent modifying the proxy in the KDE settings, used by the KDE GUI apps.
- pacman was showing errors regarding the XferCommand line, the reasons for which are yet to be understood by me.

I also wanted to make the script change Firefox's proxy settings.
