Firmware Development Environment

The firmware for the Adaptive Multi-Sensor Predictive Smart Irrigation System was developed using embedded C/C++ programming in the Arduino IDE environment. The ESP32 microcontroller was programmed to interface with multiple sensors, process environmental parameters, calculate the soil dryness condition, and automatically control the irrigation pump.

The firmware integrates different sensor libraries for communication and data acquisition:

1)Wire.h – Used for I2C communication between the ESP32 and LCD module.
2)LiquidCrystal_I2C.h – Used for displaying real-time sensor values and pump status.
3)OneWire.h and DallasTemperature.h – Used for interfacing the DS18B20 temperature sensor.
4)DHT.h – Used for humidity measurement using the DHT sensor.

The developed firmware performs the following operations:

1)Initialization of sensors and output devices.
2)Continuous acquisition of soil moisture, temperature, and humidity data.
3)Calculation of a dryness index based on environmental conditions.
4)Automatic ON/OFF control of the irrigation pump.
5)Display of real-time system parameters on an LCD module.


The ESP32 continuously collects data from multiple sensors to understand the surrounding soil and environmental conditions.

Soil Moisture Measurement

The soil moisture sensor is connected to an analog input pin of the ESP32. The analog value obtained from the sensor is converted into a moisture percentage.

The moisture value is calculated using:

Moisture(%)=
(4095−ADC Value/4095)*100

where:

ADC value represents the analog output from the soil moisture sensor.
Higher moisture percentage indicates wet soil conditions.

Temperature Measurement

The DS18B20 temperature sensor is used to measure soil/environment temperature. The sensor communicates with the ESP32 through the OneWire protocol.
The temperature value is obtained using:
humidity = dht.readHumidity();

Adaptive Dryness Index Calculation

Unlike conventional irrigation systems that rely only on soil moisture, this system uses multiple environmental parameters to determine irrigation requirements.

A dryness index (DI) is calculated by combining:

Soil moisture level
Temperature variation
Humidity condition

The implemented mathematical model is:

DI=(100−M)+Kt(T−25)−Kh(H)
Where:
DI = Dryness Index
M = Soil moisture percentage
T = Temperature value
H = Humidity percentage
KT = Temperature weighting factor
KH = Humidity weighting factor

Automated Irrigation Control Logic

Start

Read moisture, temperature and humidity values

Calculate Dryness Index

If DI > Threshold:
        Turn Pump ON
Else:
        Turn Pump OFF

Display sensor values and pump status

Repeat continuously

Firmware implementation:if(DI > threshold)
{
   digitalWrite(RELAY_PIN,HIGH);
   Serial.println("Pump ON");
}
else
{
   digitalWrite(RELAY_PIN,LOW);
   Serial.println("Pump OFF");
}
LCD Display Interface

A 16×2 I2C LCD module is used to provide real-time monitoring of system parameters.

The LCD displays:

Soil moisture percentage
Temperature value
Humidity percentage
Dryness Index
Pump operating status
M:45% H:60%
T:28C Pump:ON

Firmware Code Implementation

The firmware consists of the following major modules:
Sensor Initialization
The setup function initializes all sensors, LCD communication, and relay control pins.
void setup()
{
 Serial.begin(115200);

 pinMode(RELAY_PIN, OUTPUT);

 lcd.init();
 lcd.backlight();

 sensors.begin();
 dht.begin();
}

Sensor Reading Module
soilMoisture = analogRead(MOISTURE_PIN);

sensors.requestTemperatures();
temperature = sensors.getTempCByIndex(0);

humidity = dht.readHumidity();

Data Processing Module
DI = (100 - moisture)
     + k_temp*(temperature-25)
     - k_hum*(humidity);

Pump Control Module
if(DI > threshold)
{
 digitalWrite(RELAY_PIN,HIGH);
}
else
{
 digitalWrite(RELAY_PIN,LOW);
}
