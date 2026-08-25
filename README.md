# 412345 Internet Mapping — WebGIS Lab (สัปดาห์ 4 + 6)

Repository นี้ใช้สำหรับติดตั้ง **PostGIS + GeoServer** ผ่าน Docker Compose บน **GitHub Codespaces**
ไม่ต้องติดตั้งอะไรบนเครื่องของนักศึกษาเลย ใช้แค่เบราว์เซอร์

## วิธีใช้งาน

1. กด **Fork** repo นี้ที่มุมขวาบนของหน้านี้ เพื่อคัดลอกเป็นของตัวเอง
2. ใน repo ของตัวเอง กดปุ่มสีเขียว **Code** → แท็บ **Codespaces** → **Create codespace on main**
3. รอสภาพแวดล้อมสร้างเสร็จ (1-2 นาที) จะเห็นหน้าตาเหมือน VS Code ในเบราว์เซอร์
4. เปิด Terminal (เมนู **Terminal → New Terminal**) แล้วรัน:
   ```bash
   docker compose up -d
   ```
5. ตรวจสอบว่าทำงานสำเร็จ:
   ```bash
   docker compose ps
   ```
   ต้องเห็นทั้ง `postgis` และ `geoserver` มีสถานะ `Up`
6. ไปที่แท็บ **PORTS** ด้านล่าง คลิกไอคอนลูกโลกข้างพอร์ต **8080** เพื่อเปิด GeoServer Web Admin
7. เข้าสู่ระบบด้วย `admin` / `geoserver`
8. เมื่อเลิกใช้งาน กลับไปที่ [github.com/codespaces](https://github.com/codespaces) แล้วกด **Stop codespace** ทุกครั้ง เพื่อประหยัดโควตาเวลาฟรี

## ค่าตั้งต้นของระบบ

| รายการ | ค่า |
|---|---|
| PostGIS database | `gisdb` |
| PostGIS password | `postgres` |
| PostGIS port | `5432` |
| GeoServer admin user | `admin` |
| GeoServer admin password | `geoserver` |
| GeoServer port | `8080` |

## เชื่อมต่อ GeoServer กับ PostGIS (สัปดาห์ 6)

เมื่อสร้าง Datastore ใน GeoServer ให้ใส่ host เป็นชื่อ service คือ `postgis` **ไม่ใช่** `localhost`
เพราะทั้งสอง container อยู่ใน network เดียวกันภายใน Docker Compose

## หมายเหตุเรื่องโควตา

GitHub Codespaces ฟรี 60 ชั่วโมง/เดือน (ยืนยัน [GitHub Student Developer Pack](https://education.github.com) เพิ่มเป็น 180 ชั่วโมง)
ระบบจะหยุดอัตโนมัติหลังไม่ใช้งาน 30 นาที แต่ควรกด Stop codespace เองทุกครั้งหลังเลิกใช้งาน
