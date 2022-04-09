---
title: Getting started
date: 2018-09-15T07:42:34.000+00:00
slug: getting-started

---
## What is Tabahi Console

Tabahi Console is a Web-to-IoT interface to manage and remote control your programmable IoT devices. Using Tabahi Console, you can:

* Push data to the server and view it as tables and graphs.
* Add/Edit variables on the web that are synced to the device. You can turn on remote switches through the web.
* Set telegram notification for any variable value change.
* You can run scripts on the server to avoid overloading small devices with heavy computing.
* Easily send messages from one device to another without a direct link between them.
* View device activity on the UDP monitor to debug it (Similar to Serial Monitor).
* Over-the-Air (OTA) updates for ESP32 and ESP8266.

## Installation

To start programming, follow these steps:

1. Install Arduino IDE.
2. Install ESP32 or ESP8266 compiler on Arduino IDE.
3. Download and add the Tabahi Console library to the Arduino IDE.
4. Create an account on [console.tabahi.tech](http://console.tabahi.tech). Sign and view your Token on the [account](http://console.tabahi.tech/#account) page.
5. Run the first example after configuring your _USER_TOKEN_ and _USER_SECRET_.

If everything works, you will see a new node appear on the [nodes list](http://console.tabahi.tech/#nodes).

Even though Jamdocs is so simple, you dont really need to set it up localy (you could just fork it on github to edit styles and md-files) - if you want to change it up a bit I recommend setting up localy for a better developer experience.

To set up a new instance of Jamdocs, and start developing just clone the project from Github like, go to the directory and run gridsome:

```bash
#include <TabahiConsole.h>

#define TTC_server "console.tabahi.tech"
#define USER_TOKEN "6223338df64144aac74a3622"
#define USER_SECRET "Deu9DqvSS6pbNuIoI43aCh"
#define DEBUG_TTC 1 //set to 1 to print verbose info on Serial

TTC Console(TTC_server, 2096, 44561, USER_TOKEN, USER_SECRET, DEBUG_TTC);

```