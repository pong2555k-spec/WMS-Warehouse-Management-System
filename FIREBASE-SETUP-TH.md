# 🔥 Firebase Setup Guide (ภาษาไทย)

## ✅ ขั้นตอนตั้งค่า Firebase สำหรับ WMS System

---

## 📋 Step 1: สร้าง Firebase Project

### 1.1 เปิด Firebase Console
```
🔗 https://console.firebase.google.com/
```

### 1.2 สร้าง Project ใหม่
```
1. คลิก "Add project" (ปุ่มสีน้ำเงิน)
2. ใส่ชื่อ: "WMS-Warehouse-System"
3. คลิก "Continue"
4. Google Analytics: ปิด (ไม่บังคับ)
5. คลิก "Create project"
6. รอ 1-2 นาที
```

---

## 🗄️ Step 2: สร้าง Firestore Database

### 2.1 เปิด Firestore
```
Sidebar ซ้าย → Build → Firestore Database
```

### 2.2 สร้าง Database
```
1. คลิก "Create database"
2. Region: asia-southeast1 (Singapore) ✅ แนะนำ
3. Security Rules: "Start in test mode"
4. คลิก "Create"
```

---

## 🔐 Step 3: เปิด Anonymous Authentication

### 3.1 ไปที่ Authentication
```
Build → Authentication
```

### 3.2 ตั้งค่า
```
1. คลิก "Get Started"
2. เลือก "Anonymous"
3. เปิด toggle "Enable"
4. คลิก "Save"
```

---

## 🔑 Step 4: ดึง Firebase Config

### 4.1 ไปที่ Project Settings
```
⚙️ gear icon ขวาบน → Project Settings
```

### 4.2 เลือก General Tab

### 4.3 ล่างจะเห็น "Your apps" - เพิ่ม Web App
```
1. คลิก "</> Web"
2. ชื่อ: "WMS Portal"
3. คลิก "Register app"
4. **Copy config ทั้ง 6 ตัวนี้:**
   - apiKey
   - authDomain
   - projectId
   - storageBucket
   - messagingSenderId
   - appId
```

---

## ✅ Step 5: ตั้งค่า Firestore Rules

### 5.1 เปิด Rules Editor
```
Firestore Database → "Rules" tab
```

### 5.2 Paste Rules นี้
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

### 5.3 Publish
```
คลิก "Publish" ปุ่มสีน้ำเงินขวาล่าง
```

---

## 📝 Step 6: แก้ไข index.html

### 6.1 เปิด index.html ด้วย Text Editor

### 6.2 ค้นหา FIREBASE_CONFIG (บรรทัด ~330)
```
Ctrl+F → พิมพ์ "FIREBASE_CONFIG"
```

### 6.3 แทนที่ config
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

✅ ใหม่ (ใส่ค่าจริงจาก Step 4):
const FIREBASE_CONFIG = {
    apiKey: "AIzaSy_YOUR_ACTUAL_KEY",
    authDomain: "wms-warehouse-12345.firebaseapp.com",
    projectId: "wms-warehouse-12345",
    storageBucket: "wms-warehouse-12345.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abc123"
};
```

### 6.4 บันทึก File
```
Ctrl+S
```

---

## 🧪 Step 7: ทดสอบการทำงาน

### 7.1 บนเครื่องแรก (Machine A)
```
1. เปิดเบราว์เซอร์
2. ไปที่ index.html (Ctrl+O → เลือกไฟล์)
3. ลอกอิน: admin / admin123
4. ตรวจสอบ Header: ต้องเห็น "Cloud Sync Active" ✅
5. เพิ่มสินค้า: Dashboard → "New GR Stock"
6. ตรวจสอบ Firestore Console ว่า data update แล้ว
```

### 7.2 บนเครื่องที่ 2 (Machine B) - พร้อมกัน
```
1. เปิดเบราว์เซอร์อีกเครื่อง
2. ไปที่ index.html เดียวกัน
3. ลอกอิน: admin / admin123
4. ตรวจสอบ Header: "Cloud Sync Active" ✅
5. ไม่ต้อง refresh - ข้อมูล update ทันที! ⚡
```

---

## 🚨 ปัญหา & วิธีแก้

### ❌ "Connected (Local Mode)"
= Firebase Config ยังไม่ตั้งค่า
**วิธีแก้:** ไปที่ Step 6 แก้ไข FIREBASE_CONFIG ให้ถูกต้อง

### ❌ "Cloud Sync Error: permission-denied"
= Firestore Rules ยังไม่ Publish
**วิธีแก้:** 
1. Firestore → Rules
2. Click Publish
3. Reload page (F5)

### ❌ ข้อมูลไม่ sync ระหว่างเครื่อง
**วิธีแก้:**
1. ทั้งสองเครื่องใช้ HTML file เดียวกัน
2. ใช้ Firebase Config เดียวกัน
3. ล้าง localStorage: F12 → Console → `localStorage.clear()`
4. Reload (F5)

---

## ✨ สรุปขั้นตอน (Checklist)

```
☐ สร้าง Firebase Project
☐ สร้าง Firestore Database (Region: asia-southeast1)
☐ เปิด Anonymous Authentication
☐ Copy Firebase Config
☐ Paste config ใน FIREBASE_CONFIG
☐ ตั้ค Firestore Rules
☐ Publish Rules
☐ ทดสอบบนเครื่อง A → "Cloud Sync Active" ✅
☐ ทดสอบบนเครื่อง B → Data auto update ✅
```

---

**🎉 ขอบคุณ! ระบบพร้อมใช้งาน**

สำหรับปัญหาเพิ่มเติม ดู `TROUBLESHOOTING-TH.md`
