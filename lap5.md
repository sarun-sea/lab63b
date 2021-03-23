# การทดลองที่ 5
## วัตถุประสงค์
   1. เพื่อศึกษาการเขียนโปรแกรมเพื่อเชื่อมต่อไวไฟและสร้างเว็บเซิฟเวอร์
 
 
 ## อุปกรณ์ที่ใช้
 1. microcontroller EPS-01
 2. USB ที่ต่อเข้ากับ serial
 3. CPU 
 4. wifi ที่ต้องการเชื่อมกับ microcontroller 
   
   
 ## ศึกษาข้อมูลเบื้องต้น
   แหล่งข้อมูล https://www.youtube.com/watch?v=VX-QNQcO-b4
   
   
 ## วิธีการทำการทดลอง
  1. เข้าโปรแกรมไปที่ cd_05wifi-web-server และอธิบายโปรแกรมออกมา จะได้ดังนี้
  
  ```javascript
  #include <ESP8266WiFi.h>
//#include <WiFiClient.h>
#include <ESP8266WebServer.h>

const char* ssid = "HI_BMFWIFI_2.4G";
const char* password = "0819110933";

ESP8266WebServer server(80);

int cnt = 0;

void setup(void){
	Serial.begin(115200);

	WiFi.mode(WIFI_STA);
	WiFi.begin(ssid, password);
	while (WiFi.status() != WL_CONNECTED) {
		delay(500);
		Serial.print(".");
	}
	Serial.print("\n\nIP address: ");
	Serial.println(WiFi.localIP());

	server.onNotFound([]() {
		server.send(404, "text/plain", "Path Not Found");
	});

	server.on("/", []() {
		cnt++;
		String msg = "Hello cnt: ";
		msg += cnt;
		server.send(200, "text/plain", msg);
	});

	server.begin();
	Serial.println("HTTP server started");
}

void loop(void){
  server.handleClient();
}
```

2. ทั้งสองส่วนนี้คือส่วนที่ต้องใส่ wifi ที่ต้องการเชื่อม
  const char* ssid = "HI_BMFWIFI_2.4G";
  const char* password = "0819110933";
  
3. ซึ่งโปรแกรมนี้จะแบ่งเป็นสองส่วนคือส่วน setup เป็นส่วนที่ conect กับ wifi และส่วน setup webserver ที่จะแสดงผลว่า hello cnt โดยจะบวก 1 ไปเรื่อยๆ
4. ทำการ upload โปรแกรมด้วคำสั่ง pio run -t upload ขึ้นไปบนตัว microcontroller 
5. เสียบ microcontroller เข้าไปที่ USB to serial



7. กด reset เพื่อให้ microcontroller พร้อมที่จะรับข้อมูลโปรแกรม
8. กด pio device monitor เพื่อที่ดูผลลัพธ์โดยจะขึ้น ip address และนำไปที่บราวเซอร์ในการทดสอบ

## การบันทึกผลการทดลอง
   จะเห็นว่าากคำสั่ง pio device monitor จะขึ้น ip address มาให้และเมื่อ copy ip address ไปวางที่บราวเซอร์ จะขึ้นคำว่า hello 1 โดยจะเพิ่มตัวเลขไปที่ละ 1 เรื่อยๆ
   
## อภิปรายผลการทดลอง
   จากการทดลองจะเห็นว่าเราสามารถนำ microcontroller มาเชื่อมต่อกับ wifi และทำงานบนเว็บเซิฟเวอร์ได้
   
## คำถามหลังการทดลอง

 
