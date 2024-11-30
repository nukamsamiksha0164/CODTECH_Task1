# CODTECH_Task1
#include <DHT.h>
#include <LiquidCrystal.h>

// Pin definitions
#define DHTPIN 2         // Pin where the DHT sensor is connected
#define DHTTYPE DHT11    // DHT 11 or DHT22

// Create a DHT sensor object
DHT dht(DHTPIN, DHTTYPE);

// LCD pin connections (change as needed)
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  // Start serial communication
  Serial.begin(9600);
  
  // Initialize DHT sensor
  dht.begin();
  
  // Initialize LCD
  lcd.begin(16, 2);
  lcd.print("Temp & Humidity");
  delay(2000); // Wait for the display to stabilize
}

void loop() {
  // Read temperature and humidity
  float humidity = dht.readHumidity();
  float temperature = dht.readTemperature(); // Default is in Celsius

  // Check if reading failed
  if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Failed to read from DHT sensor!");
    lcd.clear();
    lcd.print("Sensor error");
    return;
  }

  // Print values to serial monitor
  Serial.print("Humidity: ");
  Serial.print(humidity);
  Serial.print(" %\t");
  Serial.print("Temp: ");
  Serial.print(temperature);
  Serial.println(" *C");

  // Display values on LCD
  lcd.clear();
  lcd.setCursor(0, 0);  // Set cursor to the first row
  lcd.print("Humidity: ");
  lcd.print(humidity);
  lcd.print(" %");

  lcd.setCursor(0, 1);  // Set cursor to the second row
  lcd.print("Temp: ");
  lcd.print(temperature);
  lcd.print(" C");

  // Wait before next reading
  delay(2000);  // Delay between readings (2 seconds)
}



