# TECHware_HTH_2k25
#include "DHT.h"

#define DHTPIN 23       // DHT sensor data pin
#define DHTTYPE DHT11   // Sensor type DHT11

DHT dht(DHTPIN, DHTTYPE);

const int soilSensorPin = 2;  // Soil moisture sensor analog pin

void setup() {
  Serial.begin(115200);
  dht.begin();
  delay(1000);

  Serial.println("Starting sensors...");
}

void loop() {
  // Read Temperature and Humidity from DHT11
  float humidity = dht.readHumidity();
  float temperature = dht.readTemperature();

  // Read Soil Moisture sensor analog value
  int soilValue = analogRead(soilSensorPin);
  int soilMoisturePercent = map(soilValue, 4095, 0, 0, 100);

  // Check if DHT reading is valid
  if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Failed to read from DHT sensor!");
  } else {
    Serial.print("Humidity: ");
    Serial.print(humidity);
    Serial.print("%  Temperature: ");
    Serial.print(temperature);
    Serial.println(" *C");
  }

  Serial.print("Soil Moisture: ");
  Serial.print(soilMoisturePercent);
  Serial.println("%");

  delay(2000);  // 2 seconds delay between readings
}
