#define BLYNK_PRINT Serial 
#define BLYNK_TEMPLATE_ID "TMPLSYP4gTqH" //copy from blynk 
#define BLYNK_DEVICE_NAME "smart irrigation" //copy from blynk 
#define BLYNK_AUTH_TOKEN "suvm6kxo3sUv1Zx3iLOry9829dMsSvcj" //copy from blynk 
#include <ESP8266WiFi.h> 
#include <BlynkSimpleEsp8266.h> 
WidgetLCD lcd(V0); 
char auth[] = "suvm6kxo3sUv1Zx3iLOry9829dMsSvcj"; // Blynk auth token 
char ssid[] = "ashwini"; // username or ssid of your WI-FI 
char pass[] = "mohankumar"; // password of your Wi-Fi 
int sensorvalue ; //variable for storing value read from sensor 
#define relay 0 //D3 of nodemcu connected to Realy IN 
#define sensor 14 //D5 of nodemcu connected to D0 of sensor 
void setup() 
{ 
Serial.begin(115200); 
pinMode (relay,OUTPUT); //set relay pin to OUTPUT mode 
pinMode (sensor,INPUT); //set sensor pin to INPUT mode 
Blynk.begin(auth, ssid, pass); 
lcd.clear(); //Use it to clear the LCD Widget 
lcd.print(6,0, "SMART"); // use: (position X: 0-15, position Y: 0-1, "Message you //want to print")
lcd.print(4,1,"IRRIGATION"); 
delay(9000); 
lcd.clear(); 
} 
void loop() 
{ 
Blynk.run(); 
sensorvalue=digitalRead(sensor); //read soil moisture sensor value 
Serial.println(sensorvalue); //print the read value on serial window 
if (sensorvalue == 1) //if sensor value is 1 
{ 
digitalWrite(relay,LOW); //turn on relay 
Serial.println("Pump Started, Water Flowing"); 
lcd.print(4,0,"pump on"); //msg on blynk lcd widget 
delay(1000); 
} 
else 
{ 
digitalWrite(relay,HIGH); //turn off relay 
Serial.println("Pump Stopped, Water Not Flowing"); 
lcd.print(4,0,"pump off"); //msg on blynk lcd widget 
delay(1000); 
} 
lcd.clear(); //clear lcd widget 
}
