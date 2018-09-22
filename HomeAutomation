#include <ESP8266WiFi.h>

const char* ssid = "hotspot";
const char* password = "naman1234";
 
//int ledPin = 13; // GPIO13
WiFiServer server(88);

String readStrings = "";

int pin1 = 14; // GPIO 14 (D5)
int pin2 = 12; // GPIO 12 (D6)
int pin3 = 13; // GPIO 13 (D7)
int pin4 = 15; // GPIO 15 (D8)

void setup() {
  Serial.begin(115200);
  delay(10);

  pinMode(pin1, OUTPUT); //pin1 output
  pinMode(pin2, OUTPUT); //pin2 output
  pinMode(pin3, OUTPUT); //pin3 output
  pinMode(pin4, OUTPUT); //pin4 output

  // Connect to WiFi network
  Serial.println();
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

  // Start the server
  server.begin();
  Serial.println("Server started");

  // Print the IP address
  Serial.println(WiFi.localIP());

}

void loop() {
  
  WiFiClient client = server.available();

  if (client) {
    Serial.println("Yes client");

    while (client.connected()) {
      if (client.available()) {
        char c = client.read();


        if (readStrings.length() < 100) {
          readStrings += c;
        }

        if (c == '\n') {
          Serial.println(readStrings);
          client.print("HTTP/1.1 200 OK\r\n"); //send new page
          client.print("Content-Type: text/html\r\n\r\n");
          client.print("<!DOCTYPE HTML>\r\n");
          client.print("<HTML>\r\n");//html tag
          client.print("<HEAD>\r\n"); //
          //            client.print("<meta http-equiv='refresh' content='10'/>\r\n");
          client.print("<meta name='apple-mobile-web-app-capable' content='yes' />\r\n");
          client.print("<meta name='apple-mobile-web-app-status-bar-style' content='black-translucent' />\r\n");
          client.print("<link rel='stylesheet' type='text/css' href='http://slumberjer.com/hanis.css' />\r\n");
          client.print("<TITLE>Home Automation</TITLE>\r\n");
          client.print("</HEAD>\r\n");
          client.print("<BODY style='background-color:#ff6666;'>\r\n");
          client.print("<H1>My Smart Home System</H1>\r\n");
          client.print("<hr />\r\n");
          client.print("<br />\r\n");
          client.print("<H2>CODEUTSAVA 2.0</H2>\r\n");
          client.print("<br />\r\n");
          client.print("<p><b>BULB 1</b></p><br />\r\n");
          client.print("<a href=\"/?button1on\"><font color = \"green\">ON   </font></a>\r\n");
          client.print("<a href=\"/?button1off\"><font color = \"red\">OFF  </font></a><br />\r\n");
          client.print("<p><b>BULB 2</b></p>");
          client.print("<br />\r\n");
          client.print("<a href=\"/?button2on\"><font color = \"green\">ON   </font></a>\r\n");
          client.print("<a href=\"/?button2off\"><font color = \"red\">OFF  </font></a><br />\r\n");
          client.print("<p><b>LED 1</b></p>");
          client.print("<br />\r\n");
          client.print("<a href=\"/?button3off\"><font color = \"green\">ON   </font></a>\r\n");
          client.print("<a href=\"/?button3on\"><font color = \"red\">OFF  </font></a><br />\r\n");
          client.print("<p><b>LED 2</b></p>");
          client.print("<br />\r\n");
          client.print("<a href=\"/?button4off\"><font color = \"green\">ON   </font></a>\r\n");
          client.print("<a href=\"/?button4on\"><font color = \"red\">OFF  </font></a><br />\r\n");
          client.print("<br />\r\n");
          client.print("<p><b>All Switches</b></p>");
          client.print("<br />\r\n");
          client.print("<br />\r\n");
          client.print("<a href=\"/?buttonallon\"><font color = \"green\">ALL ON   </font></a>\r\n");
          client.print("<a href=\"/?buttonalloff\"><font color = \"red\">ALL OFF  </font></a><br />\r\n");
          client.print("<br />\r\n");
          client.print("</BODY>\r\n");
          client.print("</HTML>\n");

          delay(1);

          client.stop();
          if (readStrings.indexOf("?button1on") > 0) {
            Serial.println("1 on");
            digitalWrite(pin1, LOW);
          }
          if (readStrings.indexOf("?button1off") > 0) {
            Serial.println("1 off");
            digitalWrite(pin1, HIGH);
          }

          if (readStrings.indexOf("?button2on") > 0) {
            Serial.println("2 on");
            digitalWrite(pin2, LOW);
          }
          if (readStrings.indexOf("?button2off") > 0) {
            Serial.println("2 off");
            digitalWrite(pin2, HIGH);
          }
          if (readStrings.indexOf("?button3on") > 0) {
            digitalWrite(pin3, LOW);
            Serial.println("3 on");
          }
          if (readStrings.indexOf("?button3off") > 0) {
            digitalWrite(pin3, HIGH);
            Serial.println("3 off");
          }
          if (readStrings.indexOf("?button4on") > 0) {
            digitalWrite(pin4, LOW);
            Serial.println("4 on");
          }
          if (readStrings.indexOf("?button4off") > 0) {
            digitalWrite(pin4, HIGH);
            Serial.println("4 off");
          }
          if (readStrings.indexOf("?buttonallon") > 0) {
            digitalWrite(pin1, LOW);
            digitalWrite(pin2, LOW);
            digitalWrite(pin3, HIGH);
            digitalWrite(pin4, HIGH);
          }
          if (readStrings.indexOf("?buttonalloff") > 0) {
            digitalWrite(pin1, HIGH);
            digitalWrite(pin2, HIGH);
            digitalWrite(pin3, LOW);
            digitalWrite(pin4, LOW);
          }
          readStrings = "";
        }
      }
    }
  }
}
