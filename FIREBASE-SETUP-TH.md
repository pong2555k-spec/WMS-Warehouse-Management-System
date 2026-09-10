# 🔥 Firebase Setup Guide (ภาษาไทย)

## ✅ ขั้นตอนตั้งค่า Firebase สำหรับ WMS System

---

## 📋 **Step 1: สร้าง Firebase Project**

### 1.1 เปิด Firebase Console
```
🔗 https://console.firebase.google.com/
```

### 1.2 สร้าง Project ใหม่
```
1. คลิก "Add project" (ปุ่มสีน้ำเงิน)
2. ใส่ชื่อ Project: "WMS-Warehouse-System"
3. คลิก "Continue"
4. Google Analytics: ปิด (ไม่บังคับ)
5. คลิก "Create project"
6. รอ 1-2 นาที
```

---

## 🗄️ **Step 2: สร้าง Firestore Database**

### 2.1 เปิด Firestore
```
Sidebar ซ้าย → Build → Firestore Database
```

### 2.2 สร้าง Database
```
1. คลิก "Create database"
2. เลือก Region: 
   ✅ asia-southeast1 (Singapore) ← แนะนำ
   หรือ asia-east1 (Taiwan)
3. Security Rules: "Start in test mode"
4. คลิก "Create"
```

---

## 🔐 **Step 3: เปิด Anonymous Authentication**

### 3.1 ไปที่ Authentication
```
Sidebar → Build → Authentication
```

### 3.2 ตั้งค่า
```
1. คลิก "Get Started"
2. ค้นหา "Anonymous"
3. คลิก "Anonymous"
4. เปิด toggle "Enable"
5. คลิก "Save"
```

---

## 🔑 **Step 4: ดึง Firebase Config**

### 4.1 ไปที่ Project Settings
```
มุมขวาบน → ⚙️ Project Settings
```

### 4.2 ไปที่ General Tab
```
เลือก "General"
```

### 4.3 Add Web App (ถ้ายังไม่มี)
```
1. ล่างจะเห็น "Your apps"
2. คลิก "</> Web" (ไอคอนถัง)
3. ใส่ชื่อ: "WMS Portal"
4. คลิก "Register app"
5. ทำการ Register
```

### 4.4 Copy Config
```
จะเห็น code แบบนี้:

const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "wms-warehouse-xxx.firebaseapp.com",
  projectId: "wms-warehouse-xxx",
  storageBucket: "wms-warehouse-xxx.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};

👉 คัดลอกค่า 6 ตัวนี้
```

---

## ✅ **Step 5: ตั้งค่า Firestore Rules**

### 5.1 เปิด Rules Editor
```
Firestore Database → "Rules" tab
```

### 5.2 ลบ Code เดิม
```
เลือกทั้งหมด → Delete
```

### 5.3 Paste Rules ใหม่
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // ✅ อนุญาต authenticated users ทั้งหมด
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

### 5.4 Publish
```
1. คลิก "Publish" (ปุ่มสีน้ำเงิน ขวาล่าง)
2. ยืนยัน "Publish"
3. รอ 1-2 นาที ✅
```

---

## 📝 **Step 6: แก้ไข index.html File**

### 6.1 เปิด index.html
```
ใช้ Text Editor (VS Code, Notepad++, etc.)
```

### 6.2 ค้นหา FIREBASE_CONFIG
```
กด Ctrl+F → พิมพ์ "FIREBASE_CONFIG"
จะเจอ บรรทัด ~330
```

### 6.3 แทนที่ Config
```javascript
❌ เดิม:
const FIREBASE_CONFIG = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};

✅ ใหม่:
const FIREBASE_CONFIG = {
    apiKey: "AIzaSy_YOUR_ACTUAL_KEY_HERE",
    authDomain: "wms-warehouse-12345.firebaseapp.com",
    projectId: "wms-warehouse-12345",
    storageBucket: "wms-warehouse-12345.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abc123def456"
};
```

### 6.4 บันทึก File
```
Ctrl+S (Save)
```

---

## 🧪 **Step 7: ทดสอบการทำงาน**

### 7.1 บนเครื่องแรก (Machine A)
```
1. เปิดเบราว์เซอร์
2. ไปที่ index.html (Ctrl+O → เลือกไฟล์)
3. ลอกอิน: admin / admin123
4. ตรวจสอบ Header → "Cloud Sync Active" ✅
5. เพิ่มสินค้า (Dashboard → "New GR Stock")
6. ดูข้อมูลใน Firestore Console ✓
```

### 7.2 บนเครื่องที่ 2 (Machine B)
```
1. เปิดเบราว์เซอร์
2. ไปที่ index.html เดียวกัน
3. ลอกอิน: admin / admin123
4. ตรวจสอบ Header → "Cloud Sync Active" ✅
5. ไม่ต้อง refresh - ข้อมูลจะอัพเดต real-time! ⚡
```

---

## 📊 **ตรวจสอบ Firestore Database**

### ดู Real-time Updates
```
1. Firebase Console → Firestore Database → "Data" tab
2. ขยาย:
   artifacts
     └─ wms-warehouse-app
        └─ public
           └─ data
              └─ wms_database
                 └─ main_state

3. จะเห็นข้อมูล: masterItems, inventory, grHistory, giHistory ฯลฯ
4. ลองเพิ่มสินค้าบนเครื่องใดก็ได้
5. Firestore จะอัพเดตทันที ✅
```

---

## 🚨 **ปัญหาที่อาจเจอและวิธีแก้**

### ❌ "Cloud Sync Error: permission-denied"
```
🔧 วิธีแก้:
1. Firestore Database → Rules
2. ตรวจสอบว่า Rules ถูก publish แล้ว
3. ลบ browser cache: Ctrl+Shift+Delete
4. Reload page (F5)
```

### ❌ "Firestore sync error: auth/configuration-not-found"
```
🔧 วิธีแก้:
1. ตรวจสอบ apiKey ไม่มี spaces
2. Anonymous Auth เปิดแล้ว? (Build → Authentication)
3. Copy-paste config ใหม่
4. ตรวจสอบ projectId ตรงกัน
```

### ❌ "Connected (Local Mode)"
```
❌ = Firebase Config ยังไม่ตั้งค่า

🔧 วิธีแก้:
1. ตรวจสอบ FIREBASE_CONFIG ในไฟล์
2. ตรวจสอบว่า apiKey ไม่ขึ้นต้นด้วย "YOUR_"
3. Check browser console (F12)
4. Copy config ใหม่จาก Firebase
```

### ❌ ข้อมูลไม่ sync ระหว่างเครื่อง
```
🔧 วิทธีแก้:
1. ทั้งสองเครื่อง ใช้ HTML file เดียวกัน
2. ใช้ Firebase Config เดียวกัน
3. ลบ localStorage:
   - F12 → Console
   - พิมพ์: localStorage.clear()
   - กด Enter
   - Reload page (F5)
4. ลอกอิน admin ใหม่
```

### ❌ "Your apps" ไม่มีใน Project Settings
```
🔧 วิธีแก้:
1. คลิก "</> Web" icon
2. ใส่ชื่อ app: "WMS Portal"
3. Click "Register app"
4. Config จะแสดงขึ้นมา
```

---

## 📱 **ใช้งานบนอุปกรณ์ต่าง ๆ**

### 🖥️ **PC/Mac**
```
1. บันทึก index.html ลงคอมพิวเตอร์
2. เปิดเบราว์เซอร์
3. Ctrl+O → เลือก index.html
4. ใช้งาน
```

### 📱 **iPhone/iPad**
```
1. Airdrop file ถ้า Mac
2. หรือ iCloud Drive → ดาวน์โหลด
3. Files app → เปิด HTML ด้วย Safari
4. Bookmark ไว้
```

### 🤖 **Android**
```
1. Upload ไป Google Drive
2. เปิด Drive → เปิด HTML (Chrome)
3. หรือ Download แล้วเปิดด้วย Chrome
```

### 🌐 **Web Server (แนะนำ)**
```
💡 ถ้าต้องการให้คนหลายคนเข้าถึง:

1. Firebase Hosting (ฟรี ✅):
   - npm install -g firebase-tools
   - firebase login
   - firebase init hosting
   - firebase deploy
   - ได้ URL: https://wms-warehouse-xxx.web.app

2. GitHub Pages (ฟรี ✅):
   - Push file ขึ้น GitHub
   - Settings → Pages
   - ได้ URL: https://username.github.io/wms
```

---

## ✨ **สรุปขั้นตอน (Quick Checklist)**

```
☐ สร้าง Firebase Project
☐ สร้าง Firestore Database (Region: asia-southeast1)
☐ เปิด Anonymous Authentication
☐ Copy Firebase Config
☐ Paste config ลง FIREBASE_CONFIG ใน HTML
☐ ตั้ค Firestore Rules
☐ Publish Rules
☐ ทดสอบบนเครื่องแรก → "Cloud Sync Active" ✅
☐ ทดสอบบนเครื่องที่ 2 → Data auto update ✅
```

---

## 🎉 **สำเร็จ!**

ตอนนี้คุณมีระบบ WMS ที่สามารถซิงค์ข้อมูลแบบ real-time ระหว่างเครื่องต่าง ๆ ได้แล้ว! 🎊

---

**Need Help?** → ดู TROUBLESHOOTING-TH.md