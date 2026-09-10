# 🔧 Troubleshooting Guide (ภาษาไทย)

## ❌ ปัญหา & ✅ วิธีแก้

---

## 1. "Connecting Sync..." ติดค้าง

### ✅ วิธีแก้:
```
1. ตรวจสอบ FIREBASE_CONFIG ใน index.html
   - apiKey ต้องไม่เป็น "YOUR_API_KEY"
   - projectId ต้องถูกต้อง

2. ตรวจสอบ Firestore Rules
   - Firebase → Firestore → Rules
   - ต้อง Publish แล้ว (ไม่ Draft)

3. Clear Cache & Reload
   - Ctrl+Shift+Delete
   - Select "All time"
   - Clear data
   - F5 reload

4. Check Browser Console (F12)
   - ดูว่า error อะไร
   - Screenshot error message
```

---

## 2. "Connected (Local Mode)"

### ✅ วิธีแก้:
```
= Firebase Config ยังไม่ตั้ง

1. เปิด index.html ด้วย Text Editor
2. ค้นหา FIREBASE_CONFIG (Ctrl+F)
3. ตรวจสอบว่ามี "YOUR_" เหลืออยู่ไหม?
   ❌ apiKey: "YOUR_API_KEY"
   ✅ apiKey: "AIzaSy_xxxx"

4. Copy config ใหม่จาก Firebase Console
   - Project Settings → General
   - "Your apps" → Copy firebaseConfig

5. Save & Reload (Ctrl+F5)
```

---

## 3. "Cloud Sync Error: permission-denied"

### ✅ วิธีแก้:
```
1. Firebase Console → Firestore Database → Rules tab
2. ตรวจสอบ status:
   ❌ "Draft" = ยังไม่ publish
   ✅ "Published" = publish แล้ว

3. ถ้า Draft: Click "Publish"
4. รอ 1-2 นาที
5. Reload page (Ctrl+F5)
```

---

## 4. Login ไม่ได้

### ✅ วิธีแก้:
```
Demo Users:
- admin / admin123
- anyawee.t / 1234
- staff01 / 1234

ตรวจสอบ:
1. Username case-sensitive (ตัวเล็กตัวใหญ่)
2. ไม่มี space ตัวเกิน
3. Password ถูกต้อง

ถ้ายังไม่ได้:
1. F12 → Console → localStorage.clear()
2. F5 reload
3. Login ใหม่
```

---

## 5. ข้อมูลไม่ sync ระหว่างเครื่อง

### ✅ วิธีแก้:
```
ตรวจสอบ:
1. ทั้งสองเครื่องใช้ HTML file เดียวกัน?
2. ทั้งสองเครื่องมี FIREBASE_CONFIG เดียวกัน?
3. ทั้งสองเครื่องแสดง "Cloud Sync Active"?
   ❌ "Connected (Local Mode)" = ตั้ง config ใหม่

4. ล้าง Cache & Reload ทั้งสอง:
   - Ctrl+Shift+Delete
   - F12 → Console → localStorage.clear()
   - Ctrl+F5 reload
   - Login ใหม่

5. Firestore Console
   - ดู Data tab
   - เพิ่มสินค้า Machine A
   - Machine A firestore update ไหม?
   - Machine B page update ไหม?
```

---

## 6. Sidebar/Layout หลวม

### ✅ วิธีแก้:
```
1. Ctrl+F5 (Hard refresh)
2. Ctrl+0 (Reset zoom to 100%)
3. Close all other tabs (ลด memory usage)
4. Refresh page
```

---

## 7. Page ช้า/Freeze

### ✅ วิธีแก้:
```
1. Close other browser tabs
2. F12 → Console → localStorage.clear()
3. Restart browser
4. ลอง Chrome แทน Safari/Edge
```

---

## 8. Firebase Config Copy มาแล้ว แต่ยังติด

### ✅ วิธีแก้:
```
1. ตรวจสอบว่า:
   ✓ projectId ตรงกัน
   ✓ apiKey ไม่มี space
   ✓ authDomain มี firebaseapp.com

2. Copy ใหม่แล้ว Replace ทั้งหมด

3. Save & Reload (Ctrl+F5)

4. Check Firestore Rules:
   - allow read, write: if request.auth != null;
   - Publish ?

5. F12 → Console ดู error
```

---

## 📞 ยังแก้ไม่ได้?

### ทำตามนี้:
```
1. อ่าน FIREBASE-SETUP-TH.md ใหม่ (ข้อไหนพลาดไป?)
2. Check browser console (F12) ดู error message
3. ล้าง cache ทั้งหมด (Ctrl+Shift+Delete)
4. ปิด browser ไป 10 วินาที
5. เปิด browser ใหม่
6. เปิด index.html ใหม่
7. ลอง login
```

---

**✨ Good Luck! 🚀**
