# การทดลองที่ 3
## วัตถุประสงค์ของการทดลอง
  1 เพื่อศึกษาการทำงานของ microcontroller Esp-01 
  2 เพื่อให้สามารถเขียนโปรแกรมและรัน microcontroller ที่ต่อกับ adapter และให้มี output ออกมาภายนอกได้
## อุปกรณ์ที่ใช้
  1 microcontroller ESP-01
  2 อุปกรณ์ต่อ USB กับ microcontroller
  3 adapter ที่ต่อกับ microcontroller
  4 LED
## ศึกษาข้อมมูลเบื้องต้น
แหล่งข้อมูล https://www.youtube.com/watch?v=CCnN1WJsXQY
## วิธีทำการทดลอง
  1 นำ adapter ที่มีคอร์ด 0(สีขาว) กับ 1(สีเหลือง) ต่อเข้ากับ USB seriel port และนำ microcontroller มาต่อเข้ากับตัว adapter อีกที
  
  
  ![image](https://user-images.githubusercontent.com/80879942/112137666-1e88bb80-8c03-11eb-866b-b516ad5036b6.jpg)
 
 2 ทำการเขียนโปรแกรม 
    -โปรแกรมทำการเริ่มต้นที่ 0 โดยวนลูปด้วยคำสั่ง delay(500) ซึ่งหมายถึง 500 มิลลิเซค
    -คำสั่ง cnt++ คือการนับเลขไปเรื่อยโดยกำหนดเงื่อนไข if(cnt%2) หมายถึงหากตัวเลขเป็นเลขคี่ ให้ on แต่หากไม่ใช่ก็คือจะเปน off
    
    
    ![image](https://user-images.githubusercontent.com/80879942/112139226-1c276100-8c05-11eb-9b71-6711fb943ae2.jpg)

    -ทำการรันโดยคำสั่ง pio run -t upload
    -กด reset เพื่อทำการอัปโหลดโปรแกรมไปยัง microcontroller
    
    ![image](https://user-images.githubusercontent.com/80879942/112139583-84764280-8c05-11eb-9b73-6768c03b1083.jpg
    
    
    -เมื่ออํปโลหดเสร็จให้ใช้คำสั่ง pio device monitor เพื่อดูผล
    
## การบันทึกผลการทดลอง
   จะได้ผลลัพธ์ออกมาเป็น on off สลับกันไปเรื่อย แล้วไฟ LED เปล่งแสงจะติดดับๆสลับกัน



