#include <ESP8266WiFi.h>
const char* ssid  = "wifi";
const char* password = "wifipasswordname";
const char* host = "10.0.0.19";
const int IR0=D0;
const int IR1=D1;
const int IR2=D2;
const int IR3=D3;
const int IR4=D4;
const int IR5=D5;
long state0=0;
long state1=0;
long state2=0;
long state3=0;
long state4=0;
long state5=0;
String response;
WiFiClient client;
 //RFID TAG!=2700228CD851
 //RFID TAG!=270021E8628C
 //RFID TAG!=270021E4E200
void setup() {
 Serial.begin(9600);
 delay(10);
 pinMode(IR0,INPUT);
 pinMode(IR1,INPUT);
 pinMode(IR2,INPUT);
 pinMode(IR3,INPUT);
 pinMode(IR4,INPUT);
 pinMode(IR5,INPUT);
 Serial.println();
  Serial.print("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println("WiFi connected");
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
    delay(5000);
}
void loop() {  
         if (Serial.available())  {
      response = Serial.readStringUntil('\n');
      Serial.println(response);
  }

    if(response=="2700228CD851"||response=="270021E4E200"){
    Serial.println("Door Unlocked");
    response="";

  state0=digitalRead(IR0);
  state1=digitalRead(IR1);
  state2=digitalRead(IR2);
  state3=digitalRead(IR3);
  state4=digitalRead(IR4);
  state5=digitalRead(IR5);
if(state0==HIGH||state1==HIGH||state2==HIGH||state3==HIGH||state4==HIGH||state5==HIGH){
  if(state0==HIGH){
     Serial.println("Slot 1");
  }
  else if(state1==HIGH){
     Serial.println("Slot 2");
    }
  else if(state2==HIGH){
     Serial.println("Slot 3");
    }
  else if(state3==HIGH){
     Serial.println("Slot 4");
    }
  else if(state4==HIGH){
     Serial.println("Slot 5");
    }
    else if(state5==HIGH){
      Serial.println("Slot 6");
    }
  Serial.println("Available");
  // Connect to host
  Serial.print("Connecting to ");
  Serial.println(host);
  // Use WiFiClient class to create TCP connections
  const int httpPort = 8080;
  if (!client.connect(host, httpPort)) {
    Serial.println("Connection failed!");
    return;
  }
  // Create a URL for the request.
  String url = "/nodemcu/6slot/index.php?s0=";
  url += state0;
  url += "&s1=";
  url += state1;
  url += "&s2=";
  url += state2;
  url += "&s3=";
  url += state3;
  url += "&s4=";
  url += state4;
  url += "&s5=";
  url += state5;
  // This will send the request to the server
  Serial.print("Requesting URL: ");
  Serial.println(url);
  client.print(String("GET ") + url + " HTTP/1.1\r\n" + "Host: " + host + "\r\n" + "Connection: close\r\n\r\n");
   while (client.available()) {
    String line = client.readStringUntil('\r');
    Serial.print(line);
  } 
  Serial.println();
  Serial.println("Closing connection");
}
else {
  Serial.println("Slot Not Available");
   delay(1000);
return;
}
      }
    else{
         Serial.println("Card not valid");
               }
 delay(1000);
      }
