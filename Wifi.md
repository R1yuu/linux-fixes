# Wi-Fi Problems
## Wi-Fi loses connection to Network constantly
### Description
On a battery powered Laptop the Wifi is able to find and connect to Networks.  
When on power cord everything works fine. When on battery alone the Wifi disconnects and connects constantly.
### Analyze
Use `$ iwconfig` to check if the "Power Management" for the Wifi-Adapter is turned on:
```
wlan0     IEEE 802.11  ESSID:"Wifi-SSID"  
          Mode:Managed  Frequency:5.18 GHz  Access Point: xx:xx:xx:xx:xx:xx   
          Bit Rate=780 Mb/s   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=70/70  Signal level=-39 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:59   Missed beacon:0

```
### Solve
Turning "Power Management" to "off" should help with this problem, editable in the file `/etc/NetworkManager/conf.d/default-wifi-powersave-on.conf`.  
You can edit/create this file by using:  
`$ sudo nano /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf`  
If the file already existed it will typically contain these lines:
```
[connection]
wifi.powersave = 3
```
To fix our problem now edit/fill the file to contain:
```
[connection]
wifi.powersave = 2
```
### Explanation
Possible values for Powersave are:
```
NM_SETTING_WIRELESS_POWERSAVE_DEFAULT (0): use the default value
NM_SETTING_WIRELESS_POWERSAVE_IGNORE  (1): don't touch existing setting
NM_SETTING_WIRELESS_POWERSAVE_DISABLE (2): disable powersave
NM_SETTING_WIRELESS_POWERSAVE_ENABLE  (3): enable powersave
```
### Source
Stackexchange: <https://unix.stackexchange.com/questions/269661/how-to-turn-off-wireless-power-management-permanently>  
Github: <https://gist.github.com/jcberthon/ea8cfe278998968ba7c5a95344bc8b55>
