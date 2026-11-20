# Prompt Builder PWA

สตูดิโอสร้าง Prompt AI เวอร์ชัน Progressive Web App (PWA) ใช้ HTML ไฟล์ล่าสุดที่ผู้ใช้อัปโหลด พร้อมคงชื่อแอปและชุดไอคอนเดิม

## ฟีเจอร์ในเวอร์ชันนี้
- ภาพนิ่ง: เลือกสไตล์ภาพ ขนาด ความคมชัด มุมกล้อง แสง สี และ Negative Prompt
- วิดีโอ: เลือกเสียงบรรยาย น้ำเสียง Caption และแม่แบบบทพูด
- Storyboard: วางแผนเรื่อง กลุ่มเป้าหมาย จุดประสงค์ จำนวนช็อต ภาพ ตัวละคร เสียง และรูปแบบผลลัพธ์
- แต่งเพลง: กำหนดธีม อารมณ์ แนวเพลง จังหวะ นักร้อง เครื่องดนตรี และ Style tags สำหรับ Suno/Udio
- สร้าง Prompt ภาษาอังกฤษและภาษาไทย พร้อมปุ่มคัดลอก
- สลับธีมสว่าง/มืด
- ติดตั้งเป็นแอปบนอุปกรณ์ที่รองรับ และมี Service Worker สำหรับเปิดใช้งานออฟไลน์หลังโหลดครั้งแรก

## ทดลองใช้งานบนเครื่อง
การติดตั้ง PWA และ Service Worker ต้องเปิดผ่าน HTTPS หรือ localhost (เปิดไฟล์ index.html โดยตรงจะไม่เปิดใช้ความสามารถ PWA)

ตัวอย่างใช้ Python:

```bash
python -m http.server 8080
```

จากนั้นเปิด `http://localhost:8080` ในเบราว์เซอร์

## เผยแพร่ด้วย GitHub Pages
1. สร้าง GitHub repository ใหม่ และอัปโหลดไฟล์/โฟลเดอร์ทั้งหมดในชุดนี้ โดยให้ `index.html` อยู่ที่ root ของ repository
2. ไปที่ **Settings → Pages**
3. ในส่วน Build and deployment เลือก **GitHub Actions**
4. Push ไฟล์ไปยัง branch `main` หรือกด workflow `Deploy Prompt Builder to GitHub Pages` ในแท็บ Actions
5. รอ workflow ทำงานสำเร็จ แล้วเปิด URL ที่ GitHub Pages แสดงให้

มี workflow ที่ `.github/workflows/deploy.yml` เตรียมไว้แล้ว

## การติดตั้ง
- **Android / Chrome หรือ Edge:** เปิด URL ของเว็บ แล้วกดปุ่ม “ติดตั้งแอป” หรือเลือก Install app จากเมนูเบราว์เซอร์
- **iPhone / iPad:** เปิด URL ด้วย Safari → Share → Add to Home Screen
- **Desktop:** ใช้ปุ่มติดตั้งหรือไอคอน Install ในแถบที่อยู่ (ขึ้นกับเบราว์เซอร์)

## การใช้งานออฟไลน์และข้อควรทราบ
- ต้องเปิดเว็บออนไลน์อย่างน้อยหนึ่งครั้งเพื่อให้ Service Worker เก็บ App Shell ลง cache
- ไฟล์แอปและไอคอนอยู่ใน cache; Google Fonts ต้องใช้อินเทอร์เน็ตในครั้งแรกและอาจใช้ฟอนต์สำรองเมื่อออฟไลน์
- การอัปเดตเวอร์ชันจะเปลี่ยน cache name ใน `sw.js` เพื่อให้เบราว์เซอร์ดึง App Shell รุ่นใหม่
- การคัดลอกข้อความใช้ Clipboard API ของเบราว์เซอร์ ซึ่งอาจต้องใช้ HTTPS หรือ localhost
- แอปทำงานฝั่งเบราว์เซอร์ ไม่ส่ง prompt ไปเก็บบนเซิร์ฟเวอร์โดยตัวแอปเอง

## โครงสร้างไฟล์

```text
prompt-builder-pwa/
├── index.html
├── manifest.webmanifest
├── sw.js
├── favicon.svg
├── icons/
│   ├── icon-192.png
│   ├── icon-512.png
│   ├── icon-maskable-512.png
│   └── apple-touch-icon.png
├── .nojekyll
├── .gitignore
└── .github/
    └── workflows/
        └── deploy.yml
```
