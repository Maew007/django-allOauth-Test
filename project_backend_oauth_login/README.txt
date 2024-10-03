เว็บไซด์ที่ใช้สำหรับอ้างอิง
https://www.youtube.com/watch?v=llrIu4Qsl7c


Code ตัวอย่าง
https://github.com/alamorre/django-rest-auth

สิ่งที่จำเป็นในการติดตั้ง 
source virsual environment
pip install django 
pip install djangorestframework


ติดตั้ง Extensions เพิ่มเติมให้กับ VS Code
ชื่อ REST Client for Visualstudio โดย Huachao Mao
Superuser:admindb
pass: xxxxxx
ใช้เข้าหน้าเว็บดูแลระบบหลังบ้าน หรือสามารถสร้างขึ้นใหม่ได้
สามารถทดสอบการส่ง API  ด้วย ไฟล์ test.rest


เริ่มต้นโครงการด้วย

1. เข้าไปแก้ไขไฟล์ settings.py ใน โปรเจ็คหลัก
    ProjectName ---
                   |->Floder:ProjectName |--> urls.py
                   |                     |--> settings.py ไฟล์ที่ต้องเข้าไปแก้ไข
                   |-> manage.py
                   |-> test.rest
   แก้ไขตำแหน่ง 
   #เพิ่มแอพพลิเคชันสำหรับ rest_framework #1
   #เพิ่มแอพพลิเคชันสำหรับ rest_framework #2 