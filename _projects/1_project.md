---
layout: page
title: Smart Garden
description: Having fun with sensors
img: assets/img/1.jpg
importance: 1
category: work
---

This projects contains the code necessary to set up an automatic irrigation and data collection system for a garden using an Arduino microcontroller. The system is designed to monitor soil moisture levels and automatically water the garden when the moisture falls below a certain threshold. In addition, the system collects data on temperature, humidity, and light levels to provide insights into growing conditions and plant health. The code is well-documented and includes instructions on how to set up the hardware and configure the system. The projects also includes sample data and scripts for visualizing the collected data.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Sorry for the messy set up      
</div>

This is how it started me playing with bunch of arduino sensors and a board. then decided to try it on my small plants and then a friend garden, then it was upgraded to a working demo for our company Industrial ML Inc
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/2.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A Sample sketch
</div>


Here is a demo code that I am using to collect data and connect to wifi, In the project a sample code like this and add sending  data through MQTT to the reciever section that will handle the irrigation part

{% raw %}
```cpp
#include <DHT.h>
#include <DHT_U.h>
#include <ESP8266.h>
// Global variables and defines

#define DHTPIN 2
#define DHTTYPE DHT11

const char *SSID     = "WIFI-SSID"; 
const char *PASSWORD = "PASSWORD" ; 

char* const host = "www.google.com"; 
int hostPort = 80;
ESP8266 wifi;

 int smokeA0 = A0;
 int soilA1 = A1;
 int rainA2 = A2;

DHT dht(DHTPIN, DHTTYPE);


void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
  pinMode(smokeA0, INPUT);
  pinMode(soilA1, INPUT);
  pinMode(rainA2, INPUT);
  Serial.begin(9600);
  wifi.init(SSID, PASSWORD);
  dht.begin();

}
 
void loop() {
   Serial.println(); 
   // Wifi module Test 
   wifi.httpGet(host, hostPort);
  // get response buffer. Note that it is set to 250 bytes due to the Arduino low memory
  char* wifiBuf = wifi.getBuffer();
   
  char *wifiDateIdx = strstr (wifiBuf, "Date");
  for (int i = 0; wifiDateIdx[i] != '\n' ; i++)
  Serial.print(wifiDateIdx[i]);

  int smoke_level = analogRead(smokeA0);
  int soil_moisture = analogRead(soilA1); 
  int rain_level = analogRead(rainA2); 

  float h = dht.readHumidity();
  // Read temperature as Celsius
  float t = dht.readTemperature();
  Serial.print("Temperature = ");
  Serial.print(t);
  Serial.println(" *C ");

  Serial.print("Humidity = ");
  Serial.print(h);
  Serial.println(" %\t");

  Serial.print("Smoke detector: ");
  Serial.println(smoke_level);

  Serial.print("Soil Moisture: ");
  Serial.println(soil_moisture);

  Serial.print("rain detector: ");
  Serial.println(rain_level);


  delay(2000);

}
```
{% endraw %}
