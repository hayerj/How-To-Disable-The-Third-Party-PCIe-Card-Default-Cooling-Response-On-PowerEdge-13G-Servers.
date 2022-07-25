# How-To-Disable-The-Third-Party-PCIe-Card-Default-Cooling-Response-On-PowerEdge-13G-Servers.

Symptoms
The default automatic cooling response on PowerEdge 13G server for third-party PCIe cards provisions airflow based on common industry card requirements. Our thermal algorithm targets delivery of maximum 55C inlet air to the PCIe card region based on that industry standard. 

For some cards may not need additional cooling above the baseline (such as ones that have their own fan), Dell has enabled an OEM IPMI based command to disable this default fan response to the new PCIe card.

Note that the ability to disable this feature only removes the fan response associated to the addition of third-party PCIe card and does not compromise original thermal algorithm based cooling needs. If the fan speeds were already high due to other system needs, then disabling this feature may not have an effect.
Resolution
ENABLE/DISABLE Third-Party PCIe card based default system fan response: 
Download and install OpenManage BMC Utility.
Enable the "IPMI over LAN" in iDRAC of the target machine, this can ben done via iDRAC Web GUI or BIOS Setup.
Go to the installation folder of OpenManage BMC Utility, run the following commands:
```
Set Third-Party PCIe Card Default Cooling Response Logic To Disabled
ipmitool -I lanplus -H <IPADDRESS> -U <USERNAME> -P <PASSWORD> raw 0x30 0xce 0x00 0x16 0x05 0x00 0x00 0x00 0x05 0x00 0x01 0x00 0x00 

Set Third-Party PCIe Card Default Cooling Response Logic To Enabled
ipmitool -I lanplus -H <IPADDRESS> -U <USERNAME> -P <PASSWORD> raw 0x30 0xce 0x00 0x16 0x05 0x00 0x00 0x00 0x05 0x00 0x00 0x00 0x00 

Get Third-Party PCIe Card Default Cooling Response Logic Status
ipmitool -I lanplus -H <IPADDRESS> -U <USERNAME> -P <PASSWORD> raw 0x30 0xce 0x01 0x16 0x05 0x00 0x00 0x00 
```
```wrap
The response data is:
16 05 00 00 00 05 00 01 00 00 (Disabled)
16 05 00 00 00 05 00 00 00 00 (Enabled)
```
https://www.dell.com/support/kbdoc/en-us/000135682/how-to-disable-the-third-party-pcie-card-default-cooling-response-on-poweredge-13g-servers
