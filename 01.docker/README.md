# เริ่มต้นกับ Docker

Docker เป็นแพลตฟอร์มที่ช่วยให้คุณสามารถสร้าง ส่ง และรันแอปพลิเคชันในคอนเทนเนอร์ได้อย่างง่ายดาย คอนเทนเนอร์เป็นสภาพแวดล้อมที่แยกจากกัน ซึ่งช่วยให้แอปพลิเคชันทำงานได้อย่างสม่ำเสมอในทุกสภาพแวดล้อม

## ข้อมูลพื้นฐาน

ศึกษาการใช้งาน Docker เบื้องต้นได้จากลิงก์ต่อไปนี้:

- [Docker](https://www.youtube.com/watch?v=3c-iBn73dDE) - วิดีโอแนะนำ Docker
- [Docker Compose](https://www.youtube.com/watch?v=SXwC9fSwct8) - วิดีโอแนะนำ Docker Compose

## ทดสอบเมื่อจบการดูวิดีโอ 01

หลังจากดูวิดีโอแนะนำแล้ว ให้ทำตามขั้นตอนดังนี้:

- สร้างตัวอย่างไฟล์ Dockerfile สำหรับแอปพลิเคชันอะไรก็ได้จากที่ได้เรียนรู้ในวิดีโอ จากนั้นทดสอบการสร้างอิมเมจและรันคอนเทนเนอร์ และ push ขึ้น Docker Hub
- สร้างบัญชีผู้ใช้บน [Docker Hub](https://hub.docker.com/) หากยังไม่มี
- สร้างไฟล์ `Dockerfile` สำหรับแอปพลิเคชันที่คุณเลือก
- ใช้คำสั่ง `docker build -t your_dockerhub_username/your_image_name:tag .` เพื่อสร้างอิมเมจ
- ใช้คำสั่ง `docker run -d -p host_port:container_port your_dockerhub_username/your_image_name:tag` เพื่อรันคอนเทนเนอร์
- ใช้คำสั่ง `docker push your_dockerhub_username/your_image_name:tag` เพื่อส่งอิมเมจขึ้น Docker Hub

## ทดสอบเมื่อจบการดูวิดีโอ 02

หลังจากดูวิดีโอแนะนำแล้ว ให้ทำตามขั้นตอนดังนี้:

- ทำ slide สรุปเนื้อหาที่ได้เรียนรู้จากวิดีโอทั้งสอง โดยดูตัวอย่างจากไฟล์ slide.pdf ที่อยู่ใน folder นี้ โดยให้เน้นที่หัวข้อหลัก ๆ ดังนี้
    - Docker คืออะไร
    - ประโยชน์ของการใช้ Docker
    - คอนเทนเนอร์คืออะไร
    - Docker Compose คืออะไร
    - ประโยชน์ของการใช้ Docker Compose
    - พร้อม workshop สั้น ๆ ที่อธิบายการใช้งาน Docker Compose

#### ตัวอย่าง Workshop: การใช้งาน MongoDB กับ Mongo-Express ผ่าน Docker Compose

- สร้างโฟลเดอร์เก็บ dockerfile สำหรับ mongo db และ mongo-express
- สร้างไฟล์ `docker-compose.yml`
- เพิ่ม services mongo db และ mongo-express ลงในไฟล์ `docker-compose.yml`
- รันคำสั่ง `docker-compose up -d` เพื่อเริ่มต้นคอนเทนเนอร์
- เปิดเบราว์เซอร์และไปที่ `http://localhost:8081` เพื่อเข้าถึง mongo-express
- ตรวจสอบว่าคุณสามารถเชื่อมต่อกับฐานข้อมูล MongoDB ได้ผ่าน mongo-express
- เมื่อเสร็จสิ้น ให้รันคำสั่ง `docker-compose down` เพื่อหยุดและลบคอนเทนเนอร์

#### ลิงก์เพิ่มเติม

- [Mongo Express](https://github.com/mongo-express/mongo-express)

---
