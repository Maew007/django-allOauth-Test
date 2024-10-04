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
Superuser:admin
pass: test
ใช้เข้าหน้าเว็บดูแลระบบหลังบ้าน หรือสามารถสร้างขึ้นใหม่ได้
สามารถทดสอบการส่ง API  ด้วย ไฟล์ test.rest

ขั้นตอนการทำงานของโปรเจ็คนี้ 
0. ถ้าท่านสามารถติดตั้ง git clone ได้ให้ท่านเข้าไปใช้คำสั่ง
   git clone https://github.com/Maew007/django-allOauth-Test.git
   ท่านจะไม่ต้องทำการแก้ไขไฟล์ใดๆ เลย สามารถ ทำขั้นตอนที่ 1 ต่อไปได้เลย
   $ cd django-allOauth-Test

1.ท่านต้องเข้าไปสร้างตารางและฐานข้อมูลเบื้องต้นไว้ก่อนด้วยคำสั่ง
$python manage.py migrate

2.ทำการสร้างรหัสผู้ใช้งาน สำหรับเข้าไปใช้งาน ที่เป็น Superuser เพื่อใช้เป็นรหัสเข้าใช้ผ่านหน้าเว็บแอดมิน ของ django
$python manage.py createsuperuser
 user: admin
 email: a@AAA.com   สามารถกำหนดตัวหลอกที่ไม่ใช่อีเมลจริงได้
 password: test     กรอกอะไรก็ได้ จากตัวอย่างจะกรอก เป็น test
 re-password: test  กรอกอะไรก็ได้ จากตัวอย่างจะกรอก เป็น test เพราะต้องเหมือนกับด้านบนเพื่อเป็นการยืนยันรหัสผ่าน

3. เกิดเริ่มทำการแก้ไขให้ตรวจสอบว่า
$python manage.py runserver
4. เข้าไปเว็บบราวเซอร์ ไปที่ 127.0.0.1:8000
จะพบหน้า จรวด แสดงขึ้นมา
5. เข้าไปเว็บบราวเซอร์ ไปที่ 127.0.0.1:8000/admin
จะหน้าให้กรอกรหัสผ่านและชื่อผู้ใช้งาน  แสดงขึ้นมา
6. ทำการทดสอบการทำงานตามคลิปต่อไปนี้
เว็บไซด์ที่ใช้สำหรับอ้างอิง และขอขอบคุณ มา ณ โอกาสนี้ (thank you very much !!!!)
https://www.youtube.com/watch?v=llrIu4Qsl7c



เริ่มต้นการแก้ไขไฟล์โครงการด้วยการสร้างขึ้นใหม่โดยไม่ได้ใช้ไฟล์จาก git clone
0. เริ่มสร้างโครงการโดยอัตโนมัติด้วย django admin
   $ django-admin startproject project_backend_oauth_login
   $ cd project_backend_oauth_login
   $ ใช้คำสั่ง  tree ใน linux จะแสดง

1. เข้าไปแก้ไขไฟล์ settings.py ใน โปรเจ็คหลัก ในตัวอย่างนี้ ชื่อ ProjectName จะใช้ชื่อว่า project_backend_oauth_login
    ProjectName ---
                   |->Floder:ProjectName |--> urls.py
                   |                     |--> settings.py ไฟล์ที่ต้องเข้าไปแก้ไข  ****
                   |-> manage.py
                   |-> test.rest
   แก้ไขตำแหน่ง 
   #เพิ่มแอพพลิเคชันสำหรับ rest_framework #1
   -------------------------- code settings.py ---------------------------------------------------
#แก้ไขไฟล์ที่ #1

#จุดที่ 1  แก้ไขคำสั่งเพื่อเรียกใช้งานจากไอพีที่กำหนดให้เครื่องแบบสาธารณะ
#ของเดิม ALLOWED_HOSTS = [] แก้ไขเป็น ALLOWED_HOSTS = ['*']
 
INSTALLED_APPS = [
     'django.contrib.staticfiles',

  ##จุดที่ 2 เพิ่มแอพพลิเคชันสำหรับ rest_framework #1 ต่อท้ายด้านบน
    'rest_framework',
    'rest_framework.authtoken',
]

---------------------------------------------------------------------------------

2. เข้าไปแก้ไขไฟล์ urls.py ใน โปรเจ็คหลัก
   #แก้ไขไฟล์ที่ #2
    ProjectName ---
                   |->Floder:ProjectName |--> urls.py     ไฟล์ที่ต้องเข้าไปแก้ไข ****
                   |                     |--> settings.py 
                   |-> manage.py
                   |-> test.rest
-------------------------- code urls.py ---------------------------------------------------
#แก้ไขไฟล์ที่ #2

from django.contrib import admin
from django.urls import path
from django.urls import re_path
from . import views

urlpatterns = [
    path('admin/', admin.site.urls),
    re_path('signup', views.signup),
    re_path('login', views.login),
    re_path('test_token', views.test_token),
]

---------------------------------------------------------------------------------
3. เข้าไปเพิ่มและแก้ไขไฟล์ views.py ใน โปรเจ็คหลัก
   #แก้ไขไฟล์ที่ #3
    ProjectName ---
                   |->Floder:ProjectName |--> urls.py     
                   |                     |--> settings.py 
                   |                     |--> สร้างใหม่ชื่อไฟล์ views.py ไฟล์ที่ต้องเข้าไปแก้ไข ****
                   |-> manage.py
                   |-> test.rest

--------------------------code views.py ---------------------------------------------------
#แก้ไขไฟล์ที่ #3

from rest_framework.decorators import api_view, authentication_classes, permission_classes
from rest_framework.authentication import SessionAuthentication, TokenAuthentication
from rest_framework.permissions import IsAuthenticated
from rest_framework.response import Response
from rest_framework import status

from django.shortcuts import get_object_or_404
from django.contrib.auth.models import User
from rest_framework.authtoken.models import Token

from .serializers import UserSerializer

@api_view(['POST'])
def signup(request):
    serializer = UserSerializer(data=request.data)
    if serializer.is_valid():
        serializer.save()
        user = User.objects.get(username=request.data['username'])
        user.set_password(request.data['password'])
        user.save()
        token = Token.objects.create(user=user)
        return Response({'token': token.key, 'user': serializer.data})
    return Response(serializer.errors, status=status.HTTP_200_OK)

@api_view(['POST'])
def login(request):
    user = get_object_or_404(User, username=request.data['username'])
    if not user.check_password(request.data['password']):
        return Response("missing user", status=status.HTTP_404_NOT_FOUND)
    token, created = Token.objects.get_or_create(user=user)
    serializer = UserSerializer(user)
    return Response({'token': token.key, 'user': serializer.data})

@api_view(['GET'])
@authentication_classes([SessionAuthentication, TokenAuthentication])
@permission_classes([IsAuthenticated])
def test_token(request):
    return Response("passed!")
    #ขอบเขตข้อมูลที่สามารถเรียกดูได้จะมีดังนี้
    #request.user.id          ความหมาย  ลำดับที่ ข้อมูลที่ถูกบันทึก
    #request.user.username    ความหมาย  ชื่อผู้ใช้งานเป็นภาษาอังกฤษ
    #request.user.password    ความหมาย  รหัสผ่านผู้ใช้งาน
    #request.user.email       ความหมาย  อีเมล์เข้าผู้ใช้งาน

---------------------------------------------------------------------------------

4. เข้าไปเพิ่มและแก้ไขไฟล์ serializers.py ใน โปรเจ็คหลัก
   #แก้ไขไฟล์ที่ #4
    ProjectName ---
                   |->Floder:ProjectName |--> urls.py     
                   |                     |--> settings.py 
                   |                     |--> views.py
                   |                     |--> สร้างใหม่ชื่อไฟล์ serializers.py ไฟล์ที่ต้องเข้าไปแก้ไข ****
                   |-> manage.py
                   |-> test.rest

-------------------------- code serializers.py ---------------------------------------------------
#แก้ไขไฟล์ที่ #4
from rest_framework import serializers
from django.contrib.auth.models import User

class UserSerializer(serializers.ModelSerializer):
    class Meta(object):
        model = User 
        fields = ['id', 'username', 'password', 'email']

---------------------------------------------------------------------------------

 5. เข้าไปเพิ่มและแก้ไขไฟล์ test.rest ใน โปรเจ็คหลัก
   #แก้ไขไฟล์ที่ #5
    ProjectName ---
                   |->Floder:ProjectName |--> urls.py     
                   |                     |--> settings.py 
                   |                     |--> views.py
                   |                     |--> serializers.py 
                   |-> manage.py
                   |-> สร้างใหม่ชื่อไฟล์ test.rest   ไฟล์ที่ต้องเข้าไปแก้ไข ****
-------------------------- code test.rest ---------------------------------------------------
#แก้ไขไฟล์ที่ #5
### หน้านี้สำหรับทดสอบการเชื่อมต่อ rest frame โดยที่ไม่ต้องใช้งาน Postman เพื่อตรวจสอบ api
###
###
POST http://127.0.0.1:8000/signup 
Content-Type: application/json

{ "username": "adam", "password": "Pass1234!", "email": "adam@mail.com" }

###

POST http://127.0.0.1:8000/login 
Content-Type: application/json

{ "username": "adam", "password": "Pass1234!" }

###

GET http://127.0.0.1:8000/test_token 
Content-Type: application/json
Authorization: token 60b70038312c7607b52f1289de99fe99ea7022ff

###
GET http://10.1.2.108:8000/drinks 


###

POST http://10.1.2.108:8000/login/ 
Content-Type: application/json

{ "username": "admin", "password": "test" }


---------------------------------------------------------------------------------