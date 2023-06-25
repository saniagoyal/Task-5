# Task-5
/* DHT-22 sensor with 12c 16x2 LCD with Arduino uno
2   Temperature   and humidity sensor displayed in LCD
3   based on: http://www.ardumotive.com/how-to-use-dht-22-sensor-en.html   and
4   https://www.ardumotive.com/i2clcden.html for the i2c LCD library by Michalis   Vasilakis
5   Recompile by adhitadhitadhit
6   Notes: use LCD i2c Library from   link above, i'm not sure why but new Liquidcristal library from Francisco Malpartida   isn't working for me
7   other thing, check your */
8
9//Libraries
10#include   <dht.h> // sensor library using lib from https://www.ardumotive.com/how-to-use-dht-22-sensor-en.html
11#include   <LiquidCrystal_I2C.h> // LCD library using from  https://www.ardumotive.com/i2clcden.html   for the i2c LCD library 
12#include <Wire.h> 
13dht DHT;
14
15//Constants
16#define   DHT22_PIN 2     // DHT 22  (AM2302) - pin used for DHT22 
17LiquidCrystal_I2C lcd(0x27,16,2);   // set the LCD address to 0x27 after finding it from serial monitor (see comment   above) for a 16 chars and 2 line display
18
19//Variables
20float hum;  //Stores   humidity value
21float temp; //Stores temperature value
22
23void setup()
24{
25     Serial.begin(9600);
26    lcd.init();                      // initialize the   lcd 
27  // Print a message to the LCD.
28  lcd.backlight();
29  lcd.setBacklight(HIGH);
30}
31
32void   loop()
33{
34    int chk = DHT.read22(DHT22_PIN);
35    //Read data and store   it to variables hum and temp
36    hum = DHT.humidity;
37    temp= DHT.temperature;
38     //Print temp and humidity values to LCD
39    lcd.setCursor(0,0);
40    lcd.print("Humidity:   ");
41    lcd.print(hum);
42    lcd.print("%");
43    lcd.setCursor(0,1);
44     lcd.print("Temp: "); 
45    lcd.print(temp);
46    lcd.println("Celcius");
47     delay(2000); //Delay 2 sec between temperature/humidity check.
48}
