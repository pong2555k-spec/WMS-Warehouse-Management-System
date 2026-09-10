# 🔧 Troubleshooting Guide (ภาษาไทย)

## ❌ ปัญหาที่พบบ่อยและวิธีแก้

---

## 1️⃣ **Header แสดง "Connecting Sync..." ติดค้าง**

### 🔴 Problem
```
Header ขวาบน:
🟡 Connecting Sync...
(ไม่เปลี่ยนเป็น "Cloud Sync Active")
```

### ✅ Solutions

#### วิธี A: ตรวจสอบ Firebase Config
```
1. เปิด index.html ด้วย Text Editor
2. Ctrl+F → ค้นหา "FIREBASE_CONFIG"
3. ตรวจสอบ:
   ✓ apiKey มีค่า (ไม่ว่าง)
   ✓ projectId ถูกต้อง
   ✓ authDomain มี firebaseapp.com
   ✓ ไม่มี "YOUR_" เหลืออยู่
4. Save & Reload
```

#### วิธี B: ตรวจสอบ Anonymous Auth
```
Firebase Console:
1. Build → Authentication
2. Sign-in method → Anonymous
3. ✓ Enable toggle เปิดอยู่
4. Save
```

#### วิธี C: ตรวจสอบ Firestore Rules
```
Firebase Console:
1. Firestore Database → Rules
2. ตรวจสอบ:
   - allow read, write: if request.auth != null;
   ✓ Publish แล้ว (ไม่ได้ pending)
3. รอ 1-2 นาที
```

#### วิธี D: Clear Browser Cache
```
1. Ctrl+Shift+Delete (Clear browsing data)
2. เลือก "All time"
3. Check "Cookies and other site data"
4. Check "Cached images and files"
5. Clear data
6. Reload page (F5)
```

#### วิธี E: Check Browser Console
```
1. F12 → Console tab
2. มีข้อความแดง/สีส้ม?
3. ถ่ายรูป error message
4. ตรวจสอบ error ด้านล่าง
```

---

## 2️⃣ **"Cloud Sync Error: permission-denied"**

### 🔴 Problem
```
Header:
🔴 Sync Error: permission-denied

Browser Console:
error: FirebaseError: Missing or insufficient permissions
```

### ✅ Solutions

#### วิธี A: Publish Firestore Rules
```
Firebase Console:
1. Firestore Database → Rules tab
2. ดู status: "Published" หรือ "Draft"?
3. ถ้า Draft:
   - คลิก "Publish" ด้านล่าง
   - ยืนยัน "Publish"
4. รอ 1-2 นาที
```

#### วิธี B: ตรวจสอบ Rules Syntax
```
Rules ควรมี:
allow read, write: if request.auth != null;

ทั้ง 3 ส่วน:
✓ read
✓ write  
✓ request.auth != null (ต้องมี user)
```

#### วิธี C: Reset Rules
```
1. Firebase Console → Firestore → Rules
2. ลบทั้งหมด
3. Paste rules จาก firestore-rules.txt
4. Publish
5. Reload page
```

---

## 3️⃣ **"Connected (Local Mode)" - ไม่ sync ระหว่างเครื่อง**

### 🔴 Problem
```
Header:
🟡 Connected (Local Mode)

= Firebase Config ยังไม่ถูกตั้งค่า
= Data จะเก็บใน localStorage เท่านั้น
= ไม่ sync ไปยังเครื่องอื่น
```

### ✅ Solutions

#### วิธี A: ตรวจสอบ API Key
```
1. Text Editor → เปิด index.html
2. ค้นหา "FIREBASE_CONFIG"
3. ตรวจสอบ apiKey:
   ❌ "YOUR_API_KEY" (ยังไม่แก้)
   ✅ "AIzaSy..." (ถูกแล้ว)
4. ถ้ายังไม่แก้:
   - ไปที่ Firebase Console
   - Project Settings → General
   - Copy firebaseConfig
   - Paste ไป index.html
```

#### วิธี B: Copy Config ใหม่
```
ถ้า config เก่าไม่ใช่:
1. Firebase Console → Project Settings
2. ล่างจะเห็น "Your apps"
3. ถ้าหลายแอพ: ลบแอพเก่า
4. เพิ่มแอพใหม่: </> Web
5. ใส่ชื่อ "WMS Portal"
6. Register
7. Copy config ใหม่
8. Paste ไป index.html
```

#### วิธี C: Reload After Edit
```
1. แก้ไข config ใน index.html
2. บันทึก (Ctrl+S)
3. Reload page (Ctrl+F5 hard refresh)
4. ล้าง Cache (Ctrl+Shift+Delete)
5. Reopen HTML file
```

---

## 4️⃣ **Login ไม่ได้ - "Username หรือ Password ไม่ถูกต้อง"**

### 🔴 Problem
```
พิมพ์ username/password แต่ error
ทั้งที่ username/password ถูกต้อง
```

### ✅ Solutions

#### วิธี A: ตรวจสอบ Username/Password
```
Username ต้อง case-sensitive (ขนาดตัวอักษรสำคัญ)

❌ ผิด: ADMIN, Admin
✅ ถูก: admin (ตัวเล็ก)

Demo Users:
admin / admin123
anyawee.t / 1234
staff01 / 1234
```

#### วิธี B: Clear LocalStorage
```
1. เปิด Browser DevTools (F12)
2. ไปที่ Console tab
3. พิมพ์: localStorage.clear()
4. กด Enter
5. Reload page (F5)
6. ลองลอกอิน
```

#### วิธี C: Reset Demo Data
```
1. ลอกอิน (ลองใช้ username/password ที่ถูก)
2. ถ้ายังติด: ไปที่ Settings (⚙️ icon ซ้ายล่าง)
3. คลิก "Reset" icon
4. ยืนยัน
5. Reload page
6. ลองลอกอิน admin / admin123
```

---

## 5️⃣ **ข้อมูลไม่ sync ระหว่างเครื่อง (Machine A & B)**

### 🔴 Problem
```
Machine A: เพิ่มสินค้า ✅
Machine B: ข้อมูลไม่เปลี่ยน ❌

(ทั้ง 2 เครื่องแสดง "Cloud Sync Active")
```

### ✅ Solutions

#### วิธี A: ตรวจสอบ Firebase Config
```
1. Machine A: เปิด index.html
2. Machine B: เปิด index.html เดียวกัน
3. ตรวจสอบ FIREBASE_CONFIG:
   ✓ projectId เหมือนกันหรือ?
   ✓ apiKey เหมือนกันหรือ?
4. ถ้าไม่เหมือน:
   - Copy config เดียวกัน
   - Paste ไปทั้งสองเครื่อง
```

#### วิธี B: ตรวจสอบ Network
```
1. ทั้งเครื่องต้องมี Internet
2. ลองเปิด google.com ได้หรือ?
3. ถ้าไม่ได้:
   - ตรวจสอบ WiFi/Connection
   - Restart Internet
```

#### วิธี C: Check Firestore Database
```
1. Firebase Console → Firestore → Data
2. ล้าง "artifacts" → "wms-warehouse-app"
3. ดู timestamp ของ data ล่าสุด
4. ลองเพิ่มสินค้าบน Machine A
5. Firestore update ไหม?
   - ✅ ถ้า update: Problem อยู่ที่ Machine B
   - ❌ ถ้าไม่ update: Check Rules
```

#### วิธี D: Force Refresh Both Machines
```
Machine A & B (ทำทั้งสองเครื่อง):
1. Ctrl+Shift+Delete (Clear cache)
2. Select "All time"
3. Clear data
4. F12 → Console → localStorage.clear()
5. Ctrl+F5 (Hard refresh)
6. Close & reopen browser
7. ลอกอิน
8. ลองเพิ่มสินค้า
```

---

## 6️⃣ **"Failed to fetch config" - Firebase initialization error**

### 🔴 Problem
```
Browser Console:
error: Failed to fetch config from Firebase
```

### ✅ Solutions

#### วิธี A: ตรวจสอบ URL
```
1. index.html อยู่ที่ไหน?
2. ถ้า: C:/Users/Desktop/index.html
   - เปิด ด้วย: file:///C:/Users/Desktop/index.html
3. ไม่ใช่ http:// หรือ https://
```

#### วิธี B: ตรวจสอบ Firestore Rules
```
Rules ต้องอนุญาต anonymous users:

allow read, write: if request.auth != null;

✓ publish แล้ว?
```

#### วิธี C: Check Console Errors
```
1. F12 → Console
2. ดูข้อความแดง ทั้งหมด
3. ค้นหา "CORS" หรือ "403"
4. ลอก error message แล้วแก้
```

---

## 7️⃣ **"The caller does not have permission" - Firestore write error**

### 🔴 Problem
```
เพิ่มสินค้า แล้ว error:
"The caller does not have permission to execute the specified operation"
```

### ✅ Solutions

#### วิธี A: ตรวจสอบ Rules
```
Firestore Rules ต้องมี:
allow write: if request.auth != null;

(ไม่ใช่ read-only)
```

#### วิธี B: Publish Rules Again
```
1. Firestore → Rules
2. หาก "Draft":
   - Publish
   - รอ 1-2 นาที
```

#### วิธี C: Re-authenticate
```
1. Logout (Header → Logout)
2. Clear localStorage: F12 → Console → localStorage.clear()
3. F5 reload
4. Login again
```

---

## 8️⃣ **Sidebar ซ่อนหายหรือ Layout หลวม**

### 🔴 Problem
```
- Sidebar ไม่เห็น
- Layout ไม่สมดุล
- Text เล็กเกินไป
```

### ✅ Solutions

#### วิธี A: Refresh & Clear Cache
```
1. Ctrl+F5 (Hard refresh)
2. Ctrl+Shift+Delete (Clear cache)
3. F5 (Reload)
```

#### วิธี B: Zoom Reset
```
กด Ctrl+0 (Reset zoom to 100%)
```

#### วิธี C: Check Browser Width
```
- Mobile: Sidebar อาจ collapse
- Desktop: ควรเห็น sidebar เต็ม
- F12 → Responsive design mode
```

---

## 9️⃣ **History/Transaction ไม่เห็น**

### 🔴 Problem
```
เพิ่ม GR/GI แล้ว
แต่ History ไม่เห็น
```

### ✅ Solutions

#### วิธี A: ตรวจสอบเข้า correct view
```
1. Dashboard → Inbound → "GR History (ประวัติรับเข้า)"
2. ลองเพิ่มสินค้า ด้วย "Add packaging material stock"
3. Submit → ข้อมูลจะ update ที่ History
```

#### วิธี B: Refresh
```
1. F5 reload page
2. ลอกอิน
3. ไป History view
```

#### วิธี C: Check Firestore
```
1. Firebase → Firestore → Data
2. ค้นหา "grHistory" หรือ "giHistory"
3. ถ้าว่าง = data ไม่บันทึก
4. Check if sync "Cloud Sync Active"
```

---

## 🔟 **Page ช้าหรือ Freeze**

### 🔴 Problem
```
- Click ไม่ตอบสนอง
- Loading ติดค้าง
- RAM/CPU สูง
```

### ✅ Solutions

#### วิธี A: Close Other Tabs
```
1. ปิด tab อื่น ๆ
2. ลดการใช้ memory
3. Reload WMS page
```

#### วิธี B: Clear LocalStorage
```
1. F12 → Console
2. localStorage.clear()
3. sessionStorage.clear()
4. F5 reload
```

#### วิธี C: Use Firefox/Chrome
```
- ถ้าใช้ Safari: ลอง Chrome
- ถ้าใช้ Edge: ลอง Chrome
- Chrome มักเร็วกว่า
```

#### วิธี D: Restart Browser
```
1. ปิดเบราว์เซอร์ทั้งหมด
2. รอ 10 วินาที
3. เปิดใหม่
4. เปิด index.html
```

---

## 🆘 **ยังแก้ไม่ได้?**

### โปรดตรวจสอบ:

1. **Firebase Config**
   ```
   ✓ apiKey ไม่เริ่มด้วย "YOUR_"
   ✓ projectId ถูกต้อง
   ✓ authDomain มี firebaseapp.com
   ```

2. **Firestore Rules**
   ```
   ✓ Published (ไม่ Draft)
   ✓ มี allow read, write: if request.auth != null;
   ```

3. **Anonymous Auth**
   ```
   ✓ Enable toggle เปิด
   ✓ ดู Authentication → Sign-in method
   ```

4. **Browser Console**
   ```
   F12 → Console → ดูข้อความแดง
   ✓ Copy error message
   ✓ Google search
   ```

5. **Network**
   ```
   ✓ Internet เชื่อม
   ✓ ลอง restart WiFi
   ✓ Firewall ปิด?
   ```

---

**Still Need Help?**
- ดู README.md สำหรับ overview
- ดู FIREBASE-SETUP-TH.md สำหรับ setup step-by-step
- Check browser console (F12) สำหรับ error messages