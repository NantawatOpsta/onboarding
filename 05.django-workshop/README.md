# Django Workshop

ในเวิร์กช็อปนี้ เราจะเรียนรู้การพัฒนาเว็บแอปพลิเคชันด้วย Django โดยใช้แนวคิด Clean Architecture เพื่อให้โค้ดของเรามีความยืดหยุ่นและง่ายต่อการบำรุงรักษา

![An example image](clean-architect.png)

## เนื้อหาที่จะได้เรียนรู้

- การติดตั้งและตั้งค่า Django
- การสร้างโปรเจกต์และแอปพลิเคชัน Django
- การออกแบบฐานข้อมูลด้วย Django ORM
- การสร้างมุมมอง (Views) และแม่แบบ (Templates)
- การจัดการเส้นทาง (URLs) ใน Django
- การใช้ฟอร์ม (Forms) ใน Django
- การทดสอบแอปพลิเคชัน Django
- การปรับใช้แอปพลิเคชัน Django
- การใช้ Clean Architecture ในการออกแบบแอปพลิเคชัน Django

## โครงสร้างของโปรเจกต์

```
source/
│├── product/
│   ├── migrations/
│   ├── templates/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── usecases.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py
│   └── views.py
│├── shop/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│├── manage.py
└── requirements.txt
```

## จุดประสงค์ของโปรแกรม

จุดประสงค์ของโปรแกรมนี้คือการเรียนรู้การพัฒนาเว็บแอปพลิเคชันด้วย Django โดยใช้แนวคิด Clean Architecture เพื่อให้โค้ดของเรามีความยืดหยุ่นและง่ายต่อการบำรุงรักษา

- สร้างระบบจัดการสินค้า (Product Management System) ที่สามารถเพิ่ม แก้ไข ลบ และแสดงรายการสินค้าได้
