# Windows: Resetting a Network Adapter

After exiting the program the connection often doesn't reset correctly. Means
you still have no connection (somehow the network lock isn't always deactivated,
even when closing the program correctly)

If someone encounters that problem, this helps (resetting the connected network
adapter):

```cmd
REM N.B. Start cmd as admin
netsh interface show interface

REM See what network adapter is used to connect you to the internet
netsh interface IPv4 set dnsserver <your_network_adapter_name> dhcp
```

---

re:

> "The only real issue I have with Eddie is that it changes the Windows DNS
> settings. This is usually a good thing as it ensures all DNS requests are
> resolved by AirVPN's servers, but if for any reason the client shuts down
> suddenly, I need to manually reset the DNS settings before I can connect to the
> internet again (Control Panel -> Network and Sharing Center -> Change adapter
> settings -> right-click connection -> Properties -> select Internet Protocol
> Version 4 -> Properties -> Preferred DNS server: 8.8.8.8)."
