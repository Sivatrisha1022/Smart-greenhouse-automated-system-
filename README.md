# Smart-greenhouse-automated-system-
Smart Greenhouse Automated System is an IoT-based project that monitors temperature, humidity, and soil moisture using sensors. It automatically controls irrigation, ventilation, and lighting to create an optimal environment for plant growth, improving efficiency and reducing manual effort in agriculture
## Overview
An IoT-based automated greenhouse monitoring system that controls temperature, humidity, and irrigation.

## Features
- Automatic watering
- Temperature monitoring
- Humidity control
- Real-time monitoring

## Components Used
- Arduino / Raspberry Pi
- DHT11 Sensor
- Soil Moisture Sensor
- Relay Module
- Water Pump

## Applications
Smart farming and automated agriculture.

## Author
Sivatrisha K

## Code
#include <DHT.h>

#define DHTPIN 2
#define DHTTYPE DHT11

DHT dht(DHTPIN, DHTTYPE);

int soilMoisturePin = A0;
int waterPump = 8;
int fan = 9;

void setup() {
  Serial.begin(9600);
  dht.begin();

  pinMode(waterPump, OUTPUT);
  pinMode(fan, OUTPUT);

  digitalWrite(waterPump, HIGH);
  digitalWrite(fan, HIGH);
}

void loop() 
{
  float temperature = dht.readTemperature();
  float humidity = dht.readHumidity();
  int soilValue = analogRead(soilMoisturePin);

  Serial.print("Temperature: ");
  Serial.println(temperature);

  Serial.print("Humidity: ");
  Serial.println(humidity);

  Serial.print("Soil Moisture: ");
  Serial.println(soilValue);

  // Soil Moisture Control
  if (soilValue > 600) 
  {
    digitalWrite(waterPump, LOW);
    Serial.println("Water Pump ON");
  } else 
  {
    digitalWrite(waterPump, HIGH);
    Serial.println("Water Pump OFF");
  }

  // Temperature Control
  if (temperature > 30) 
  {
    digitalWrite(fan, LOW);
    Serial.println("Fan ON");
  } else 
  {
    digitalWrite(fan, HIGH);
    Serial.println("Fan OFF");
  }

  delay(2000);
}
