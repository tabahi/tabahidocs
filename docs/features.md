---
title: Features
date: 2022-04-29
slug: features

---
Sign up or Login to the console here: [console.tabahi.tech](https://console.tabahi.tech)

## Tabahi Console

Tabahi Console is a Web-to-IoT interface to manage and remote control your programmable IoT devices. **It's like an online remote switch but with a lot more features than just a switch.**  
Using Tabahi Console, you can:

* Push data to the server and view it as tables and graphs.
* Add/Edit variables on the web that are synced to the device. You can turn on remote switches through the web.
* Set telegram notification for any variable value change.
* You can run scripts on the server to avoid overloading small devices with heavy computing.
* Easily send messages from one device to another without a direct link between them.
* Check the weather forecast and sun timings.
* View device activity on the UDP monitor to debug it (similar to Serial Monitor).
* Over-the-Air (OTA) updates for ESP32 and ESP8266.

![](/ttc.png)

#### Example use cases

* Dynamically control remote devices depending on the situation or data.
* Offload heavy computing to the cloud script.
* Send messages device-to-device.
* Change states or variables remotely without uploading a new code.
* Automate weather-dependent remote devices using forecasts.
* Use AI scripts to make control decisions on-the-fly using a trained model on previously collected data.

### Devices

Add up to 10 devices. Currently, the Arduino library supports ESP32 and ESP866 devices.

<img src="/screenshot-2022-05-04-at-04-55-48-console-tabahi-tech.png" alt="console view" width="1400"/>

### Variables Syncing

* View, edit, add and delete variables that are synced in the device's memory.
* Synced variables are essentially remote switches, but they support all other types of variables like boolean, integer, float, geo-coordinations, time, string, and HEX.
* When you set a new value on the console, the device will be synced to that newer value.
* Devices can also update the variables which are then synced to the console.

<img src="/screenshot-2022-05-04-at-04-56-12-console-tabahi-tech.png" alt="console view" width="1400"/>

In remote locations, there are usually dynamic situations where you can't trust a burned program to deal with whatever happens... like weather situations. In those cases, you need an online console where you can turn on or off switches depending on the condition without uploading a new code on the remote device... Synced variables can solve that problem. When you change a value on the web console, the device will also set to a new value.

### Trigger Notifications or Scripts

You can set up a telegram notification trigger for a certain change in a variable's value.

<img src="/screenshot-2022-05-04-at-04-59-05-console-tabahi-tech.png" alt="console view" width="1400"/>

### View and Plot data

The data pushed by a device can be easily viewed, plotted, and downloaded.

<img src="/screenshot-2022-05-04-at-04-56-26-console-tabahi-tech.png" alt="console view" width="1400"/>

<img src="/screenshot-2022-05-04-at-04-56-42-console-tabahi-tech.png" alt="console view" width="1400"/>

### Configure the Device

Remotely restart or activate deep sleep.

<img src="/screenshot-2022-05-04-at-05-00-15-console-tabahi-tech.png" alt="console view" width="1400"/>

### View UDP Logs from the device

UDP monitor is a simpler, faster, plain protocol for viewing the raw activity logs directly from the device. This helps during the debugging just like the Serial Monitor. A simple `Console.log("Hello")` from the device will print Hello on the UDP monitor.

<img src="/screenshot-2022-05-04-at-04-59-29-console-tabahi-tech.png" alt="console view" width="1400"/>

### OTA Update

Easily manage binary updates for devices. See an example [here](https://github.com/tabahi/TabahiConsole/blob/main/examples/OTAupdate/OTAupdate.ino) for a quick start with a safe mode in case of faulty codes.

<img src="/screenshot-2022-05-04-at-04-57-45-console-tabahi-tech.png" alt="console view" width="1400"/>

### Scripts

Javascript scripts that devices can trigger on the cloud can help offload heavy computing. Scripts run in a container and can read and update the synced variables of devices during the processing.

<img src="/screenshot-2022-05-04-at-04-58-04-console-tabahi-tech.png" alt="console view" width="1400"/>

Sign up or Login to the console here: [console.tabahi.tech](https://console.tabahi.tech)

![](https://console.tabahi.tech/stats/3.png)