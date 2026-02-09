# เริ่มต้นกับ Django

เริ่มใช้ Docker กับ Django Restframework อย่างง่ายดาย
[Django Restframework](https://www.django-rest-framework.org/) เป็น framework ยอดนิยมสำหรับการสร้าง API ด้วย Django

## Dockerfile

```
# สร้าง django image
docker build -t django .

# สร้างโฟลเดอร์ source สำหรับเก็บโปรเจค Django
mkdir -p source

# สร้างโปรเจค Django ชื่อ myapi ในโฟลเดอร์ source
docker run --rm --user 1000 -v $(pwd)/source:/app django django-admin startproject myapi .

# รันโปรเจค Django
docker run --rm --user 1000 -v $(pwd)/source:/app -p 8000:8000 --name django-server django python manage.py runserver 0.0.0.0:8000
```

## การใช้งาน

- เปิดเว็บเบราว์เซอร์แล้วเข้าไปที่ [http://localhost:8000](http://localhost:8000) จะเห็นหน้าเริ่มต้นของ Django แสดงขึ้นมา
- ติดตั้ง vscode และลง extension Dev Containers เพื่อช่วยในการพัฒนา Django ภายใน container https://code.visualstudio.com/docs/devcontainers/tutorial
- Attach vscode ไปที่ container django-server ที่รันอยู่
- แก้ไขโค้ดใน vscode แล้วบันทึกไฟล์ จากนั้นรีเฟรชหน้าเว็บเบราว์เซอร์ จะเห็นการเปลี่ยนแปลงที่เกิดขึ้นทันที
- ติดตั้ง python extension ใน vscode เพื่อช่วยในการพัฒนา python และ django https://marketplace.visualstudio.com/items?itemName=ms-python.python
- เริ่มทำตาม [Restframwork Tutorial](https://www.django-rest-framework.org/tutorial/quickstart/)

## การพัฒนาเพิ่มเติม

- จะพบกว่าหลังจากเปิดคู่มือแล้วคำสั่งที่ใช้ในการสร้างไฟล์นั้น ได้ทำการสร้างไป้ในโฟลเดอร์ source แล้ว สามารถแก้ไขโค้ดในโฟลเดอร์ source ได้เลย

## จบการทดลอง

- แสดงผลการทดลองโดยการถ่ายภาพหน้าจอเว็บเบราว์เซอร์ที่แสดงหน้าเริ่มต้นของ Django พร้อมกับโค้ดที่แก้ไขใน vscode
- สามารถเปรียบเทียบความต่าระหว่าง APIView, ModelViewSet และ GenericAPIView ได้
