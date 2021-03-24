# การทดลองที่ 6 เรื่อง การเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์(Wifi AP)

# วัตถุประสงค์
เพื่อเขียนโปรมแกรมที่จะสร้าไวไฟแอคเซสพอยต์ขึ้นมาเองที่จะสามารถนำไวไฟของตัวเองเชื่อมกับอุปกรณือื่น

# อุปกรณ์ที่ใช้
* 1.CPU
* 2.อุปกรณ์ต่อUSB
* 3.ไมโครคอนโทรเลอร์ESP-01

# ศึกษาข้อมูลเบื้องต้น
* platformio.ini
* https://youtu.be/APdBR37Ukxg

# วิธีการทำการทดลอง
* 1.กำหนดชื่อและตั้งพาสเวิด
 ![image](https://user-images.githubusercontent.com/80879678/112093962-ea92a380-8bcc-11eb-8b5d-9c367a3b9449.jpg)

* 2.กำหนดIPAdress,gateway,subnet
![image](https://user-images.githubusercontent.com/80879678/112094552-13676880-8bce-11eb-840f-558fcd636b35.jpg)

* 3.เตรียมเว็บเซิฟเวอร์1ตัว
 ![image](https://user-images.githubusercontent.com/80879678/112094082-32192f80-8bcd-11eb-9905-b37362433e7a.jpg)

* 4.รันคำสั่งsoftAPแล้วกำหนดssiadกับpassword
 ![image](https://user-images.githubusercontent.com/80879678/112094155-537a1b80-8bcd-11eb-9f3f-7429cc1003ca.jpg)
* 5.อัปโหลดโปรแกรมโดยใช้คำสั่งpio run -t upload
![image](https://user-images.githubusercontent.com/80879678/112094212-6ee52680-8bcd-11eb-963f-b78ec3414b97.jpg)
* 6.กดปุ่มรีเซ็ต
 ![image](https://user-images.githubusercontent.com/80879678/112094256-88866e00-8bcd-11eb-8bab-dc64b6cff485.jpg)

* 7.เช็คว่าไวไฟที่สร้างขึ้นนั้นมีจริงมั้ยโดยใช้คำสั่งpio device monitor
 ![image](https://user-images.githubusercontent.com/80879678/112094298-9cca6b00-8bcd-11eb-84ab-2dc865285aca.jpg)
* 8.ใช็โทรศัพท์มือถือค้นหาไวไฟ
* โค้ดที่ใช้ในการเขียนโปรแกรมคือ
```javascript
#include <ESP8266WiFi.h>
//#include <WiFiClient.h>
#include <ESP8266WebServer.h>

const char* ssid = "MY-ESP8266";
const char* password = "choompol";

IPAddress local_ip(192, 168, 1, 1);
IPAddress gateway(192, 168, 1, 1);
IPAddress subnet(255, 255, 255, 0);

ESP8266WebServer server(80);

int cnt = 0;

void setup(void){
 Serial.begin(115200);

 WiFi.softAP(ssid, password);
 WiFi.softAPConfig(local_ip, gateway, subnet);
 delay(100);

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
# การบันทึกผลการทดลอง
สามารถสร้างไวไฟแอคเซสพอยต์ขึ้นมาเองได้ โดยทดลองค้นหาด้วยโทรศัพท์แล้วว่ามีจริง
![image](https://user-images.githubusercontent.com/80879678/112094339-ad7ae100-8bcd-11eb-98da-a0eb09f63ef6.jpg) 

# อภิปรายผลการทดลอง
จากการทดลองนี้เราเขียนโปรแกรมเพื่อที่จะให้ไมโครคอนโทรเลอร์สามารถปล่อยไวไฟจากตัวมันเองออกมาได้และสามารถเชื่อมต่อกับอุปกรณ์อื่น
# คำถามหลังการทดลอง
microcontroller นี้มีลักษณะคล้ายกับอุปกรณ์อิเล็กทรอนิกส์ใด
-  ตอบ เราเตอร์กระจายสัญญาณ wifi
