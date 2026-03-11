# 🏠 PropVal Pro v2.0
### ระบบประเมินมูลค่าอสังหาริมทรัพย์ — AssetX Estate Co., Ltd.

![PropVal Pro](https://img.shields.io/badge/PropVal_Pro-v2.0-c9a84c?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAzMiAzMiI+PHJlY3Qgd2lkdGg9IjMyIiBoZWlnaHQ9IjMyIiByeD0iNiIgZmlsbD0iIzBkMTQyMiIvPjx0ZXh0IHg9IjE2IiB5PSIyMiIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxOCIgZm9udC1mYW1pbHk9InNlcmlmIiBmaWxsPSIjYzlhODRjIj5BPC90ZXh0Pjwvc3ZnPg==)
![React](https://img.shields.io/badge/React-18-61dafb?style=for-the-badge&logo=react)
![Vite](https://img.shields.io/badge/Vite-5-646cff?style=for-the-badge&logo=vite)
![Vercel](https://img.shields.io/badge/Deploy-Vercel-000?style=for-the-badge&logo=vercel)

---

## 📋 เกี่ยวกับระบบ

PropVal Pro เป็นระบบประเมินมูลค่าอสังหาริมทรัพย์แบบครบวงจร พัฒนาสำหรับ **AssetX Estate Co., Ltd.** รองรับการประเมินทรัพย์เพื่องานขายฝาก จำนอง และซื้อขายทุกประเภท พร้อมบันทึกประวัติและเชื่อมต่อ Google Sheets อัตโนมัติ

---

## ✨ ฟีเจอร์หลัก

| ฟีเจอร์ | รายละเอียด |
|---|---|
| 🔖 **ประเภทการประเมิน** | ขายฝาก / จำนอง / ซื้อขาย / สินเชื่อ / ประเมินมูลค่า |
| 🏠 **ประเภทอสังหาฯ** | 7 กลุ่มหลัก 27 ประเภทย่อย ครอบคลุมทุกรูปแบบ |
| 📊 **คำนวณราคาตลาด** | อิง Zone Multiplier / ผังเมือง / สภาพถม / Comparable |
| ⚠️ **Property Score** | ประเมินความเสี่ยง 8 ปัจจัย คะแนน 0–100 |
| 💰 **วงเงินแนะนำ** | FSV Discount + LTV Rate คำนวณอัตโนมัติ |
| 💾 **บันทึกประวัติ** | Persistent Storage ดูย้อนหลังได้ทุกรายการ |
| 📤 **Google Sheets** | บันทึกข้อมูล 23 คอลัมน์ลง Google Sheet อัตโนมัติ |
| 📄 **Export PDF** | พิมพ์รายงานส่งนายทุนได้ทันที |
| ⬇️ **Export CSV** | ดาวน์โหลดประวัติทั้งหมดเป็น CSV |
| ⏱️ **Real-time Clock** | แสดงวันที่และเวลาจริงใน Header |
| 📱 **Responsive** | รองรับมือถือ แท็บเล็ต และคอมพิวเตอร์ |

---

## 🗂️ โครงสร้างโปรเจกต์

```
propval-vercel/
├── public/
│   └── favicon.svg          # ไอคอนเว็บ
├── src/
│   ├── App.jsx              # ตัวแอปหลักทั้งหมด
│   └── main.jsx             # Entry point
├── index.html               # HTML template
├── package.json             # Dependencies
├── vite.config.js           # Vite configuration
├── vercel.json              # Vercel deploy config
├── .gitignore
└── README.md
```

---

## 🚀 วิธีติดตั้งและรันในเครื่อง

### ความต้องการของระบบ
- Node.js v18 ขึ้นไป
- npm v9 ขึ้นไป

### ขั้นตอน

```bash
# 1. Clone repository
git clone https://github.com/YOUR_USERNAME/propval-pro.git
cd propval-pro

# 2. ติดตั้ง dependencies
npm install

# 3. รันในโหมด development
npm run dev
```

เปิดเบราว์เซอร์ไปที่ `http://localhost:5173`

```bash
# Build สำหรับ production
npm run build

# Preview production build
npm run preview
```

---

## ☁️ Deploy บน Vercel

### วิธีที่ 1 — เชื่อมกับ GitHub (แนะนำ)

1. Push โค้ดขึ้น GitHub
2. ไปที่ [vercel.com](https://vercel.com) → **Add New Project**
3. เลือก **Import Git Repository** → เลือก Repo นี้
4. Vercel ตรวจจับ Vite อัตโนมัติ → กด **Deploy**
5. ✅ ทุกครั้งที่ `git push` เว็บอัปเดตอัตโนมัติ

### วิธีที่ 2 — อัปโหลด ZIP

1. รัน `npm run build` → ได้โฟลเดอร์ `dist/`
2. ไปที่ Vercel → **Deploy** → ลาก folder `dist/` วาง

---

## 📊 การเชื่อมต่อ Google Sheets

### ขั้นตอนตั้งค่า (ทำครั้งเดียว)

**1. สร้าง Google Sheet ใหม่**

**2. เปิด Apps Script**
ไปที่ Extensions → Apps Script → วางโค้ดนี้:

```javascript
function doPost(e) {
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  const sh = ss.getActiveSheet();
  const d = JSON.parse(e.postData.contents);

  // สร้าง Header อัตโนมัติถ้ายังไม่มี
  if (sh.getLastRow() === 0) {
    sh.appendRow([
      "วันที่", "ประเภทประเมิน", "ประเภทอสังหาฯ", "ชื่อทรัพย์",
      "โฉนด", "ตำบล", "อำเภอ", "จังหวัด", "เนื้อที่(ตรว)",
      "ราคารัฐ/ตรว", "มูลค่ารัฐ", "ราคาตลาด/ตรว", "มูลค่าตลาด",
      "FSV", "LTV%", "วงเงิน", "Score", "ความเสี่ยง",
      "ทำเล", "ผังเมือง", "สภาพถม", "ผู้ประเมิน", "หมายเหตุ"
    ]);
  }
  sh.appendRow(d.row);

  return ContentService
    .createTextOutput(JSON.stringify({ status: "ok" }))
    .setMimeType(ContentService.MimeType.JSON);
}

function doGet(e) {
  return ContentService.createTextOutput("PropVal Pro - Ready");
}
```

**3. Deploy Web App**
- กด **Deploy** → New Deployment → Web App
- Execute as: **Me**
- Who has access: **Anyone**
- Copy **Web App URL**

**4. วาง URL ในแอป**
เปิดแอป → แท็บ **⚙️ ตั้งค่า** → วาง URL → กด **บันทึก**

---

## 🧮 สูตรคำนวณ

```
ราคาตลาด/ตรว. = ราคาประเมินรัฐ × Zone Mult × Zoning Mult × (1 + Road% + Frontage% + Fill%)

FSV            = ราคาตลาด × 0.65–0.80  (ขึ้นกับ Risk Score)

วงเงินแนะนำ   = FSV × LTV%
```

### Zone Multipliers

| ทำเล | ตัวคูณ |
|---|---|
| ติดถนนใหญ่ 4 เลน+ | ×2.4 |
| ใกล้ถนนใหญ่ < 500 ม. | ×1.8 |
| ซอยรอง ใกล้ชุมชน | ×1.4 |
| ในซอย / เลียบคลอง | ×1.1 |
| ซอยลึก / ห่างถนนใหญ่ | ×0.85 |

### FSV Discount

| Risk Score | Discount |
|---|---|
| 0–19 คะแนน | 80% |
| 20–39 คะแนน | 75% |
| 40+ คะแนน | 65% |

---

## 🌿 Git Workflow แนะนำ

```bash
# พัฒนาฟีเจอร์ใหม่
git checkout -b feature/ชื่อฟีเจอร์
# ... แก้โค้ด ...
git add .
git commit -m "feat: เพิ่ม..."
git push origin feature/ชื่อฟีเจอร์

# Merge เข้า main เมื่อพร้อม
git checkout main
git merge feature/ชื่อฟีเจอร์
git push origin main
# ✅ Vercel auto-deploy ทันที
```

---

## 📱 Screenshots

| หน้าประเมิน | ประวัติ | ตั้งค่า Google Sheet |
|---|---|---|
| Step 1–4 กรอกข้อมูลทีละขั้น | ตารางรายการทั้งหมด + Export CSV | วิธีตั้งค่า Apps Script |

---

## 🛠️ Tech Stack

- **Frontend**: React 18 + Hooks
- **Build Tool**: Vite 5
- **Styling**: Inline CSS + CSS Variables
- **Storage**: Window Storage API (Persistent)
- **Fonts**: Sarabun (Thai) + IBM Plex Mono
- **Deploy**: Vercel
- **Integration**: Google Apps Script (Sheets Webhook)

---

## 📄 License

Private — AssetX Estate Co., Ltd. © 2025  
พัฒนาสำหรับใช้งานภายในองค์กรเท่านั้น

---

<div align="center">
  <strong>AssetX Estate Co., Ltd.</strong><br/>
  ขายฝาก • จำนอง • นายหน้าอสังหาริมทรัพย์
</div>
