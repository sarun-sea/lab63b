# การทดลองที่ 2 เรื่อง การเขียนโปรแกรมค้นหาไวไฟ

# วัตถุปรสงค์
* 1.เพื่อที่จะรันโปรแกรมบนไมโครคอนโทรลเลอร์ ESP-01 ที่จะค้นหา wifi

# อุปกรณ์ที่ใช้
* 1.CPU
* 2.เสาอากาศสำหรับรับไวไฟ
* 3.อุปกรณ์ต่อUSB
* 4.ไมโครคอนโทรลเลอร์ESP-01ที่มีไวไฟในตัวเอง

# ศึกษาข้อมูลเบื้องต้น
* จะใช้ข้อมูลจากplatfromio.ini เพื่อดูข้อมูลไมโครคอนโทรเลอร์ ESP-01
* คลิปการสอนของอาจารย์ https://youtu.be/yBjab0UNuB8

# วิธีการทดลอง
* 1.เสียบไมโครคอนโทรลเลอร์ใน USB to serealพอร์ต
* 2.อัปโหลดโปรแกรมโดยรันคำสั่ง upload
 ![image](https://user-images.githubusercontent.com/80879678/112092429-0c3e5b80-8bca-11eb-9138-49a05fa33128.jpg)
* 3.กดปุ่มอัปโหลด
* 4.กดปุ่มรีเซ็ต
 ![image](https://user-images.githubusercontent.com/80879678/112092578-62ab9a00-8bca-11eb-853f-540fc48be65c.jpg)
* 5.เมื่อuploadครบ100%ใช้คำสั่ง pio device monitor
 ![image](https://user-images.githubusercontent.com/80879678/112092640-8242c280-8bca-11eb-8907-0a1be8c000f2.jpg)
 * โค้ดที่ใช้ในการเขียนโปรแกรม
 
javascript   
#include <Arduino.h>
#include <ESP8266WiFi.h>

int cnt = 0;

void setup()
{
 Serial.begin(115200);
 WiFi.mode(WIFI_STA);
 WiFi.disconnect();
 delay(100);
 Serial.println("\n\n\n");
}

void loop()
{
 Serial.println("========== เริ่มต้นแสกนหา Wifi ===========");
 int n = WiFi.scanNetworks();
 if(n == 0) {
  Serial.println("NO NETWORK FOUND");
 } else {
  for(int i=0; i<n; i++) {
   Serial.print(i + 1);
   Serial.print(": ");
   Serial.print(WiFi.SSID(i));
   Serial.print(" (");
   Serial.print(WiFi.RSSI(i));
   Serial.println(")");
   delay(10);
  }
 }
 Serial.println("\n\n");
}
  

# การบันทึกผล
เมื่ออัปโหลดเสร็จจะมีส่วนset upที่เซ็ตไวไฟให้พร้อมทำงานส่วนลูปคือวนลูปตลอดไป
แสดงผลเริ่มต้นคือ เริ่มต้นสแกนหาwifi
จะมีการค้นหา wifiบริเวณนั้น
![image](https://user-images.githubusercontent.com/80879678/112092782-ca61e500-8bca-11eb-94f7-4198a18f1636.jpg)

# อภิปรายผลการทดลอง
* จากการทดลองสามารถค้นหาwifiที่มีสัญญาณอยู่บริเวณนั้นๆได้
![image](https://user-images.githubusercontent.com/80879678/112092782-ca61e500-8bca-11eb-94f7-4198a18f1636.jpg)

# คำถามหลังการทดลอง
