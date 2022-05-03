---
title: Getting started
date: 2022-02-03
slug: getting-started

---
# Console

Sign up or Login to console here: [console.tabahi.tech](https://console.tabahi.tech)

## What is Tabahi Console

Tabahi Console is a Web-to-IoT interface to manage and remote control your programmable IoT devices. Using Tabahi Console, you can:

* Push data to the server and view it as tables and graphs.
* Add/Edit variables on the web that are synced to the device. You can turn on remote switches through the web.
* Set telegram notification for any variable value change.
* You can run scripts on the server to avoid overloading small devices with heavy computing.
* Easily send messages from one device to another without a direct link between them.
* Check weather forecast and sun timings.
* View device activity on the UDP monitor to debug it (similar to Serial Monitor).
* Over-the-Air (OTA) updates for ESP32 and ESP8266.

## Installation

To start programming, follow these steps:

1. Install [Arduino IDE](https://www.arduino.cc/en/software).
2. Install [ESP32](https://microcontrollerslab.com/install-esp32-arduino-ide/) or [ESP8266](https://microcontrollerslab.com/how-to-install-esp8266-board-arduino-ide/) compiler on Arduino IDE.
3. Download and add the [Tabahi Console library](https://github.com/tabahi/TabahiConsole) to the Arduino IDE. Goto **Sketch > Include Library > Add .ZIP Library** to install the library.
4. Create an account on [console.tabahi.tech](http://console.tabahi.tech). Sign and view your Token on the [account](http://console.tabahi.tech/#account) page.
5. Run the first example after configuring your `USER_TOKEN` and `USER_SECRET`.

If everything works, you will see a new node appear on the [devices list](http://console.tabahi.tech/#nodes).

A simple example for interfacing the console with ESP32 or ESP8266:

```cpp
#include <TabahiConsole.h>

const char* ssid     = "WiFi Name";
const char* password = "WiFi Pass";

#define TTC_server "api.tabahi.tech" //api.tabahi.tech
#define USER_TOKEN "6225868df6412032c74a3698"
#define USER_SECRET "Deu9DqvSS6pbNuIoI43aCh"
#define DEBUG_TTC 1 //set to 1 to print verbose info on Serial

TTC Console(TTC_server, 2096, 44561, USER_TOKEN, USER_SECRET, DEBUG_TTC);

String mac_address = ""; //will set in setup. Used for node identification.
int increment = 0; //dummy variable


void setup()
{
  Serial.begin(115200);
  WiFi.disconnect(true); // delete old wifi config
  delay(1000);
  WiFi.begin(ssid, password);

  mac_address = WiFi.macAddress();
  Serial.print(F("\nMAC: "));
  Serial.println(mac_address);

  Console.initialize();

  delay(5000); //wait 5 sec for Wifi to connect
}



void loop()
{
  if (WiFi.status() == WL_CONNECTED)
  {
    if (Console.node_token_valid == false) //Need to get a Node Token before anything else
    {
      WiFiClient TCPclient;

      //Identify Node Token using mac address
      int idn_status = Console.Identify(&TCPclient, mac_address);

      if (idn_status == 1) {
        Serial.print("Got NT: ");
        Serial.println(Console.NT);
      }
      else {
        Serial.printf("Identification failed %d\n", idn_status);
      }
    }

    if (Console.node_token_valid == true) //if have a registered NT
    {
      sync_variables(); //sync, update, add, edit variables

      push_data();    //push data to tables


      //print some logs on UDP monitor:
      Console.log("UTC time: "); //will show on UDP monitor on console.tabahi.tech
      Console.logln(Console.realtime()); //time is synced with UTC epoch in total seconds (unsigned long)
      Console.logln("Done");
      Console.CommitLogs(mac_address.c_str()); //send all the monitor logs to server, using mac address as the identifier
      //must call CommitLogs() after log() to send logs to the server.
    }

    delay(30000); //wait for 30 seconds
  }
  else
  {
    Serial.print("Waiting for WiFi\t");
    Serial.println(ssid);
    WiFi.disconnect(true);
    WiFi.begin(ssid, password); //try reconnecting
    delay(10000); //wait 10 sec
  }
}




int sync_variables()
{
  WiFiClient TCPclient;
  int n_vars = Console.runSync(&TCPclient);

  if (n_vars >= 0) //check if variables sync was ok
  {
    Console.logln("Sync: OK");
    Console.printVariables(); //print all the vairables on Serial
  }
  else
    Serial.printf("Sync failed, status: %d \n", n_vars);

  unsigned long heartbeat = Console.get_ulong("heartbeat");

  //check if a there is a variable 'example'
  if (Console.isValidType("example", 'b'))
    bool example = Console.get_bool("example");

  //setting a variable to a new value
  increment++;
  Console.set_int("increment", increment); //this new value will show on the console after the next sync cycle

  return n_vars;  //returns number of synced variables. Error if it's negative.
}



void push_data()
{
  //create a data row:
  Console.newDataRow(); //new row with a current timestamp
  Console.push_ulong("a",  123);
  Console.push_float("b", 456.789);
  Console.push_String("c_geo", String("1.223") + "," + String("-5.235"));  //heading including 'geo' will link to google maps

  WiFiClient TCPclient;
  //Data is not sent until 'CommitData' is called.
  if (Console.CommitData(&TCPclient) > 0) Console.logln("Data sent");
}
```