# การทดลองที่ 3
## วัตถุประสงค์ของการทดลอง
  *1 เพื่อศึกษาการทำงานของ microcontroller Esp-01 
  *2 เพื่อให้สามารถเขียนโปรแกรมและรัน microcontroller ที่ต่อกับ adapter และให้มี output ออกมาภายนอกได้
  *3 เพื่อศึกษาหน้าที่ของ Relay
## อุปกรณ์ที่ใช้
  1 microcontroller ESP-01
  2 อุปกรณ์ต่อ USB กับ microcontroller
  3 adapter ที่ต่อกับ microcontroller
  4 LED
  5 Relay
## ศึกษาข้อมมูลเบื้องต้น
แหล่งข้อมูล https://www.youtube.com/watch?v=CCnN1WJsXQY
          https://www.youtube.com/watch?v=6JnhaUILGuw
## วิธีทำการทดลอง
  1 นำ adapter ที่มีคอร์ด 0(สีขาว) กับ 1(สีเหลือง) ต่อเข้ากับ USB seriel port และนำ microcontroller มาต่อเข้ากับตัว adapter อีกที
  
  
  ![image](https://user-images.githubusercontent.com/80879942/112137666-1e88bb80-8c03-11eb-866b-b516ad5036b6.jpg)
 
 2 ทำการเขียนโปรแกรม 
 ```javascript
 #include <Arduino.h>
#include <ESP8266WiFi.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
	pinMode(0, OUTPUT);
	Serial.println("\n\n\n");
}

void loop()
{
	cnt++;
	if(cnt % 2) {
		Serial.println("========== ON ===========");
		digitalWrite(0, HIGH);
	} else {
		Serial.println("========== OFF ===========");
		digitalWrite(0, LOW);
	}
	delay(500);
}
```
    
   -โปรแกรมทำการเริ่มต้นที่ 0 โดยวนลูปด้วยคำสั่ง delay(500) ซึ่งหมายถึง 500 มิลลิเซค
    -คำสั่ง cnt++ คือการนับเลขไปเรื่อยโดยกำหนดเงื่อนไข if(cnt%2) หมายถึงหากตัวเลขเป็นเลขคี่ ให้ on แต่หากไม่ใช่ก็คือจะเปน off
    
    
  ![image](https://user-images.githubusercontent.com/80879942/112139226-1c276100-8c05-11eb-9b71-6711fb943ae2.jpg)

   -ทำการรันโดยคำสั่ง pio run -t upload
   -กด reset เพื่อทำการอัปโหลดโปรแกรมไปยัง microcontroller จะได้หน้าต่างที่มีกำลัง upload ตามรูป
    
   ![image](https://user-images.githubusercontent.com/80879942/112140260-5e9d6d80-8c06-11eb-9a5d-70b1e3322553.jpg)

    
   -เมื่อัปโลหดเสร็จให้ใช้คำสั่ง pio device monitor เพื่อดูผล
   
   
   -หลังจากเกิดผลแล้วนำ microcontroller มาต่อเข้ากับตัว Relay เพื่อให้ตัวรีเลย์ทำหน้าที่เปิด-ปิดสวิตซ์ แล้วนำแหล่งจ่ายไฟมาต่อเข้ากับตัว Relay เพื่อจ่ายไฟให้รีเลย์ทำงานได้
   
   
  
   
 ## การบันทึกผลการทดลอง
   จะได้ผลลัพธ์ออกมาเป็น on off สลับกันไปเรื่อย แล้วไฟ LED เปล่งแสงสีเขียวจะติดดับๆสลับกัน แต่ไฟสีน้ำเงินจะไม่ติด  
   
   
   ![image](https://user-images.githubusercontent.com/80879942/112142078-ba68f600-8c08-11eb-97b0-456029f00641.jpg)
   
   
   เมื่อนำ microcontroller มาต่อกับตัว Relay จะทำให้รีเลย์เปิด-ปิด สวิตซ์ ตามรูปดังนี้
   
   
   ![image](https://user-images.githubusercontent.com/80879942/112144123-5eec3780-8c0b-11eb-94d0-840e7917e15a.jpg)
   
   
   
 ## อภิปรายผลการทดลอง
   - การทดลองนี้จะอธิบายถึงวิธีการ ประโยชน์ ของการใช้อุปกรณ์ของตัว adepter ที่ต่อกับ microcontroller และ Realy ที่ต่อกับตัว microcontroller ซึ่งการต่อทั้งสองแบบนี้จะสามารถทำให้เกิด output ของโปรแกรมที่เกิดจาก microcontroller ESP-01 ให้เห็นภาพชัดเจนยิ่งขึ้น โดยการต่อกับ Relay ที่จะทำให้เกิดสวิตซ์เปิด-ปิด สามารถนำไปใช้เกี่ยวกับเครื่องใช้ไฟฟ้าภายในบ้านได้หลายอย่าง
 
 
 ## คำถามหลังการทดลอง
   - หากทำการเปลี่ยน delay ให้มากกว่าเดิมจะเกิดอะไรขึ้น
   * ตอบ จะทำให้ระยะห่างของเวลาในการติดดับของไฟมากขึ้น
   
   
   



