---
title: Getting started
date: 2018-09-15T07:42:34.000+00:00
slug: getting-started

---
## What is Tabahi Console

Tabahi Console is a Web-to-IoT interface to manage and remote control your IoT devices. Using Tabahi Console, you can:

* Push data to the server and view it as tables and graphs.
* Add/Edit variables on the web that are synced to the device. You can turn on remote switches through the web.
* Set telegram notification for any variable value change.
* You can run scripts on the server to avoid overloading small devices with heavy computing.
* Easily send messages from one device to another without a direct link between them.
* View device activity on the UDP monitor to debug it (Similar to Serial Monitor).
* Over-the-Air (OTA) updates for ESP devices.

## Local installation

Even though Jamdocs is so simple, you dont really need to set it up localy (you could just fork it on github to edit styles and md-files) - if you want to change it up a bit I recommend setting up localy for a better developer experience.

To set up a new instance of Jamdocs, and start developing just clone the project from Github like, go to the directory and run gridsome:

```bash
git clone https://github.com/samuelhorn/jamdocs project-name
cd project-name
gridsome develop
```