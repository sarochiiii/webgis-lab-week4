# 412345 Internet Mapping — WebGIS Lab 
Repository นี้ใช้สำหรับติดตั้ง PostGIS + GeoServer ผ่าน Docker Compose บน GitHub Codespaces
ไม่ต้องติดตั้งอะไรบนเครื่องของนักศึกษาเลย ใช้แค่เบราว์เซอร์

## วิธีใช้งาน

1. กด Fork repo นี้ที่มุมขวาบนของหน้านี้ เพื่อคัดลอกเป็นของตัวเอง
2. ใน repo ของตัวเอง กดปุ่มสีเขียว Code แท็บ Codespaces Create codespace on main
3. รอสภาพแวดล้อมสร้างเสร็จ (1-2 นาที)
4. เปิด Terminal (Terminal New Terminal) แล้วรัน `docker compose up -d`
5. ตรวจสอบด้วย `docker compose ps` ต้องเห็น postgis และ geoserver สถานะ Up
6. ไปที่แท็บ PORTS คลิกไอคอนลูกโลกข้างพอร์ต 8080
7. เติม /geoserver/web ต่อท้าย URL ถ้าเจอหน้า 404
8. เข้าสู่ระบบด้วย admin / geoserver
9. เมื่อเลิกใช้งาน กด Stop codespace ที่ github.com/codespaces

## ค่าตั้งต้นของระบบ

- PostGIS database: gisdb, password: postgres, port: 5432
- GeoServer admin: admin / geoserver, port: 8080

## เชื่อมต่อ GeoServer กับ PostGIS

ใส่ host เป็นชื่อ service คือ postgis ไม่ใช่ localhost
